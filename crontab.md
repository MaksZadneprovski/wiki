`cron` — это утилита для планирования задач (cron jobs) в Unix-подобных системах. Она позволяет автоматизировать выполнение сценариев или команд в определенное время или по определенному расписанию. Файл расписания, используемый `cron`, называется `crontab`.

**Основные особенности `cron`:**

1. **Планирование задач**: `cron` позволяет запускать задачи с определенной периодичностью: ежеминутно, ежечасно, ежедневно, еженедельно и т.д.
2. **Файл конфигурации `crontab`**: Каждому пользователю разрешается иметь собственный файл `crontab`, что позволяет управлять задачами на уровне пользователя.
3. **Простота использования**: Настройка задач с помощью `cron` довольно проста и не требует глубоких знаний системного администрирования.
4. **Примеры использования**: Ежедневное резервное копирование, очистка временных файлов, отправка отчетов по электронной почте и т.д.

**Пример записи в `crontab`:**

Откройте редактор crontab для редактирования заданий:

```bash
sudo crontab -e
```

```sccc
# минута (0-59) час (0-23) день_месяца (1-31) месяц (1-12) день_недели (0-7, где 0 и 7 — воскресенье) 0 2 * * * /usr/local/bin/backup.sh
```

Эта запись запускает скрипт `backup.sh` каждый день в 2 часа ночи.