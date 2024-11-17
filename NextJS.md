
# Next.js Методичка

## Что такое Next.js?

**Next.js** — это популярный фреймворк для React, который позволяет создавать серверно-рендеринг (SSR) и статически сгенерированные (SSG) приложения. Он предоставляет множество встроенных возможностей для ускорения разработки, улучшения производительности и SEO.

---

## Установка и настройка

1. **Создание нового проекта:**
   ```bash
   npx create-next-app@latest my-next-app
   cd my-next-app
   npm run dev
   ```
   Это создаёт структуру проекта и запускает локальный сервер разработки по адресу `http://localhost:3000`.

2. **Основные команды:**
   - `npm run dev` — Запуск сервера разработки.
   - `npm run build` — Сборка приложения для продакшена.
   - `npm start` — Запуск собранного приложения.

---

## Основные концепции Next.js

### 1. **Файловая маршрутизация**

Каждый файл в папке `pages/` автоматически становится маршрутом:
- `pages/index.js` → `/`
- `pages/about.js` → `/about`

#### Динамические маршруты:
Создайте файл с именем в квадратных скобках, например:
- `pages/post/[id].js` → `/post/:id`

```jsx
import { useRouter } from 'next/router';

const Post = () => {
  const router = useRouter();
  const { id } = router.query;

  return <p>Post ID: {id}</p>;
};

export default Post;
```

---

### 2. **Серверный рендеринг (SSR)**

Используйте функцию `getServerSideProps` для получения данных на сервере:
```jsx
export async function getServerSideProps(context) {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data }, // Передаём данные в компонент
  };
}

const Page = ({ data }) => <div>{JSON.stringify(data)}</div>;

export default Page;
```

---

### 3. **Статическая генерация (SSG)**

Используйте `getStaticProps` для генерации страниц на этапе сборки:
```jsx
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
  };
}

const Page = ({ data }) => <div>{JSON.stringify(data)}</div>;

export default Page;
```

#### Генерация динамических маршрутов:
```jsx
export async function getStaticPaths() {
  const res = await fetch('https://api.example.com/items');
  const items = await res.json();

  const paths = items.map((item) => ({
    params: { id: item.id.toString() },
  }));

  return { paths, fallback: false };
}

export async function getStaticProps({ params }) {
  const res = await fetch(`https://api.example.com/item/${params.id}`);
  const data = await res.json();

  return {
    props: { data },
  };
}
```

---

### 4. **API Routes**

Создавайте API прямо в Next.js:
- `pages/api/hello.js`:
```jsx
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello, API!' });
}
```

Обращайтесь к API через `/api/hello`.

---

### 5. **Оптимизация изображений**

Используйте компонент `next/image` для оптимизации изображений:
```jsx
import Image from 'next/image';

const MyImage = () => (
  <Image src="/me.jpg" alt="Me" width={500} height={500} />
);

export default MyImage;
```

---

### 6. **CSS и стилизация**

- **CSS Modules**:
  Импортируйте CSS как модули:
  ```jsx
  import styles from './MyComponent.module.css';

  const MyComponent = () => <div className={styles.container}>Hello</div>;
  ```

- **Global CSS**:
  Подключите глобальные стили в `pages/_app.js`:
  ```jsx
  import '../styles/globals.css';

  export default function App({ Component, pageProps }) {
    return <Component {...pageProps} />;
  }
  ```

---

## Полезные встроенные функции

### 1. **Middleware**
Позволяет выполнять код перед рендерингом страницы. Создайте файл `_middleware.js`:
```jsx
export function middleware(req, ev) {
  // Логика middleware
}
```

### 2. **Redirects и Rewrites**
Настраивайте редиректы в `next.config.js`:
```javascript
module.exports = {
  async redirects() {
    return [
      {
        source: '/old-route',
        destination: '/new-route',
        permanent: true,
      },
    ];
  },
};
```

---

## Деплой

Next.js приложения легко развернуть на Vercel:
1. Перейдите на [vercel.com](https://vercel.com).
2. Подключите ваш репозиторий.
3. Нажмите «Deploy».

---

## Заключение

Next.js значительно упрощает разработку современных приложений, предоставляя инструменты для оптимизации производительности, SEO и удобного управления маршрутизацией. Начните использовать Next.js уже сегодня, чтобы ускорить процесс создания веб-приложений.

## Полезные функции Next.js

### 1. `getStaticProps` и `getServerSideProps`
- **`getStaticProps`** используется для получения данных во время сборки (SSG).
- **`getServerSideProps`** вызывается на сервере при каждом запросе (SSR).

Пример использования `getStaticProps`:
```javascript
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
  };
}
```

Пример использования `getServerSideProps`:
```javascript
export async function getServerSideProps(context) {
  const res = await fetch(`https://api.example.com/data?id=${context.query.id}`);
  const data = await res.json();

  return {
    props: { data },
  };
}
```

### 2. API-роуты
Next.js поддерживает создание серверных API в папке `pages/api`.

Пример простого API-эндпоинта:
```javascript
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello, API!' });
}
```

## Оптимизация производительности

1. **Кэширование данных**
   - Используйте `Incremental Static Regeneration (ISR)` для обновления данных на ходу без полного пересборки сайта.
   ```javascript
   export async function getStaticProps() {
     const res = await fetch('https://api.example.com/data');
     const data = await res.json();

     return {
       props: { data },
       revalidate: 10, // Данные обновляются каждые 10 секунд
     };
   }
   ```

2. **Оптимизация изображений**
   - Используйте компонент `next/image` для автоматической оптимизации изображений.
   ```javascript
   import Image from 'next/image';

   export default function Page() {
     return <Image src="/example.jpg" alt="Example" width={500} height={500} />;
   }
   ```

## Интеграция с внешними библиотеками

1. **Tailwind CSS**
   - Установите Tailwind CSS для стилизации компонентов:
   ```bash
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init
   ```
   - Настройте `tailwind.config.js` и импортируйте стили в `pages/_app.js`.

2. **Redux Toolkit**
   - Добавьте глобальное состояние с помощью Redux Toolkit:
   ```bash
   npm install @reduxjs/toolkit react-redux
   ```
   - Настройте store и подключите провайдер в `_app.js`.

## Лучшие практики

1. **Используйте TypeScript** для повышения надежности кода.
   ```bash
   npx typescript --init
   ```

2. **Делите код на модули** для улучшения читаемости.

3. **Следите за размером бандла** через анализатор:
   ```bash
   npm run analyze
   ```

4. **Используйте динамические импорты** для уменьшения времени загрузки страниц.
   ```javascript
   import dynamic from 'next/dynamic';

   const DynamicComponent = dynamic(() => import('../components/HeavyComponent'));
   ```

---

## Полезные ссылки
- [Официальная документация](https://nextjs.org/docs)
- [Примеры проектов на GitHub](https://github.com/vercel/next.js/tree/canary/examples)
- [Сообщество Next.js](https://vercel.com/solutions/nextjs)
