# Routing

### Intro

В отличие от `react`, где для роутинга мы используем дополнительные библиотеки вроде `react-router`, в `next.js` роутинг идет из коробки и строится на основе структуры файлов корневой папки `pages` (не путать с src/pages)

```
public/
pages/ - тут находится роутинг страниц
src/
```
### Static routes

Статичные пути создаются по названию файла:
```js
pages/
    about.tsx // "/about"
    info.tsx // "/info"
    index.tsx // "/"
```

### Nested routes

Чтобы создать вложенные роуты, нужно создавать дополнительные папки:
```js
pages/
    user/
        settings.tsx // "/user/settings"
        profile // "/user/profile"
    info.tsx // "/info"
    about/
        news/ // "/about/news"
        index.tsx // "/about" - обратите внимание на этот случай
    categories/
        zoo/
            products/
                news.tsx // "/categories/zoo/products/news"
    index.tsx // "/"
```
### Dynamic routes

Для создания динамических роутов нужно создать файл/папку с `[]`:

> Динамические роуты могут быть как строкой, так и числом

```js
pages/
    products/
        [id].tsx // "/products/1"
    sellers/[category]/[id].tsx // "/sellers/zoo/4 "
```

> Название внутри `[]` имеет значение, по нему можно получить значение в `useRouter`, 
> об этом ниже

### Сaveats 

Иногда нам нужны маршруты любого пути, тогда можно использовать `[...name]` синтаксис:
```js
pages/
    about/
        [...slug].tsx // "/about/any/some/path"
```
> в router.query.slug это будет массив - `['any','some', 'path']`

### 404

Чтобы сделать кастомную страницу 404, используем `404.tsx` в корне:
```
pages/
    404.tsx
```

### Error page
```js
// TODO
```

### Getting queries

Чтобы получить значения маршрута на странице, нужно использовать `useRouter`:

```jsx
// blogs/[id].tsx
import { useRouter } from 'next/router'

const Demo = () => {
    const { query } = useRouter()  
   <div>{`you are on ${query.id} page`}</div> 
   // для /blogs/5 , query.id = 5 etc.
    ...
}
```

### Практика

В папке статьи есть пример папки `pages/`, в каждой папке пример URL.