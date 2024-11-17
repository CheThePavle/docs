
# Простое руководство по HTML

HTML (HyperText Markup Language) — это язык, который помогает создавать страницы в интернете. Представьте, что HTML — это скелет, на котором держится ваша веб-страница.

## Что такое HTML-документ?
Это обычный текстовый файл с расширением `.html`, который браузер понимает и отображает как страницу. Например:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Моя первая страница</title>
</head>
<body>
    <h1>Привет, мир!</h1>
    <p>Это моя первая страница на HTML.</p>
</body>
</html>
```

### Как это работает?
- **`<!DOCTYPE html>`**: сообщает браузеру, что мы используем HTML5.
- **`<html>`**: самый главный тег, в котором живёт весь наш код.
- **`<head>`**: скрытая часть страницы, где мы задаём настройки, такие как название.
- **`<body>`**: видимая часть страницы, которую видит пользователь.

---

## Теги — это строительные блоки HTML
Теги — это ключевые слова в угловых скобках, которые говорят браузеру, как показывать содержимое. Например:
- **`<h1>`**: заголовок.
- **`<p>`**: параграф (текст).
- **`<a>`**: ссылка.
- **`<img>`**: картинка.

---

## Примеры популярных тегов

### 1. Заголовки
Заголовки помогают разделять текст на логические блоки. Они бывают от `<h1>` до `<h6>`.

```html
<h1>Главный заголовок</h1>
<h2>Подзаголовок</h2>
<h3>Ещё меньше</h3>
```

### 2. Параграфы
Для текста используем тег `<p>`.

```html
<p>Это обычный текст на странице.</p>
```

### 3. Ссылки
Ссылки создаются с помощью тега `<a>`.

```html
<a href="https://google.com" target="_blank">Перейти в Google</a>
```
- **`href`**: адрес, куда ведёт ссылка.
- **`target="_blank"`**: открывает ссылку в новой вкладке.

### 4. Картинки
Картинки добавляются с помощью тега `<img>`.

```html
<img src="photo.jpg" alt="Описание картинки" width="500">
```
- **`src`**: путь к файлу с изображением.
- **`alt`**: текст, который показывается, если картинка не загрузилась.

---

## Работа с формами
Формы позволяют пользователю вводить данные, например, имя или email.

```html
<form action="/submit" method="post">
    <label for="username">Ваше имя:</label>
    <input type="text" id="username" name="username" required>
    
    <label for="email">Ваш email:</label>
    <input type="email" id="email" name="email" required>
    
    <input type="submit" value="Отправить">
</form>
```

- **`action`**: куда отправляются данные.
- **`method`**: как отправляются данные (`post` для конфиденциальных данных).

---

## Списки

### Нумерованные списки
Используйте тег `<ol>` для списков с числами.

```html
<ol>
    <li>Первый пункт</li>
    <li>Второй пункт</li>
    <li>Третий пункт</li>
</ol>
```

### Маркированные списки
Для списка с точками используйте `<ul>`.

```html
<ul>
    <li>Первый пункт</li>
    <li>Второй пункт</li>
    <li>Третий пункт</li>
</ul>
```

---

## Таблицы
Таблицы удобны для отображения данных в виде строк и колонок.

```html
<table border="1">
    <tr>
        <th>Имя</th>
        <th>Возраст</th>
    </tr>
    <tr>
        <td>Аня</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Миша</td>
        <td>30</td>
    </tr>
</table>
```
- **`<th>`**: заголовок колонки.
- **`<td>`**: ячейка таблицы.

---

## Полезные элементы
### Скрытые блоки
Используйте `<details>` и `<summary>` для создания блоков, которые можно раскрывать.

```html
<details>
    <summary>Нажмите, чтобы увидеть больше</summary>
    <p>Это скрытый текст!</p>
