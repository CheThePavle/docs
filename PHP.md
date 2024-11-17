
# Подробное учебное руководство по PHP

PHP — это серверный язык программирования, который используется для создания веб-приложений. Эта методичка объяснит основные концепции, синтаксис, а также покажет полезные библиотеки и практики.

---

## 1. Установка PHP

### Установка на Windows:
1. Скачайте PHP с сайта: [php.net](https://www.php.net/downloads).
2. Распакуйте архив в любую папку (например, `C:\php`).
3. Добавьте папку PHP в переменные окружения PATH.

### Установка на macOS:
Если у вас установлен Homebrew:
```bash
brew install php
```

### Установка на Linux:
```bash
sudo apt update
sudo apt install php
```

### Проверка версии:
```bash
php -v
```

---

## 2. Первая программа на PHP

Создайте файл `hello.php` и напишите:
```php
<?php
echo "Hello, World!";
?>
```

Запустите в терминале:
```bash
php hello.php
```

---

## 3. Основы синтаксиса

### Переменные
Переменные в PHP начинаются с `$`.
```php
<?php
$name = "PHP";
$age = 25;
$is_active = true;

echo "Язык: $name, Возраст: $age";
?>
```

### Типы данных
- `string` — строки
- `int` — целые числа
- `float` — числа с плавающей точкой
- `bool` — логические значения (true/false)
- `array` — массивы
- `object` — объекты
- `NULL` — пустое значение

---

## 4. Условные конструкции

```php
<?php
$age = 20;

if ($age < 18) {
    echo "Моложе 18.";
} elseif ($age == 18) {
    echo "Вам ровно 18.";
} else {
    echo "Старше 18.";
}
?>
```

---

## 5. Циклы

### Цикл `for`:
```php
<?php
for ($i = 0; $i < 5; $i++) {
    echo $i . "\n";
}
?>
```

### Цикл `while`:
```php
<?php
$count = 0;
while ($count < 5) {
    echo $count . "\n";
    $count++;
}
?>
```

---

## 6. Функции

Функции помогают переиспользовать код.

### Пример функции:
```php
<?php
function greet($name) {
    return "Привет, $name!";
}

echo greet("Мир");
?>
```

---

## 7. Массивы

### Одномерные массивы:
```php
<?php
$fruits = ["яблоко", "банан", "вишня"];
echo $fruits[1]; // банан
?>
```

### Ассоциативные массивы:
```php
<?php
$person = ["name" => "Иван", "age" => 30];
echo $person["name"]; // Иван
?>
```

---

## 8. Работа с файлами

### Чтение файла:
```php
<?php
$content = file_get_contents("example.txt");
echo $content;
?>
```

### Запись в файл:
```php
<?php
file_put_contents("example.txt", "Hello, PHP!");
?>
```

---

## 9. Работа с базами данных (MySQL)

### Подключение к базе:
```php
<?php
$conn = new mysqli("localhost", "username", "password", "database");

if ($conn->connect_error) {
    die("Ошибка подключения: " . $conn->connect_error);
}
echo "Успешное подключение!";
?>
```

### Выполнение запроса:
```php
<?php
$sql = "SELECT * FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "Имя: " . $row["name"] . "\n";
    }
} else {
    echo "Нет данных";
}
$conn->close();
?>
```

---

## 10. Полезные библиотеки и фреймворки

1. **Composer** — менеджер зависимостей.
   Установка:
   ```bash
   curl -sS https://getcomposer.org/installer | php
   mv composer.phar /usr/local/bin/composer
   ```
   Использование:
   ```bash
   composer require <package>
   ```

2. **Laravel** — мощный фреймворк для веб-разработки.
   Установка:
   ```bash
   composer global require laravel/installer
   laravel new myproject
   ```

3. **Guzzle** — HTTP-клиент.
   Установка:
   ```bash
   composer require guzzlehttp/guzzle
   ```

   Пример использования:
   ```php
   <?php
   require 'vendor/autoload.php';

   use GuzzleHttp\Client;

   $client = new Client();
   $response = $client->request('GET', 'https://api.github.com');

   echo $response->getBody();
   ?>
   ```

4. **PHPUnit** — инструмент для тестирования.
   Установка:
   ```bash
   composer require --dev phpunit/phpunit
   ```

---

## 11. Работа с API

Пример запроса к API:
```php
<?php
$url = "https://api.example.com/data";
$response = file_get_contents($url);
$data = json_decode($response, true);

print_r($data);
?>
```

---

## Заключение

PHP остается актуальным и мощным инструментом для веб-разработки. Используйте современные библиотеки и фреймворки, чтобы создавать надежные и масштабируемые приложения.


---

## 12. Подробнее о синтаксисе PHP

### Комментарии
Комментарии помогают документировать код:
```php
<?php
// Однострочный комментарий

/*
Многострочный
комментарий
*/

# Альтернативный однострочный комментарий
?>
```

---

## 13. Подключение файлов

PHP позволяет подключать внешние файлы с помощью `include` и `require`.

### Пример:
```php
<?php
// В файле header.php
echo "<h1>Заголовок страницы</h1>";

// В основном файле
include "header.php"; // Или require "header.php";
?>
```

Разница:
- `include` — продолжает выполнение, даже если файл отсутствует.
- `require` — вызывает ошибку и завершает выполнение, если файл отсутствует.

---

## 14. Подробно о функциях

### Функции с параметрами по умолчанию:
```php
<?php
function greet($name = "Гость") {
    return "Привет, $name!";
}

echo greet(); // Привет, Гость!
echo greet("Иван"); // Привет, Иван!
?>
```

### Анонимные функции:
```php
<?php
$sum = function($a, $b) {
    return $a + $b;
};

echo $sum(3, 5); // 8
?>
```

---

## 15. Обработка форм

### Пример обработки POST-запроса:
HTML-форма:
```html
<form method="POST" action="process.php">
    <input type="text" name="username" placeholder="Имя пользователя">
    <button type="submit">Отправить</button>
</form>
```

PHP-код (`process.php`):
```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = htmlspecialchars($_POST["username"]);
    echo "Привет, $username!";
}
?>
```

---

## 16. Сессии и куки

### Работа с сессиями:
```php
<?php
// Начало сессии
session_start();

// Установка значения
$_SESSION["username"] = "Иван";

// Доступ к значению
echo $_SESSION["username"];
?>
```

### Работа с куки:
```php
<?php
// Установка куки
setcookie("user", "Иван", time() + 3600); // 1 час

// Доступ к куки
if (isset($_COOKIE["user"])) {
    echo "Привет, " . $_COOKIE["user"];
}
?>
```

---

## 17. ООП в PHP

### Основы ООП:
```php
<?php
class Car {
    public $brand;
    private $speed;

    public function __construct($brand, $speed) {
        $this->brand = $brand;
        $this->speed = $speed;
    }

    public function getSpeed() {
        return $this->speed;
    }
}

$car = new Car("Toyota", 120);
echo $car->brand; // Toyota
echo $car->getSpeed(); // 120
?>
```

### Наследование:
```php
<?php
class Vehicle {
    public $type;

    public function __construct($type) {
        $this->type = $type;
    }
}

class Bike extends Vehicle {
    public $wheels;

    public function __construct($type, $wheels) {
        parent::__construct($type);
        $this->wheels = $wheels;
    }
}

$bike = new Bike("Mountain Bike", 2);
echo $bike->type; // Mountain Bike
echo $bike->wheels; // 2
?>
```

---

## 18. Полезные библиотеки и фреймворки (дополнительно)

1. **Monolog** — мощная библиотека для логирования.
   Установка:
   ```bash
   composer require monolog/monolog
   ```

   Использование:
   ```php
   <?php
   require 'vendor/autoload.php';

   use Monolog\Logger;
   use Monolog\Handler\StreamHandler;

   $log = new Logger('name');
   $log->pushHandler(new StreamHandler('app.log', Logger::WARNING));

   $log->warning('Это предупреждение');
   ?>
   ```

2. **PHPMailer** — отправка писем через SMTP.
   Установка:
   ```bash
   composer require phpmailer/phpmailer
   ```

   Пример:
   ```php
   <?php
   use PHPMailer\PHPMailer\PHPMailer;

   $mail = new PHPMailer();
   $mail->setFrom('from@example.com');
   $mail->addAddress('to@example.com');
   $mail->Subject = 'Тема письма';
   $mail->Body = 'Содержимое письма';

   if (!$mail->send()) {
       echo "Ошибка: " . $mail->ErrorInfo;
   } else {
       echo "Письмо отправлено!";
   }
   ?>
   ```

---

## 19. Рекомендации по написанию кода

1. **PSR-12**: Следуйте стандарту кодирования PHP.
2. **Документируйте код**: Используйте PHPDoc для описания функций и классов.
3. **Безопасность**:
   - Проверяйте входные данные (`htmlspecialchars`, `filter_input`).
   - Используйте подготовленные запросы для работы с базой данных.
4. **Автоматическое тестирование**: Используйте PHPUnit для написания тестов.

---

## Заключение

Эта методичка охватывает основные и продвинутые темы PHP. Следуйте этим рекомендациям, изучайте документацию и практикуйтесь, чтобы стать профессионалом.


---

## 7. Советы по производительности PHP

1. **Используйте кеширование**:
   - Используйте OPcache для ускорения исполнения кода.
   - Применяйте сторонние системы кеширования, такие как Redis или Memcached.

2. **Минимизируйте использование include/require**:
   - Объединяйте файлы, где это возможно.

3. **Оптимизируйте SQL-запросы**:
   - Используйте подготовленные запросы.
   - Применяйте индексы в базах данных.

4. **Избегайте использования `eval()`**:
   - Это не только замедляет выполнение, но и представляет угрозу безопасности.

5. **Работа с массивами**:
   - Используйте функции с нативной поддержкой PHP, такие как `array_map()` и `array_filter()`.

---

## 8. Безопасность в PHP

1. **Санитизация ввода**:
   - Используйте фильтры, такие как `filter_input()` и `htmlspecialchars()`.

2. **Защита от SQL-инъекций**:
   - Всегда применяйте подготовленные запросы с PDO или MySQLi.

3. **Защита от XSS-атак**:
   - Экранируйте пользовательский ввод, отображаемый в браузере.

4. **Используйте HTTPS**:
   - Защитите данные, передаваемые между клиентом и сервером.

5. **Избегайте утечек ошибок**:
   - Отключите вывод ошибок на продакшене, используя `error_reporting(0)`.

---

## 9. Отладка PHP

1. **Используйте встроенные функции**:
   - `var_dump()`, `print_r()`, `debug_backtrace()`.

2. **Применяйте Xdebug**:
   - Настройте Xdebug для пошаговой отладки.

3. **Логирование**:
   - Используйте `error_log()` для записи ошибок в логи.

4. **PHPUnit**:
   - Покрывайте код юнит-тестами.

---

## 10. Популярные фреймворки PHP

1. **Laravel**:
   - Прост в изучении, предлагает мощные возможности (маршрутизация, ORM Eloquent).
   - Используйте Artisan для автоматизации задач.

2. **Symfony**:
   - Подходит для сложных проектов, высоко конфигурируемый.
   - Применяет компоненты, которые можно интегрировать в другие проекты.

3. **CodeIgniter**:
   - Легковесный фреймворк с минимальным потреблением ресурсов.

4. **Yii**:
   - Отлично подходит для API-разработки и масштабируемых приложений.

---

## 11. Работа с базами данных

1. **PDO**:
   - Пример подключения:
     ```php
     $dsn = 'mysql:host=localhost;dbname=testdb';
     $username = 'root';
     $password = '';
     $options = [PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION];
     $pdo = new PDO($dsn, $username, $password, $options);
     ```

2. **Миграции**:
   - Используйте миграции для управления схемой базы данных (например, в Laravel).

3. **ORM**:
   - Применяйте Object-Relational Mapping для работы с базой как с объектами.

---

## 12. Полезные библиотеки

1. **Composer**:
   - Используйте Composer для управления зависимостями.

2. **PHPMailer**:
   - Для отправки email.

3. **Monolog**:
   - Логирование на профессиональном уровне.

4. **Guzzle**:
   - Работа с HTTP-запросами.

---

