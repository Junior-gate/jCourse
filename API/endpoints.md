# Endpoints

Очень удобно создать объект endpoints для API и использовать нужные пути в нужных запросахЖ

```ts
// api/endpoints.ts
export const endpoints = {
  products: {
    list: '/products/',
    product: (id: number) => `/products/${id}/`,
    add: `/products/create`,
  },
  user: {
    profile: '/user/me',
    order: (id: number) => `/user/orders/${id}/`,
  },
}

// Usage

// api/product.ts
export const getProductById = (id: number): AxiosPromise<Product> => {
  return api.get(endpoints.products.product(id))
}
```