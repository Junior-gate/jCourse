# Instance

Создание instance, это must have в работе с API. Вот пример инициализации instance в axios:

```js
import Axios from 'axios'
import shopAPI from './constants'
export * from './endpoints'


export const api = Axios.create({
  baseURL: shopAPI, // http://url
  headers: {
    'Content-Type': 'application/json',
  },
  withCredentials: true,
})
```

Использование:
```js
import api from './instance'

export const getCategories = (): AxiosPromise<Category[]> => {
  return api.get(endpoints.categories)
}

export const postRequest = (
  data: RequestQuotePost
): AxiosPromise<Response> => {
  return api.post(endpoints.request, data)
}
```