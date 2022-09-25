# ENV

Чтобы не писать в каждом запросе к API  
```js
 'https://someLongBaseUrlName/product',
 'https://someLongBaseUrlName/categories'
 //...
```
Создается [instance](./instance.md), 

Также base URL часто создается в env переменных, вот как это делается:

```js
// .env
NOVE_ENV=development
REACT_APP_API_URL='https://someLongBaseUrlName'

// api/instance.ts
const BASE_URL = process.env.REACT_APP_API_URL
```