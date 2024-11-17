
# Методичка по JSDoc

JSDoc — это инструмент для документирования кода JavaScript, который позволяет создавать аннотации для функций, переменных, классов и других элементов кода. Аннотации помогают улучшить читаемость кода и автоматизировать генерацию документации.

## Основы JSDoc

JSDoc-аннотации записываются в многострочных комментариях. Они начинаются с `/**` и заканчиваются на `*/`. Внутри используются теги, которые описывают различные аспекты кода.

### Пример базового использования
```javascript
/**
 * Приветствует пользователя.
 * @param {string} name - Имя пользователя.
 * @returns {string} Приветственное сообщение.
 */
function greet(name) {
    return `Привет, ${name}!`;
}
```

## Основные теги JSDoc

### @param
Используется для описания параметров функции.
- **Синтаксис:** `@param {Тип} имя - описание`
- **Пример:**
```javascript
/**
 * Вычисляет сумму двух чисел.
 * @param {number} a - Первое число.
 * @param {number} b - Второе число.
 * @returns {number} Сумма чисел.
 */
function sum(a, b) {
    return a + b;
}
```

### @returns
Описывает возвращаемое значение функции.
- **Синтаксис:** `@returns {Тип} описание`
- **Пример:**
```javascript
/**
 * Умножает два числа.
 * @param {number} x - Первый множитель.
 * @param {number} y - Второй множитель.
 * @returns {number} Произведение.
 */
function multiply(x, y) {
    return x * y;
}
```

### @type
Используется для описания типа переменной или объекта.
- **Пример:**
```javascript
/** @type {string} */
let username = "John Doe";
```

### @typedef
Создаёт пользовательский тип.
- **Пример:**
```javascript
/**
 * @typedef {Object} User
 * @property {string} name - Имя пользователя.
 * @property {number} age - Возраст пользователя.
 */

/** @type {User} */
const user = { name: "Alice", age: 25 };
```

### @property
Используется для описания свойств объекта.
- **Пример:**
```javascript
/**
 * @typedef {Object} Car
 * @property {string} make - Марка автомобиля.
 * @property {string} model - Модель автомобиля.
 * @property {number} year - Год выпуска.
 */
```

### @example
Добавляет пример использования.
- **Пример:**
```javascript
/**
 * Считает количество символов в строке.
 * @param {string} str - Входная строка.
 * @returns {number} Количество символов.
 * @example
 * // Пример использования:
 * const length = getStringLength("hello");
 * console.log(length); // 5
 */
function getStringLength(str) {
    return str.length;
}
```

### @deprecated
Помечает функцию или метод как устаревший.
- **Пример:**
```javascript
/**
 * @deprecated Используйте newMethod вместо этого.
 */
function oldMethod() {
    console.log("Этот метод устарел.");
}
```

### @async
Помечает функцию как асинхронную.
- **Пример:**
```javascript
/**
 * Загружает данные асинхронно.
 * @async
 * @returns {Promise<string>} Данные.
 */
async function fetchData() {
    return "Данные загружены.";
}
```

## Дополнительные фичи JSDoc

1. **Поддержка модулей:** Вы можете использовать JSDoc для описания модулей с помощью `@module`.
   ```javascript
   /**
    * Модуль для работы с пользователями.
    * @module UserModule
    */
   export function createUser(name) {
       return { name };
   }
   ```

2. **Встраивание ссылок:** Внутри описаний можно использовать HTML или Markdown.
   ```javascript
   /**
    * Пример использования функции можно найти [здесь](https://example.com).
    */
   ```

3. **Опциональные параметры:** Описываются с использованием квадратных скобок.
   ```javascript
   /**
    * Приветствует пользователя.
    * @param {string} [name] - Имя пользователя (опционально).
    * @returns {string} Приветственное сообщение.
    */
   function greet(name = "Гость") {
       return `Привет, ${name}!`;
   }
   ```

