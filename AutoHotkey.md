[[Переназначение CapsLock для смены раскладки]]
[[Автоматический запуск скриптов]]

AutoHotkey (AHK) — это мощный и гибкий инструмент для автоматизации задач на компьютере под управлением Windows. Вот несколько возможностей, которые предоставляет AutoHotkey, помимо переназначения клавиш:

### 1. **Автоматизация задач**

- **Автоматизация повторяющихся задач:** AHK может выполнять повторяющиеся действия, такие как открытие программ, ввод текста и нажатие кнопок.
- **Заполнение форм:** AHK может автоматически заполнять веб-формы или другие виды форм.

### 2. **Создание горячих клавиш**

- **Горячие клавиши для запуска программ:** Вы можете создать горячие клавиши для быстрого запуска приложений или файлов.
- **Сочетания клавиш:** AHK позволяет создавать сложные сочетания клавиш для выполнения различных действий.

### 3. **Создание макросов**

- **Запись макросов:** AHK может записывать последовательности действий и воспроизводить их по требованию.
- **Макросы для игр:** AHK часто используется для создания макросов для автоматизации действий в компьютерных играх.

### 4. **Работа с окнами и контролами**

- **Управление окнами:** AHK может перемещать, изменять размеры, скрывать и показывать окна, а также изменять их атрибуты.
- **Контроль над приложениями:** AHK может взаимодействовать с элементами управления в приложениях, такими как кнопки, текстовые поля и списки.

### 5. **Автоматизация ввода текста**

- **Автозамена текста:** AHK может автоматически заменять текст на лету, например, сокращения на полные фразы.
- **Ввод заранее определенного текста:** AHK может вводить заранее определенные блоки текста с помощью горячих клавиш.

### 6. **Работа с файлами и папками**

- **Автоматизация управления файлами:** AHK может создавать, перемещать, копировать и удалять файлы и папки.
- **Обработка файлов:** AHK может читать и записывать данные в файлы.

### 7. **Работа с буфером обмена**

- **Манипуляции с буфером обмена:** AHK может читать содержимое буфера обмена, изменять его и вставлять обратно.

### 8. **Создание графического интерфейса**

- **Создание GUI:** AHK позволяет создавать простые графические интерфейсы для ваших скриптов, такие как окна с кнопками, текстовыми полями и другими элементами управления.

### 9. **Системные уведомления и звуки**

- **Системные уведомления:** AHK может отображать всплывающие уведомления и сообщения.
- **Проигрывание звуков:** AHK может воспроизводить звуки и мелодии.

### 10. **Работа с сетью**

- **Сетевые запросы:** AHK может выполнять HTTP-запросы и взаимодействовать с веб-API.

### Пример использования:

#### Пример 1: Запуск программы с горячей клавишей

```
^!n::Run notepad.exe  ; Ctrl+Alt+N для запуска Блокнота

```
#### Пример 2: Автозамена текста

```
::btw::by the way  ; Автозамена "btw" на "by the way"

```
#### Пример 3: Автоматизация повторяющейся задачи


```
F1::
Loop 5  ; Повторить 5 раз
{
    Send, Hello
    Sleep, 1000  ; Пауза 1 секунда
}
return

```

#### Пример 4: Создание простого GUI

```
Gui, Add, Text,, Please enter your name:
Gui, Add, Edit, vName
Gui, Add, Button, gSubmit, Submit
Gui, Show
return

Submit:
Gui, Submit
MsgBox, Hello, %Name%!
return

```