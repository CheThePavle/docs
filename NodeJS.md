
# Методичка по Node.js

## Что такое Node.js?
Node.js — это платформа для выполнения JavaScript на серверной стороне. Она основана на движке V8 от Google Chrome и позволяет разрабатывать быстрые и масштабируемые сетевые приложения.

### Основные особенности Node.js
1. **Событийно-ориентированная архитектура**:
   Node.js использует событийный цикл, что делает его идеально подходящим для приложений реального времени.

2. **Неблокирующий ввод/вывод**:
   Запросы обрабатываются асинхронно, что позволяет масштабировать приложения без создания множества потоков.

3. **Единый язык**:
   Вы можете использовать JavaScript как для фронтенда, так и для серверной части.

4. **Модульная структура**:
   Node.js поддерживает модульную разработку с использованием CommonJS или ES6 модулей.

---

## Установка Node.js
1. Скачайте Node.js с [официального сайта](https://nodejs.org/).
2. Установите, следуя инструкциям.
3. Проверьте установку:
   ```bash
   node -v
   npm -v
   ```

---

## Основы работы с Node.js

### Ваш первый скрипт
Создайте файл `app.js`:
```javascript
console.log("Hello, Node.js!");
```

Запустите:
```bash
node app.js
```

### Работа с модулями
#### Импорт встроенного модуля
```javascript
const fs = require('fs');

fs.writeFileSync('hello.txt', 'Привет, мир!');
console.log('Файл создан');
```

#### Установка и использование внешних модулей
1. Установите модуль:
   ```bash
   npm install axios
   ```

2. Используйте его:
   ```javascript
   const axios = require('axios');

   axios.get('https://api.github.com')
       .then(response => console.log(response.data))
       .catch(error => console.error(error));
   ```

---

## Основные модули Node.js
1. **fs (File System)** — работа с файлами.
2. **http** — создание серверов.
3. **path** — работа с путями файлов.
4. **os** — информация о системе.

Пример создания сервера:
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, Node.js Server!');
});

server.listen(3000, () => {
    console.log('Сервер запущен на http://localhost:3000');
});
```

---

## Работа с пакетами через npm
- Установка глобального пакета:
  ```bash
  npm install -g nodemon
  ```

- Запуск скрипта с автоматической перезагрузкой:
  ```bash
  nodemon app.js
  ```

- Удаление пакета:
  ```bash
  npm uninstall axios
  ```

---

## Асинхронное программирование
### Callbacks (Обратные вызовы)
```javascript
const fs = require('fs');