</details>
```

### Встраивание других страниц
Используйте `<iframe>`, чтобы показать содержимое другой страницы.

```html
<iframe src="https://example.com" width="600" height="400"></iframe>
```

---

## Пример полной страницы
```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Моя страница</title>
</head>
<body>
    <header>
        <h1>Добро пожаловать!</h1>
        <nav>
            <ul>
                <li><a href="#about">О нас</a></li>
                <li><a href="#services">Услуги</a></li>
                <li><a href="#contact">Контакты</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section id="about">
            <h2>О нас</h2>
            <p>Мы создаём красивые сайты.</p>
        </section>
        
        <section id="services">
            <h2>Услуги</h2>
            <ul>
                <li>Дизайн</li>
                <li>Разработка</li>
                <li>Поддержка</li>
            </ul>
        </section>
    </main>
    
    <footer>
        <p>Свяжитесь с нами: <a href="mailto:info@example.com">info@example.com</a></p>
    </footer>
</body>
</html>
```

Теперь вы знаете основы HTML! Попробуйте создать свою страницу прямо сейчас.

---

## Ресурсы для изучения
1. [MDN Web Docs на русском](https://developer.mozilla.org/ru/docs/Web/HTML)
2. [HTML Учебник на W3Schools](https://www.w3schools.com/html/)


## Основные теги HTML

### Семантические теги HTML5
Семантические теги помогают сделать код понятным как для разработчиков, так и для браузеров. Они описывают содержание страницы.

- `<header>`: Заголовок страницы или раздела.
- `<nav>`: Навигационное меню.
- `<main>`: Основное содержимое страницы.
- `<section>`: Раздел страницы, связанный по смыслу.
- `<article>`: Независимый контент (например, статья или пост).
- `<aside>`: Боковая информация (например, сайдбар или заметки).
- `<footer>`: Нижний колонтитул страницы или раздела.

Пример использования:
```html
<header>
    <h1>Добро пожаловать на мой сайт</h1>
</header>
<main>
    <section>
        <article>
            <h2>Мой первый пост</h2>
            <p>Это пример статьи на моей странице.</p>
        </article>
    </section>
    <aside>
        <p>Полезная информация: ссылки, контакты и т.д.</p>
    </aside>
</main>
<footer>
    <p>© 2024 Мой сайт</p>
</footer>
```

### Формы HTML
Формы позволяют пользователям взаимодействовать с сайтом, отправляя данные.

Основные элементы форм:
- `<form>`: Контейнер для формы.
- `<input>`: Поле ввода.
- `<textarea>`: Многострочное текстовое поле.
- `<button>`: Кнопка отправки.
- `<select>` и `<option>`: Выпадающий список.
- `<label>`: Описание для элементов формы.

Пример:
```html
<form action="/submit" method="POST">
    <label for="name">Имя:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <button type="submit">Отправить</button>
</form>
```

### Мультимедиа
HTML поддерживает встроенные элементы для мультимедиа, такие как видео и аудио.

Пример видео:
```html
<video controls width="600">
    <source src="example.mp4" type="video/mp4">
    Ваш браузер не поддерживает видео.
</video>
```

Пример аудио:
```html
<audio controls>
    <source src="example.mp3" type="audio/mpeg">
    Ваш браузер не поддерживает аудио.
</audio>
```

### Таблицы
Таблицы помогают структурировать данные.

Пример таблицы:
```html
<table>
    <thead>
        <tr>
            <th>Имя</th>
            <th>Возраст</th>
            <th>Город</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Анна</td>
            <td>25</td>
            <td>Москва</td>
        </tr>
        <tr>
            <td>Иван</td>
            <td>30</td>
            <td>Санкт-Петербург</td>
        </tr>
    </tbody>
</table>
```

## Новые возможности HTML5
### Локальное хранилище
Позволяет сохранять данные прямо в браузере.

Пример:
```html
<script>
    localStorage.setItem('username', 'Анна');
    console.log(localStorage.getItem('username')); // Вывод: Анна
</script>
```

### API для работы с геолокацией
Позволяет получать данные о местоположении пользователя.

Пример:
```html
<script>
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(function(position) {
            console.log("Широта: " + position.coords.latitude);
            console.log("Долгота: " + position.coords.longitude);
        });
    } else {
        console.log("Геолокация не поддерживается вашим браузером.");
    }
</script>
```

### Элемент `<canvas>`
Используется для рисования графики.

Пример:
```html
<canvas id="myCanvas" width="200" height="100"></canvas>
<script>
    const canvas = document.getElementById('myCanvas');
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = "blue";
    ctx.fillRect(20, 20, 150, 75);
</script>
```

