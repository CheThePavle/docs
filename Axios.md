
# Полная методичка по Axios

Axios — это популярная JavaScript-библиотека для выполнения HTTP-запросов. Она позволяет легко работать с API и поддерживает промисы, упрощая асинхронную работу. Ниже описаны основные фичи, установка и использование Axios.

---

## Установка

### Через npm
```bash
npm install axios
```

### Через CDN
Добавьте ссылку в ваш HTML-файл:
```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

---

## Основные функции Axios

1. **GET-запрос**
   Получение данных с сервера.
   ```javascript
   axios.get('https://api.example.com/data')
     .then(response => {
       console.log(response.data); // Данные из API
     })
     .catch(error => {
       console.error(error);
     });
   ```

2. **POST-запрос**
   Отправка данных на сервер.
   ```javascript
   axios.post('https://api.example.com/data', {
       name: 'John',
       age: 30
     })
     .then(response => {
       console.log(response.data);
     })
     .catch(error => {
       console.error(error);
     });
   ```

3. **PUT-запрос**
   Обновление данных.
   ```javascript
   axios.put('https://api.example.com/data/1', {
       name: 'Jane',
       age: 25
     })
     .then(response => {
       console.log(response.data);
     })
     .catch(error => {
       console.error(error);
     });
   ```

4. **DELETE-запрос**
   Удаление данных.
   ```javascript
   axios.delete('https://api.example.com/data/1')
     .then(response => {
       console.log(response.data);
     })
     .catch(error => {
       console.error(error);
     });
   ```

---

## Настройка запросов

### Заголовки
Добавьте заголовки для запроса.
```javascript
axios.get('https://api.example.com/data', {
  headers: {
    Authorization: 'Bearer token'
  }
})
.then(response => {
  console.log(response.data);
})
.catch(error => {
  console.error(error);
});
```

### Параметры запроса
Передача параметров через строку запроса.
```javascript
axios.get('https://api.example.com/data', {
  params: {
    userId: 123
  }
})
.then(response => {
  console.log(response.data);
})
.catch(error => {
  console.error(error);
});
```

---

## Axios Instance

Вы можете создать экземпляр Axios с заранее заданными настройками:
```javascript
const api = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 1000,
  headers: { 'Authorization': 'Bearer token' }
});

api.get('/data')
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
```

---

## Обработка ошибок

Axios предоставляет информацию об ошибке через объект `error`.
```javascript
axios.get('https://api.example.com/data')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    if (error.response) {
      console.error('Ошибка ответа:', error.response.data);
    } else if (error.request) {
      console.error('Ошибка запроса:', error.request);
    } else {
      console.error('Неизвестная ошибка:', error.message);
    }
  });
```

---

## Перехватчики (Interceptors)

Перехватчики позволяют обрабатывать запросы и ответы перед их выполнением.
```javascript
axios.interceptors.request.use(config => {
  console.log('Запрос отправлен:', config);
  return config;
}, error => {
  return Promise.reject(error);
});

axios.interceptors.response.use(response => {
  console.log('Ответ получен:', response);
  return response;
}, error => {
  return Promise.reject(error);
});
```

---

## Отмена запросов

Вы можете отменить запрос с помощью `CancelToken`.
```javascript
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('https://api.example.com/data', {
  cancelToken: source.token
})
.catch(error => {
  if (axios.isCancel(error)) {
    console.log('Запрос отменён:', error.message);
  } else {
    console.error(error);
  }
});

// Отмена запроса
source.cancel('Отмена запроса пользователем.');
```

---

## Работа с JSON и другими форматами данных

Axios автоматически преобразует JSON-данные.
```javascript
axios.post('https://api.example.com/data', {
  name: 'John'
})
.then(response => {
  console.log(response.data);
})
.catch(error => {
  console.error(error);
});
```

Если вам нужно передать данные в другом формате, используйте `transformRequest`:
```javascript
axios.post('https://api.example.com/data', 'param1=value1&param2=value2', {
  headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
  transformRequest: [(data) => {
    return data; // Здесь можно трансформировать данные
  }]
})
.then(response => console.log(response.data))
.catch(error => console.error(error));
```

---

## Советы по использованию Axios

1. **Повторное использование**: Создавайте `axios instance` для каждого API.
2. **Тестирование**: Используйте моки, такие как `axios-mock-adapter`, для тестирования.
3. **Обновления**: Регулярно проверяйте обновления библиотеки для новых возможностей и исправлений.

---

С этой методичкой вы сможете эффективно использовать Axios в своих проектах. Удачи в разработке!
