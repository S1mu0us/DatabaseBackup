# [Задание](https://github.com/netology-code/sdb-homeworks/blob/main/12-08.md) к занятию "`Резервное копирование баз данных`"

---

### Задание 1
#### 1.1
Необходимо делать бекап ежедневно, подойдёт полное резервное копирование, пожертвовав объемом хранения.
#### 1.2
Нужны инкрементные бекапы, т.е. копируя только последние изменения. Ещё можно использовать журнал транзакций с базовым бекапом в PostgreSQL/MySQL.

---

### Задание 2

```bash
pg_dump -U [имя_пользователя] -F c -b -v -f [имя_файла] [имя_базы]
```

---

### Задание 3

Копирование
```bash
xtrabackup --backup --target-dir=[куда_сохранить] --datadir=[рабочие_данные]
xtrabackup --backup --target-dir=[место_для_инкрементного_бэкапа] --incremental-basedir=[на_основе_какого_бэкапа] --datadir=[рабочие_данные]
xtrabackup --backup --target-dir=[место_для_другого_инкрементного_бэкапа] --incremental-basedir=[можно_сослаться_на_предыдущий] --datadir=/var/lib/mysql
```

Извлечение
```bash
xtrabackup --prepare --apply-log-only --target-dir=[куда_сохранено]
xtrabackup --prepare --apply-log-only --target-dir=[куда_сохранено] --incremental-dir=[место_инкрементного_бэкапа_1]
xtrabackup --prepare --apply-log-only --target-dir=[куда_сохранено] --incremental-dir=[место_инкрементного_бэкапа_2]
```

Обработка
```bash
xtrabackup --prepare --target-dir=[сохраненный_бекап]
```

Восстановление
```bash
xtrabackup --copy-back --target-dir=[сохраненный_бекап]
```

---
