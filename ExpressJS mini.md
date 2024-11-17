
# Методичка по Express.js

## 1. Введение в Express.js

### Что такое Express.js?
Express.js — это минималистичный и гибкий веб-фреймворк для Node.js, который позволяет быстро и просто создавать серверные веб-приложения и API. Он предоставляет набор инструментов для обработки HTTP-запросов, маршрутизации, работы с middleware и многого другого.

### Установка и настройка
Перед началом работы убедитесь, что у вас установлен **Node.js** и **npm**. Для установки Express выполните команду:

```bash
npm install express
```

### Создание простого сервера

```javascript
// server.js
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello, Express!');
});

app.listen(PORT, () => {
  console.log(`Сервер запущен на http://localhost:${PORT}`);
});
```

Для запуска сервера выполните команду:

```bash
node server.js
```

## 2. Базовые концепции

### Маршруты (Routes)
Маршрут в Express определяет, как сервер должен обрабатывать запросы к определённым URL.

```javascript
app.get('/users', (req, res) => {
  res.send('Список пользователей');
});

app.post('/users', (req, res) => {
  res.send('Создать пользователя');
});
```

### Middleware
Middleware — это функции, которые выполняются во время обработки запроса до отправки ответа.

```javascript
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

### Обработка запросов (GET, POST, PUT, DELETE)
```javascript
app.get('/item/:id', (req, res) => {
  const { id } = req.params;
  res.send(`Получение элемента с ID: ${id}`);
});

app.post('/item', (req, res) => {
  res.send('Элемент создан');
});

app.put('/item/:id', (req, res) => {
  res.send(`Элемент с ID ${req.params.id} обновлён`);
});

app.delete('/item/:id', (req, res) => {
  res.send(`Элемент с ID ${req.params.id} удалён`);
});
```

## 3. Работа с шаблонизаторами

### Подключение шаблонизатора Pug
```bash
npm install pug
```

```javascript
app.set('view engine', 'pug');
app.set('views', './views');

app.get('/hello', (req, res) => {
  res.render('index', { title: 'Привет', message: 'Добро пожаловать!' });
});
```

**Файл views/index.pug**
```pug
doctype html
html
  head
    title= title
  body
    h1= message
```

## 4. API и работа с данными

### Создание REST API и подключение к MongoDB с использованием Mongoose

```bash
npm install mongoose
```

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('MongoDB подключена'))
  .catch(err => console.error(err));

const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
});

const User = mongoose.model('User', userSchema);

app.get('/api/users', async (req, res) => {
  const users = await User.find();
  res.json(users);
});
```

## 5. Безопасность и аутентификация

### Работа с CORS
```bash
npm install cors
```

```javascript
const cors = require('cors');
app.use(cors());
```

### Аутентификация с JWT
```bash
npm install jsonwebtoken
```

```javascript
const jwt = require('jsonwebtoken');

app.post('/login', (req, res) => {
  const token = jwt.sign({ userId: 123 }, 'secret_key', { expiresIn: '1h' });
  res.json({ token });
});
```

## 6. Дополнительные фичи

### Работа с файлами
```bash
npm install multer
```

```javascript
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('Файл загружен');
});
```

### Логирование и обработка ошибок
```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Что-то пошло не так!');
});
```

## 7. Деплой на Heroku
```bash
heroku login
heroku create
git push heroku main
```

## 8. Полезные советы и практики

- **Структура проекта**:
  ```
  ├── controllers
  ├── models
  ├── routes
  ├── views
  ├── .env
  └── server.js
  ```

- **Использование .env файлов**:
  ```bash
  npm install dotenv
  ```

  **Пример**:
  ```javascript
  require('dotenv').config();
  const PORT = process.env.PORT || 3000;
  ```

- **Рекомендации по тестированию**:
  ```bash
  npm install mocha chai supertest
  ```

## Заключение
Express.js — это мощный инструмент для создания веб-приложений и API. Изучив основы, вы сможете разрабатывать сложные проекты и интегрировать их с другими сервисами.

**Удачи в разработке!**
