
# Руководство по Nuxt JS

## 1. Введение в Nuxt JS
**Nuxt.js** — это высокоуровневый фреймворк для разработки приложений на основе Vue.js. Он предоставляет инструменты для серверного рендеринга (SSR), статической генерации сайтов (SSG) и создания одностраничных приложений (SPA). Основные преимущества Nuxt.js:
- Лёгкость настройки и использования.
- Автоматическая маршрутизация и серверный рендеринг.
- Поддержка SEO и мета-тегов из коробки.
- Встроенная поддержка TypeScript.

## 2. Установка и настройка проекта

Для начала нужно установить **Nuxt.js**. Выполним следующие команды:

```bash
npx nuxi init my-nuxt-app
cd my-nuxt-app
npm install
npm run dev
```

Эта команда создаст новый проект и запустит его в режиме разработки на `http://localhost:3000`.

## 3. Структура проекта

Основные директории и файлы:
- **pages/** — содержит страницы приложения, маршруты создаются автоматически.
- **components/** — компоненты для повторного использования.
- **layouts/** — шаблоны макетов для страниц.
- **plugins/** — подключение сторонних библиотек и плагинов.
- **store/** — управление состоянием (Vuex Store).
- **nuxt.config.ts** — настройки проекта.

## 4. Работа с маршрутизацией

Nuxt автоматически создаёт маршруты на основе файлов в папке `pages/`. Например, файл `pages/about.vue` будет доступен по адресу `/about`.

```vue
<template>
  <div>
    <h1>О нас</h1>
    <p>Эта страница рассказывает о нашей компании.</p>
  </div>
</template>
```

## 5. Компоненты и их реиспользование

Создадим компонент `Button.vue` в папке `components/`:

```vue
<template>
  <button class="btn">{{ text }}</button>
</template>

<script setup>
defineProps({
  text: String
});
</script>

<style scoped>
.btn {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
}
</style>
```

Используем его на странице:

```vue
<template>
  <Button text="Нажми меня" />
</template>
```

## 6. Состояние (Store) и управление данными

В Nuxt 3 используется Pinia вместо Vuex для работы с состоянием:

```bash
npm install @pinia/nuxt
```

Создадим файл `stores/counter.ts`:

```typescript
import { defineStore } from 'pinia';

export const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0
  }),
  actions: {
    increment() {
      this.count++;
    }
  }
});
```

Используем store в компоненте:

```vue
<script setup lang="ts">
import { useCounterStore } from '@/stores/counter';
const counter = useCounterStore();
</script>

<template>
  <div>
    <p>Счётчик: {{ counter.count }}</p>
    <button @click="counter.increment">Увеличить</button>
  </div>
</template>
```

## 7. Работа с API и Axios

Для выполнения запросов к API:

```bash
npm install @nuxtjs/axios
```

Добавим модуль в `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxtjs/axios'],
  axios: {
    baseURL: 'https://jsonplaceholder.typicode.com'
  }
});
```

Пример использования:

```vue
<script setup>
import { ref } from 'vue';

const posts = ref([]);
async function fetchPosts() {
  const { data } = await useFetch('/posts');
  posts.value = data.value;
}
fetchPosts();
</script>

<template>
  <div v-for="post in posts" :key="post.id">
    <h2>{{ post.title }}</h2>
    <p>{{ post.body }}</p>
  </div>
</template>
```

## 8. Полезные плагины и модули

- **@nuxtjs/tailwindcss** — для стилизации с использованием Tailwind CSS.
- **@pinia/nuxt** — для работы с состоянием.
- **@nuxtjs/axios** — для HTTP-запросов.

## 9. Стилизация с Tailwind CSS

```bash
npm install -D @nuxtjs/tailwindcss
```

Добавим в `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxtjs/tailwindcss']
});
```

Создадим файл `tailwind.config.js`:

```javascript
module.exports = {
  content: ['./components/**/*.{vue,js}', './pages/**/*.vue']
};
```

## 10. SEO и Meta-теги

Настроим мета-теги в `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  app: {
    head: {
      title: 'Мой Nuxt сайт',
      meta: [
        { name: 'description', content: 'Это описание моего сайта на Nuxt.js' }
      ]
    }
  }
});
```

## 11. Деплой проекта

Для деплоя на Vercel:

```bash
npm install -g vercel
vercel
```

Или на Netlify:

```bash
npm install -g netlify-cli
netlify deploy
```

## Заключение

Nuxt.js — мощный фреймворк, который позволяет быстро создавать современные веб-приложения. Его гибкость и мощные встроенные инструменты делают разработку удобной и продуктивной.
