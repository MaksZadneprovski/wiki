**AVR-libc** — это официальная библиотека для работы с микроконтроллерами AVR на языке C. Она предоставляет доступ к регистрам, периферии, а также функции для низкоуровневого программирования.

#### **Ключевые разделы документации AVR-libc**:

1. **<avr/io.h>**:
   - Доступ к регистрам микроконтроллера.
   - Например, чтобы управлять пинами порта:
```c
DDRB |= (1 << PB5); // Установить пин PB5 как выход
PORTB |= (1 << PB5); // Установить высокий уровень на PB5
```

2. **<util/delay.h>**:
  - Простая реализация задержек:
```c
_delay_ms(1000); // Задержка на 1000 мс
```

3. **<avr/interrupt.h>**:
  - Управление прерываниями:
```c
sei();  // Разрешить глобальные прерывания
cli();  // Запретить глобальные прерывания
```

4. **<avr/eeprom.h>**:
   - Работа с EEPROM:
```c
uint8_t value = eeprom_read_byte((uint8_t*)0x00); // Чтение из EEPROM
eeprom_write_byte((uint8_t*)0x00, 42); // Запись в EEPROM
```