4. **Массивы и объекты:** Для типов можно использовать `Array<Type>` или `Object<Key, Value>`.
   ```javascript
   /**
    * @param {Array<number>} numbers - Список чисел.
    * @returns {number} Сумма чисел.
    */
   function sumArray(numbers) {
       return numbers.reduce((acc, num) => acc + num, 0);
   }
   ```

## Генерация документации
После написания аннотаций, сгенерировать документацию можно с помощью:
1. Установки JSDoc: `npm install -g jsdoc`.
2. Запуска команды: `jsdoc имя_файла.js`.

Документация будет создана в HTML-формате и доступна в указанной директории.

## Полезные ссылки
- [Официальная документация JSDoc](https://jsdoc.app/)
- [Примеры использования](https://jsdoc.app/tags-param.html)



## Расширенные возможности JSDoc

### Аннотация пользовательских типов с @typedef
`@typedef` позволяет создавать собственные типы данных для лучшей читаемости и структурированности кода.
```javascript
/**
 * @typedef {Object} User
 * @property {number} id - Уникальный идентификатор пользователя.
 * @property {string} name - Имя пользователя.
 * @property {boolean} isActive - Активен ли пользователь.
 */

/**
 * Получает информацию о пользователе.
 * @returns {User} Объект пользователя.
 */
function getUser() {
    return { id: 1, name: "Иван", isActive: true };
}
```

### Описание функций обратного вызова с @callback
Используйте `@callback` для документирования callback-функций.
```javascript
/**
 * @callback Comparator
 * @param {number} a - Первое число.
 * @param {number} b - Второе число.
 * @returns {number} Разница между числами.
 */

/**
 * Сортирует массив чисел.
 * @param {number[]} array - Массив чисел для сортировки.
 * @param {Comparator} compare - Функция для сравнения чисел.
 * @returns {number[]} Отсортированный массив.
 */
function sortArray(array, compare) {
    return array.sort(compare);
}
```

### Использование шаблонов типов с @template
`@template` полезен для описания обобщенных типов (generic).
```javascript
/**
 * Создает массив с элементами заданного типа.
 * @template T
 * @param {T} value - Значение, которое будет добавлено в массив.
 * @param {number} count - Количество элементов в массиве.
 * @returns {T[]} Массив с элементами типа T.
 */
function createArray(value, count) {
    return Array(count).fill(value);
}
```

## Поддержка TypeScript
JSDoc активно используется для типизации в TypeScript. Например:
```javascript
/**
 * @param {string} message - Сообщение для отображения.
 * @param {number} [timeout=3000] - Время отображения в миллисекундах.
 */
function showMessage(message, timeout = 3000) {
    console.log(message);
    setTimeout(() => console.log('Скрытие сообщения'), timeout);
}
```
Используйте `ts-check` для включения проверки типов в JavaScript-файлах:
```javascript
// @ts-check
```

## Лучшие практики написания JSDoc
1. **Консистентность**: Используйте одинаковый стиль для всех аннотаций в проекте.
2. **Краткость**: Описания должны быть понятными, но не излишне длинными.
3. **Актуальность**: Регулярно обновляйте документацию при изменении кода.

## Автоматизация с помощью JSDoc
Для генерации документации:
1. Установите JSDoc: `npm install -g jsdoc`.
2. Сгенерируйте HTML-документацию: `jsdoc файл.js -d docs`.

Вы можете интегрировать JSDoc в CI/CD пайплайн, чтобы автоматически обновлять документацию при каждом обновлении кода.

## Примеры сложных сценариев

### Документирование асинхронных функций
```javascript
/**
 * Получает данные из API.
 * @async
 * @param {string} url - URL для запроса.
 * @returns {Promise<Object>} Данные ответа API.
 */
async function fetchData(url) {
    const response = await fetch(url);
    return response.json();
}
```

### Документация модулей
```javascript
/**
 * Модуль для работы с пользователями.
 * @module userModule
 */

/**
 * Добавляет нового пользователя.
 * @param {Object} user - Объект пользователя.
 * @param {string} user.name - Имя пользователя.
 * @param {string} user.email - Email пользователя.
 */
export function addUser(user) {
    // ...
}
```

