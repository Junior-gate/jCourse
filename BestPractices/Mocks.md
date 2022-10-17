# Mocks

### Что такое моки?

Моки, моковые данные — объекты, имитирующие реальные данные, которые используются вместо реальных данных (например, с API), когда использовать реальные данные нет возможности.

Другими словами, когда во время разработки мы не можем использовать реальные данные (не готово API, нужно имитировать данные которых нет в базе данных, заказчик не скинул контент для сайта и тд), мы прибегаем к фейковым данным, чтобы не тормозить процесс.

### Использование моков

Обычно моки хранятся в отдельной директории, например shared/mocks:

```js
// shared/mocks/products.ts

export const productsMock = [
    {id: 1, name: 'Chili'},
    {id: 2, name: 'Soup'}
]
```

Далее используем их там, где нужны реальные данные:

```js

import productsMock from './mocks'
// ...
// real API request is commented:
// const { data } = getProducts()
const data = productsMock;
data.map(...)
```

### Mocks VS Hard-code

Частой ошибкой является попытка "хардкодить вместо того", чтобы использовать моки.
В примере ниже, getUserProfile API еще не готов, в первом случае по готовности API придется вновь переписывать компонент:
```jsx

// ❌ Wrong:
const UserProfile = () => {
 return 
 <div>
    Name: <div>Ivan</div>
    Age: <div>35</div>
 </div>
}

// Usage:

<UserProfile />

// ✅ Correct:
const UserProfile = (props) => {
 return 
 <div>
    Name: <div>{props.name}</div>
    Age: <div>{proos.age}</div>
 </div>
}

// Usage:

// const user = useSelector(getUser)
const user = userMocks;
<UserProfile name={user.name} age={user.age} />


```

### Fetch mock

Можно создать функцию которая возвращает мок, чтобы затем заменить реальную функцию-запрос к API на моковую.

```ts
// helper
const fetch = (data) =>
  new Promise((resolve) => {
    setTimeout(() => resolve(data), 3000);
  });

// mocks
export const getProducts = fetch(productsMocks);

//usage

import getProducts from './mock'
// import getProducts from './api'

const { data } = await getProducts()
```