fs.readFile('hello.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});
```

### Promises (Промисы)
```javascript
const fs = require('fs').promises;

fs.readFile('hello.txt', 'utf8')
   .then(data => console.log(data))
   .catch(err => console.error(err));
```

### Async/Await
```javascript
const fs = require('fs').promises;

(async () => {
    try {
        const data = await fs.readFile('hello.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
})();
```

---

## Создание REST API
Пример с использованием фреймворка Express:
1. Установите Express:
   ```bash
   npm install express
   ```

2. Создайте сервер:
   ```javascript
   const express = require('express');
   const app = express();

   app.get('/', (req, res) => {
       res.send('Hello, REST API!');
   });

   app.listen(3000, () => {
       console.log('Сервер работает на http://localhost:3000');
   });
   ```

---

## Полезные советы
1. Используйте **ESLint** для проверки кода.
2. Для разработки используйте **dotenv** для управления переменными окружения.
3. Регулярно обновляйте зависимости: `npm outdated` и `npm update`.
4. Для тестирования используйте фреймворки, такие как Mocha или Jest.

---

## Заключение
Node.js — это мощный инструмент для создания современных веб-приложений. Используя его, вы сможете разрабатывать серверную часть, обрабатывать запросы, создавать API и интеграции, а также масштабировать свои приложения.

Удачи в изучении!

## Полезные пакеты для Node.js

Node.js предлагает множество пакетов, которые могут упростить разработку. Вот список популярных и полезных библиотек:

### Общие утилиты
1. **lodash**: Набор утилит для работы с массивами, объектами, строками и другими типами данных.
   ```bash
   npm install lodash
   ```
   Пример использования:
   ```javascript
   const _ = require('lodash');
   const array = [1, 2, 3, 4];
   console.log(_.reverse(array)); // [4, 3, 2, 1]
   ```

2. **moment** / **dayjs**: Для работы с датами.
   ```bash
   npm install dayjs
   ```
   Пример использования:
   ```javascript
   const dayjs = require('dayjs');
   console.log(dayjs().format('YYYY-MM-DD'));
   ```

3. **dotenv**: Для работы с переменными окружения.
   ```bash
   npm install dotenv
   ```
   Пример использования:
   ```javascript
   require('dotenv').config();
   console.log(process.env.MY_VARIABLE);
   ```

### Для работы с API
1. **axios**: Лёгкая HTTP-библиотека.
   ```bash
   npm install axios
   ```
   Пример использования:
   ```javascript
   const axios = require('axios');
   axios.get('https://api.example.com/data')
       .then(response => console.log(response.data))
       .catch(error => console.error(error));
   ```

2. **express**: Один из самых популярных фреймворков для создания веб-серверов.
   ```bash
   npm install express
   ```
   Пример использования:
   ```javascript
   const express = require('express');
   const app = express();

   app.get('/', (req, res) => res.send('Hello World!'));
   app.listen(3000, () => console.log('Server running on port 3000'));
   ```

### Для работы с базами данных
1. **mongoose**: Работа с MongoDB.
   ```bash
   npm install mongoose
   ```
   Пример использования:
   ```javascript
   const mongoose = require('mongoose');
   mongoose.connect('mongodb://localhost/test', { useNewUrlParser: true, useUnifiedTopology: true });

   const schema = new mongoose.Schema({ name: String });
   const Model = mongoose.model('Model', schema);

   const doc = new Model({ name: 'Test' });
   doc.save().then(() => console.log('Document saved'));
   ```

2. **sequelize**: ORM для работы с SQL-базами данных.
   ```bash
   npm install sequelize
   ```
   Пример использования:
   ```javascript
   const { Sequelize, DataTypes } = require('sequelize');
   const sequelize = new Sequelize('sqlite::memory:');

   const User = sequelize.define('User', {
       username: DataTypes.STRING,
   });

   sequelize.sync().then(() => User.create({ username: 'John' }));
   ```

### Тестирование
1. **jest**: Фреймворк для тестирования.
   ```bash
   npm install jest
   ```
   Пример теста:
   ```javascript
   test('adds 1 + 2 to equal 3', () => {
       expect(1 + 2).toBe(3);
   });
   ```

2. **mocha** и **chai**: Для написания тестов и утверждений.
   ```bash
   npm install mocha chai
   ```

### Разные утилиты
1. **chalk**: Добавляет цветной вывод в консоль.
   ```bash
   npm install chalk
   ```
   Пример использования:
   ```javascript
   const chalk = require('chalk');
   console.log(chalk.green('Success!'));
   ```

2. **nodemon**: Автоматически перезапускает сервер при изменении файлов.
   ```bash
   npm install --save-dev nodemon
   ```

### Работа с WebSocket
1. **socket.io**: Библиотека для WebSocket.
   ```bash
   npm install socket.io
   ```
   Пример использования:
   ```javascript
   const io = require('socket.io')(3000);
   io.on('connection', socket => {
       console.log('A user connected');
   });
   ```

## Ресурсы для изучения
1. Официальная документация: [https://nodejs.org](https://nodejs.org)
2. Учебники и курсы на [freeCodeCamp](https://www.freecodecamp.org/)
3. Онлайн-платформы: [Udemy](https://www.udemy.com/) и [Coursera](https://www.coursera.org/).

