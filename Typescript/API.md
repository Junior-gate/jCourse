```ts
export interface DefaultPaginationParams {
  limit?: number
  offset?: number // or "skip"
}

export interface AxiosPaginatedResponse<T = any> {
  count: number
  next: T | null
  previous: T | null
  results: T[]
}
```