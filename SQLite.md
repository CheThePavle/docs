
# Руководство по SQLite

SQLite — это легковесная встроенная реляционная база данных. Она хранит всю информацию в одном файле и не требует отдельного сервера для работы.

---

## Основные характеристики SQLite:
- **Легкость и простота использования**: SQLite не требует настройки сервера.
- **Встроенная**: Может быть использована прямо в приложении.
- **Один файл**: Все данные хранятся в одном `.sqlite` или `.db` файле.
- **ACID совместимость**: SQLite гарантирует надежность данных.
- **Поддержка SQL**: Поддерживает основной синтаксис SQL.

---

## Установка
SQLite обычно встроен в операционные системы. Для проверки установки:
```bash
sqlite3 --version
```

Если SQLite не установлен, загрузите его с официального сайта [SQLite](https://sqlite.org/download.html) и установите.

---

## Основные команды SQLite

### Создание базы данных
База данных создается автоматически при открытии нового файла:
```bash
sqlite3 my_database.db
```

### Основные SQL-команды
1. **Создание таблицы**:
    ```sql
    CREATE TABLE users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        email TEXT UNIQUE NOT NULL,
        age INTEGER
    );
    ```

2. **Добавление данных**:
    ```sql
    INSERT INTO users (name, email, age)
    VALUES ('Alice', 'alice@example.com', 30);
    ```

3. **Чтение данных**:
    ```sql
    SELECT * FROM users;
    ```

4. **Обновление данных**:
    ```sql
    UPDATE users
    SET age = 31
    WHERE name = 'Alice';
    ```

5. **Удаление данных**:
    ```sql
    DELETE FROM users
    WHERE name = 'Alice';
    ```

6. **Удаление таблицы**:
    ```sql
    DROP TABLE users;
    ```

---

## Полезные возможности SQLite

### 1. **Типы данных**
SQLite поддерживает динамическую типизацию. Основные типы:
- `NULL`: Отсутствие значения.
- `INTEGER`: Целые числа.
- `REAL`: Числа с плавающей запятой.
- `TEXT`: Строки.
- `BLOB`: Двоичные данные.

### 2. **Создание индекса**
Индексы ускоряют запросы:
```sql
CREATE INDEX idx_users_email ON users(email);
```

### 3. **Встроенные функции**
SQLite поддерживает множество функций:
- `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`
- Работа с текстом: `UPPER()`, `LOWER()`, `LENGTH()`
- Работа с датами: `DATE()`, `DATETIME()`

Пример:
```sql
SELECT UPPER(name) AS uppercase_name FROM users;
```

### 4. **Транзакции**
Для выполнения нескольких операций как одной:
```sql
BEGIN TRANSACTION;
INSERT INTO users (name, email, age) VALUES ('Bob', 'bob@example.com', 25);
UPDATE users SET age = 26 WHERE name = 'Bob';
COMMIT;
```

Если что-то пошло не так:
```sql
ROLLBACK;
```

### 5. **Привязка параметров**
Для защиты от SQL-инъекций используйте параметры:
```python
import sqlite3

conn = sqlite3.connect('my_database.db')
cursor = conn.cursor()

cursor.execute("INSERT INTO users (name, email, age) VALUES (?, ?, ?)", ('Charlie', 'charlie@example.com', 28))
conn.commit()
```

---

## Резервное копирование
Сохранение копии базы данных:
```bash
sqlite3 my_database.db ".backup backup_my_database.db"
```

---

## Инструменты для работы с SQLite
- **DB Browser for SQLite**: Графический интерфейс для работы с SQLite.
- **SQLiteStudio**: Простое и мощное приложение для управления базами данных SQLite.

---

## Советы и трюки

1. **Просмотр структуры таблицы**:
    ```sql
    PRAGMA table_info(users);
    ```

2. **Проверка всех таблиц в базе**:
    ```sql
    .tables
    ```

3. **Импорт и экспорт данных**:
    - Импорт:
        ```sql
        .import data.csv users
        ```
    - Экспорт:
        ```sql
        .output data.csv
        SELECT * FROM users;
        .output stdout
        ```

---

## Заключение
SQLite — мощный инструмент для локального хранения данных. Он идеально подходит для приложений, требующих встроенной базы данных без сложной настройки сервера.


---

## Расширенные запросы SQL

### 1. Создание сложных таблиц
Пример создания таблицы с ограничениями и значениями по умолчанию:
```sql
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY,
    customer_name TEXT NOT NULL,
    order_date TEXT DEFAULT (date('now')),
    total_amount REAL CHECK(total_amount > 0)
);
```

### 2. Работа с вложенными запросами
Пример использования вложенного SELECT:
```sql
SELECT customer_name, total_amount
FROM orders
WHERE total_amount > (SELECT AVG(total_amount) FROM orders);
```

### 3. Объединение данных
Использование объединения таблиц:
```sql
SELECT customers.name, orders.order_date, orders.total_amount
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id;
```

---

## Оптимизация производительности

1. **Используйте индексы**: Создавайте индексы на столбцы, часто используемые в WHERE и JOIN.
```sql
CREATE INDEX idx_orders_customer_id ON orders(customer_id);
```

2. **Включайте кеширование**: SQLite автоматически управляет кешем, но параметры можно настроить с помощью PRAGMA.
```sql
PRAGMA cache_size = 10000;
PRAGMA synchronous = NORMAL;
```

3. **Минимизируйте размер базы данных**:
   - Используйте типы данных с меньшим размером (например, INTEGER вместо TEXT).
   - Регулярно очищайте неиспользуемые данные с помощью `VACUUM`.

---

## Особенности использования SQLite

1. SQLite **не поддерживает** полноценный многопользовательский доступ. Это ограничение делает его идеальным для локальных приложений.
2. Отсутствие строгой схемы типов: SQLite не проверяет типы данных строго, что иногда может приводить к ошибкам.
3. SQLite **не поддерживает** хранимые процедуры.

---

## Безопасность

1. **Шифрование базы данных**: SQLite не имеет встроенного шифрования. Используйте сторонние библиотеки, такие как `SQLCipher`.
2. **Резервные копии**:
   - Создавайте бэкапы с использованием команды `.backup` в SQLite CLI.
   - Или делайте копии файла базы данных.

---

## Полезные инструменты

1. **DB Browser for SQLite**: Графический интерфейс для управления SQLite.
2. **SQLiteStudio**: Легкий инструмент для работы с SQLite.
3. **Python (sqlite3)**: Библиотека для интеграции SQLite в проекты на Python.

---

## Часто задаваемые вопросы

1. **Как восстановить базу данных?**
   Если база повреждена, используйте `.recover` в CLI для восстановления.

2. **Как работать с большими данными?**
   Убедитесь, что данные индексированы, и используйте стриминг запросов.

---

