
# PostgreSQL: Методичка для начинающих

## Введение в PostgreSQL

PostgreSQL — это мощная, открытая реляционная база данных (СУБД), которая поддерживает расширения, соблюдение стандартов SQL и широкий спектр функций.

## Установка PostgreSQL

### На Windows
1. Скачайте установочный файл с официального сайта [postgresql.org](https://www.postgresql.org/).
2. Запустите установку, следуя инструкциям мастера установки.
3. Укажите порт (по умолчанию — 5432), задайте пароль администратора и выберите компоненты для установки.

### На Linux
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

### Проверка установки
После установки можно проверить статус PostgreSQL:
```bash
sudo systemctl status postgresql
```

## Основные команды работы с PostgreSQL

### Вход в PostgreSQL
```bash
sudo -u postgres psql
```

### Создание базы данных
```sql
CREATE DATABASE my_database;
```

### Подключение к базе данных
```bash
\c my_database
```

### Создание пользователя
```sql
CREATE USER my_user WITH PASSWORD 'my_password';
```

### Назначение привилегий пользователю
```sql
GRANT ALL PRIVILEGES ON DATABASE my_database TO my_user;
```

## Основные функции PostgreSQL

### Типы данных
- **Числовые:** `INTEGER`, `SMALLINT`, `BIGINT`, `NUMERIC`, `REAL`, `DOUBLE PRECISION`
- **Строковые:** `CHAR`, `VARCHAR`, `TEXT`
- **Дата и время:** `DATE`, `TIME`, `TIMESTAMP`, `INTERVAL`
- **Другие:** `BOOLEAN`, `JSON`, `UUID`, `ARRAY`

### Создание таблицы
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Вставка данных
```sql
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```

### Чтение данных
```sql
SELECT * FROM users;
```

### Обновление данных
```sql
UPDATE users SET name = 'Jane Doe' WHERE id = 1;
```

### Удаление данных
```sql
DELETE FROM users WHERE id = 1;
```

### Индексы
Для ускорения поиска можно создавать индексы:
```sql
CREATE INDEX idx_users_email ON users(email);
```

## Расширенные функции PostgreSQL

### Работа с JSON
```sql
CREATE TABLE json_example (
    id SERIAL PRIMARY KEY,
    data JSON
);

INSERT INTO json_example (data) VALUES ('{"key": "value"}');

SELECT data->>'key' AS key_value FROM json_example;
```

### Работа с массивами
```sql
CREATE TABLE array_example (
    id SERIAL PRIMARY KEY,
    tags TEXT[]
);

INSERT INTO array_example (tags) VALUES (ARRAY['tag1', 'tag2', 'tag3']);

SELECT tags[1] AS first_tag FROM array_example;
```

### Транзакции
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### Хранимые функции
```sql
CREATE OR REPLACE FUNCTION get_user_count() RETURNS INTEGER AS $$
BEGIN
    RETURN (SELECT COUNT(*) FROM users);
END;
$$ LANGUAGE plpgsql;
```

### Репликация и масштабирование
PostgreSQL поддерживает:
- **Стриминговую репликацию:** для создания резервных копий базы данных.
- **Шардинг:** через расширения, такие как `Citus`.

## Полезные команды
- Список баз данных: `\l`
- Список таблиц: `\dt`
- Схема таблицы: `\d table_name`
- Выход из psql: `\q`

## Полезные расширения
- `pg_stat_statements`: для анализа запросов.
- `PostGIS`: для работы с географическими данными.
- `pg_trgm`: для быстрого поиска по тексту.

## Резервное копирование и восстановление

### Экспорт базы данных
```bash
pg_dump my_database > backup.sql
```

### Импорт базы данных
```bash
psql my_database < backup.sql
```

## Полезные ссылки
- Официальная документация: [https://www.postgresql.org/docs/](https://www.postgresql.org/docs/)
- Сообщество PostgreSQL: [https://www.postgresql.org/community/](https://www.postgresql.org/community/)


## Работа с таблицами

### Создание таблиц
Пример создания таблицы с несколькими столбцами и различными типами данных:
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    position VARCHAR(50),
    salary NUMERIC(10, 2),
    hire_date DATE DEFAULT CURRENT_DATE
);
```

### Изменение таблиц
Добавление нового столбца:
```sql
ALTER TABLE employees ADD COLUMN department VARCHAR(50);
```
Изменение типа данных столбца:
```sql
ALTER TABLE employees ALTER COLUMN salary TYPE INTEGER;
```

Удаление столбца:
```sql
ALTER TABLE employees DROP COLUMN department;
```

### Удаление таблиц
```sql
DROP TABLE employees;
```

## Индексы

Индексы повышают производительность запросов:
```sql
CREATE INDEX idx_employees_name ON employees (name);
```

Удаление индекса:
```sql
DROP INDEX idx_employees_name;
```

## Резервное копирование и восстановление

### Резервное копирование базы данных
Использование `pg_dump` для создания дампа базы данных:
```bash
pg_dump my_database > my_database.sql
```

### Восстановление базы данных
```bash
psql my_database < my_database.sql
```

## Оптимизация запросов

### Использование EXPLAIN
Команда `EXPLAIN` помогает понять план выполнения запроса:
```sql
EXPLAIN SELECT * FROM employees WHERE salary > 50000;
```

### Анализ запросов с EXPLAIN ANALYZE
```sql
EXPLAIN ANALYZE SELECT * FROM employees WHERE salary > 50000;
```

### Рекомендации
- Используйте индексы для ускорения выборок.
- Избегайте использования `SELECT *` в больших таблицах.
- Разбивайте сложные запросы на более простые.

## Транзакции

### Основные команды
Начало транзакции:
```sql
BEGIN;
```

Подтверждение транзакции:
```sql
COMMIT;
```

Откат транзакции:
```sql
ROLLBACK;
```

### Пример
```sql
BEGIN;
UPDATE employees SET salary = salary * 1.1 WHERE position = 'Manager';
ROLLBACK; -- Если нужно отменить изменения
```

## Расширения PostgreSQL

### Установка расширений
Пример установки расширения `uuid-ossp` для работы с UUID:
```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

### Использование расширения PostGIS
PostGIS добавляет поддержку географических данных:
```sql
CREATE EXTENSION IF NOT EXISTS postgis;
```
Пример создания таблицы с географическим столбцом:
```sql
CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    coordinates GEOGRAPHY(Point, 4326)
);
```

## Распространённые ошибки и их исправление

### Ошибка подключения
- Убедитесь, что PostgreSQL работает:
  ```bash
  sudo systemctl start postgresql
  ```
- Проверьте настройки `pg_hba.conf`.

### Ошибка синтаксиса
- Проверьте корректность SQL-запроса.
- Используйте `psql` для пошагового выполнения команд.

### Блокировка таблиц
- Узнайте, какая транзакция держит блокировку:
  ```sql
  SELECT * FROM pg_stat_activity WHERE state = 'active';
  ```

