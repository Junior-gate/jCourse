# Request

Немного советов по созданию запросов

- Использовать "async , await" вместо "then"
- Выполнять запрос в useEffect, либо в thunk, saga 
- Отдельно создавать функцию для API запроса
- Использовать try-catch для обработки ошибок
- Обрабатывать loading когда это необходимо

## UseEffect example
```jsx
  useEffect(() => {
    const loadProducer = async (id: number) => {
      try {
        const { producer } = await getProducerById(id)
        dispatch(setProducer(producer))
      } catch (error) {
         dispatch(setError(error))
      }
    }
    loadProducer(id)
  }, [dispatch, id])

```

## thunk example
```ts

export const getProductsThunk = createAsyncThunk<Product[], GetProductsPayload>(
  'products/getProductThunk',
  async (payload) => {
    const { limit, skip } = payload;
    const response = await getProducts({ limit, skip });
    if (response.status === 200 && response.data.results.length) {
      const products: Product[] = response.data.results;
      return products;
    }
    return [];
  }
);

```

## saga example
```
```
## RTK example
```
```