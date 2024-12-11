# Урок 1
pyenv

### Cтроковые префиксы

```python
r'сырой (raw) строковый литерал. Спец-символы не работают.'
b'байтовые строки - допускаются только символы ASCII (от 0 до 127).'
u'строки в Unicode. В python 3 по умолчанию, использоавть не обязательно.'
br'Некоторые префиксы можно комбинировать, например, сырые байтовые строки'
f'f-строки (форматированные строки). My name is {name}'
```

python - строгая динамическая типизация.
js - слабая динамическая типизация.

```python
print(type(0.1))
isinstance("line", str) #True
isinstance(123, int | float) #True
isinstance(123, int, float) #True
isinstance(True, int) #True
True + True # 2
```

# Урок 2

```python
a = "abcabc" 

#  Что менять, на что менять, сколько раз менять
a = a.replace("ab", "bc", 1)

# Перевернуть строку
a = a[::-1]

# Диапазон с шагом
a = a[0:6:2]

# Разделить по символам
a = a.split()    # По пробелу, не важно сколько пробелов подряд
a = a.split(" ") # Разделелиится по одному пробелу
a = a.split("s", 2) # Задать количество

# Количество подстрок
a = a.count("ab")

# Выбрасывает исключение, если нет подстроки
a = a.index("a") # Индекс вхождения подстроки
a = a.index("a", 5) # С какого символа начинать

# Возвращает -1, если нет подстроки
a = a.find("a") # Индекс вхождения подстроки
a = a.find("a", 5) # С какого символа начинать
```

```python
s1 = "abc"
s2 = "ab"
s2 += "c"

# Проверка ссылок на объекты (сравнивает id)
s1 is s2 # False
# Проверка символов
s1 is s2 # True

# Узнать id
id(s1)

```


# Лекция 1

Cookiecutter -  шаблоны проектов
pyproject.toml - почти стандарт 
vim - необходимо уметь пользоваться
Pre-commit Hooks
**pyenv** for python version managment
**pytest** for testing
**flake8** for linting
**black** for code formatiing
**isort** for sorting imports
**mypy** for type annotations
**pyupgrade** for syntax changes
**ruff** - the fastest python linter and auto-formatter
**makefile** for shortcuts
github action or gitlab CI

# Лекция 2. Дистрибуция кода и развертывание

Zip file
Zip import


```python

```

