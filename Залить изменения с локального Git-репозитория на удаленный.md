1. Добавьте удаленный репозиторий: Если вы ещё не добавили удаленный репозиторий, используйте команду: 
```bash
git remote add origin <URL удаленного репозитория>
```
[[git remote add origin|Суть команды git remote add origin]]

2. Выполните коммит в ветке:
```bash
git add .
git commit -m "коммент"
```

3. Выполните push в удаленный репозиторий:
```bash
git push -u origin ваша_ветка
```

Эти команды отправят ваши изменения в удаленный репозиторий. Если вам нужно обновить существующий удаленный репозиторий, используйте git push без указания ветки:

```bash
git push
```

#### Если адрес удаленного репозиторий изменился
```bash
git remote remove origin 
```

```bash
git remote add origin <URL удаленного репозитория>
```
