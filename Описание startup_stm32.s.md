
#### 1. **Таблица векторов**

Секция `.isr_vector` содержит вектор прерываний, аналогичный таблице, написанной на C:

```asm
g_pfnVectors:
  .word  _estack            // Начальный указатель стека
  .word  Reset_Handler      // Обработчик сброса

  .word  NMI_Handler        // Non-Maskable Interrupt
  .word  HardFault_Handler  // Hard Fault
  .word  MemManage_Handler  // Memory Management Fault
  .word  BusFault_Handler   // Bus Fault
  .word  UsageFault_Handler // Usage Fault
  .word  0                  // Зарезервировано
  .word  0
  .word  0
  .word  0
  .word  SVC_Handler        // Supervisor Call (SVC)
  .word  DebugMon_Handler   // Debug Monitor
  .word  0
  .word  PendSV_Handler     // Pendable Service Interrupt
  .word  SysTick_Handler    // SysTick Timer

```

- Первый элемент: `_estack` — адрес начального указателя стека.
- Второй элемент: `Reset_Handler` — обработчик сброса, выполняемый сразу после включения питания или сброса процессора.
- Остальные элементы — обработчики исключений и прерываний.

---

#### 2. **Обработчик сброса (`Reset_Handler`)**

Обработчик сброса выполняет базовую инициализацию системы. Это аналог функции `Reset_Handler` в C.

```asm
Reset_Handler:
  ldr   r0, =_estack        // Загрузка начального значения указателя стека
  mov   sp, r0              // Установка стека

/* Копирование данных из флеш в SRAM */
  movs  r1, #0              // Обнуление регистра r1
  b     LoopCopyDataInit

CopyDataInit:
  ldr   r3, =_sidata        // Адрес начала данных в флеш
  ldr   r3, [r3, r1]        // Загрузка данных
  str   r3, [r0, r1]        // Копирование данных в SRAM
  adds  r1, r1, #4          // Смещение к следующему слову

LoopCopyDataInit:
  ldr   r0, =_sdata         // Начало секции .data
  ldr   r3, =_edata         // Конец секции .data
  adds  r2, r0, r1
  cmp   r2, r3              // Проверка на конец
  bcc   CopyDataInit        // Если не конец, продолжить

/* Обнуление секции .bss */
  ldr   r2, =_sbss          // Начало секции .bss
  b     LoopFillZerobss

FillZerobss:
  movs  r3, #0              // Обнуление текущего слова
  str   r3, [r2], #4        // Запись в память

LoopFillZerobss:
  ldr   r3, =_ebss          // Конец секции .bss
  cmp   r2, r3              // Проверка на конец
  bcc   FillZerobss         // Если не конец, продолжить

/* Инициализация системы и вызов main() */
  bl    systemInit          // Инициализация аппаратных блоков
  bl    __libc_init_array   // Вызов глобальных конструкторов C++
  bl    main                // Запуск основной программы
  bx    lr                  // Завершение обработчика
```
- **Копирование .data**: Значения переменных, хранящиеся во флеш, переносятся в оперативную память (SRAM).
- **Обнуление .bss**: Все неинициализированные переменные (секция `.bss`) обнуляются.
- **Запуск main**: После инициализации вызывается `main`.

---

#### 3. **Обработчик по умолчанию**

```asm
Default_Handler:
Infinite_Loop:
  b  Infinite_Loop
```

Этот обработчик используется для необработанных прерываний. Он просто зацикливается, позволяя разработчику отладить проблему.

---

#### 4.Слабый алиас (`weak`)
```
.weak      NMI_Handler
.thumb_set NMI_Handler,Default_Handler
```
**Директива `.weak`**:

```asm
.weak NMI_Handler
```
Эта строка объявляет символ `NMI_Handler` как слабый (weak). Это означает, что линковщик не будет выдавать ошибку, если нет другой реализации этой функции. Если пользовательская реализация отсутствует, символ будет связан с обработчиком по умолчанию.

**Директива `.thumb_set`**:
```asm
.thumb_set NMI_Handler, Default_Handler
```
Эта строка связывает слабый символ `NMI_Handler` с `Default_Handler`. То есть, если другая реализация `NMI_Handler` не найдена, будет использоваться адрес `Default_Handler`.

### **Как вызываются обработчики?**

1. **Прерывание или исключение**:
    
    - При возникновении события (например, SysTick) процессор определяет его векторный номер.
2. **Поиск обработчика**:
    
    - Из таблицы векторов вычисляется адрес обработчика: адрес=адрес_таблицы+(номер_вектора×4)\text{адрес} = \text{адрес\_таблицы} + (\text{номер\_вектора} \times 4)адрес=адрес_таблицы+(номер_вектора×4)
3. **Переход к обработчику**:
    
    - Процессор автоматически загружает значение из таблицы (адрес обработчика) и передаёт ему управление.
4. **Сохранение контекста**:
    
    - До перехода к обработчику процессор сохраняет регистры (PC, LR, xPSR и др.) в стек.
5. **Возврат из обработчика**:
    
    - Команда `BX LR` возвращает управление основной программе.


