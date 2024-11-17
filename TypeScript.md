
# Руководство по TypeScript

TypeScript — это язык программирования, который расширяет возможности JavaScript за счёт добавления строгой типизации. TypeScript компилируется в JavaScript, который понимается всеми браузерами.

## Основные особенности TypeScript

1. **Типизация**:
   - Позволяет определить типы переменных, параметров функций и возвращаемых значений.
   - Делает код более предсказуемым и удобным для сопровождения.

2. **Интерфейсы и Типы**:
   - Помогают определить структуру объектов.

3. **Классы и Наследование**:
   - Расширяют возможности ООП (Объектно-Ориентированного Программирования).

4. **Модули**:
   - Позволяют организовывать код в отдельные файлы и пространства имён.

5. **Декораторы**:
   - Позволяют изменять поведение классов и методов.

6. **Универсальные шаблоны (Generics)**:
   - Позволяют работать с обобщёнными типами.

---

## Установка TypeScript

Для начала работы с TypeScript необходимо установить Node.js и TypeScript:

```bash
npm install -g typescript
```

Проверьте версию:
```bash
tsc --version
```

---

## Базовый синтаксис

### Типы переменных
```typescript
let isDone: boolean = false;
let age: number = 25;
let username: string = "Alice";
let hobbies: string[] = ["reading", "gaming"];
let tupleExample: [number, string] = [1, "example"];
```

### Интерфейсы
```typescript
interface User {
    id: number;
    name: string;
    isActive: boolean;
}

const user: User = {
    id: 1,
    name: "John Doe",
    isActive: true,
};
```

### Классы
```typescript
class Person {
    private name: string;
    public age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hello, my name is ${this.name}`;
    }
}

const person = new Person("Alice", 30);
console.log(person.greet());
```

### Модули
**Файл math.ts**
```typescript
export function add(a: number, b: number): number {
    return a + b;
}
```

**Файл app.ts**
```typescript
import { add } from "./math";

console.log(add(5, 10));
```

### Декораторы
```typescript
function Log(target: any, propertyName: string | Symbol) {
    console.log("Property decorator called");
}

class Test {
    @Log
    title: string;

    constructor(title: string) {
        this.title = title;
    }
}
```

### Generics
```typescript
function identity<T>(arg: T): T {
    return arg;
}

console.log(identity<number>(10));
console.log(identity<string>("Hello"));
```

---

## Работа с компилятором

### Конфигурация TypeScript
Создайте файл `tsconfig.json` для настройки компилятора:
```json
{
    "compilerOptions": {
        "target": "ES6",
        "module": "commonjs",
        "strict": true,
        "outDir": "./dist"
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules"]
}
```

Запустите компиляцию:
```bash
tsc
```

---

## Типы и их особенности

- `any` — любой тип (используйте с осторожностью).
- `unknown` — тип, который требует проверки перед использованием.
- `void` — отсутствие значения (например, у функций, которые ничего не возвращают).
- `never` — функция никогда не завершится (например, если выбрасывает ошибку).

### Примеры
```typescript
let anything: any = "hello";
let notSure: unknown = 4;
if (typeof notSure === "number") {
    console.log(notSure + 1);
}

function logMessage(message: string): void {
    console.log(message);
}

function throwError(message: string): never {
    throw new Error(message);
}
```

---

## Полезные утилиты TypeScript

- `Partial<T>` — делает все свойства опциональными.
- `Readonly<T>` — делает все свойства только для чтения.
- `Pick<T, K>` — выбирает определённые свойства.
- `Record<K, T>` — создаёт объект с указанными ключами и типами значений.

```typescript
interface Task {
    title: string;
    description: string;
}

const task: Partial<Task> = {};
task.title = "Learn TypeScript";
```

---

## Лучшая практика

1. Используйте `strict` режим в `tsconfig.json`.
2. Предпочитайте конкретные типы вместо `any`.
3. Старайтесь использовать интерфейсы и типы для описания данных.
4. Пишите модульный код, разделяя файлы по функциональности.

---

Для подробной документации посетите: [TypeScript Docs](https://www.typescriptlang.org/docs/).

## Почему стоит использовать TypeScript?
TypeScript помогает избежать многих ошибок, которые могут возникнуть в JavaScript, благодаря строгой типизации. Основные преимущества использования TypeScript:
- Улучшенная читаемость и сопровождение кода.
- Более раннее обнаружение ошибок на этапе компиляции.
- Улучшение автодополнения и документации в IDE.

## Установка TypeScript
TypeScript устанавливается через npm:
```bash
npm install -g typescript
```

Проверьте установку:
```bash
tsc --version
```

## Основы использования TypeScript

### Типы данных
TypeScript поддерживает базовые типы:
- `number`
- `string`
- `boolean`
- `null` и `undefined`
- `any` — для произвольных типов (не рекомендуется использовать без необходимости).
- `unknown` — более безопасная альтернатива `any`.
- `void` — для функций, которые ничего не возвращают.

Пример:
```typescript
let isDone: boolean = true;
let decimal: number = 6;
let color: string = "blue";
```

### Интерфейсы
Интерфейсы определяют структуру объектов:
```typescript
interface User {
    name: string;
    age: number;
    isAdmin: boolean;
}

let user: User = {
    name: "Alice",
    age: 25,
    isAdmin: false,
};
```

### Типы и объединения
TypeScript позволяет задавать сложные типы:
```typescript
type ID = string | number;

let userId: ID = 123;
userId = "ABC";
```

### Классы и наследование
TypeScript поддерживает классы и объектно-ориентированное программирование:
```typescript
class Animal {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    makeSound(): void {
        console.log("Some generic sound");
    }
}

class Dog extends Animal {
    makeSound(): void {
        console.log("Woof!");
    }
}

const dog = new Dog("Buddy");
dog.makeSound(); // Woof!
```

## Лучшие практики работы с TypeScript
1. Используйте строгий режим компилятора (`--strict`) для обеспечения более высокого качества кода.
2. По возможности избегайте использования типа `any`.
3. Разделяйте интерфейсы и классы в разные файлы для улучшения читаемости.
4. Используйте `Readonly` для неизменяемых объектов:
   ```typescript
   interface Point {
       readonly x: number;
       readonly y: number;
   }

   let p1: Point = { x: 10, y: 20 };
   // p1.x = 5; // Ошибка!
   ```

5. Объявляйте переменные и параметры функций с явным указанием типа.

## Ресурсы для изучения
1. [Официальная документация TypeScript](https://www.typescriptlang.org/docs/)
2. [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
3. [Playground TypeScript](https://www.typescriptlang.org/play)
