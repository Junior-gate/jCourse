# Constants

Для поддержания чистоты и ясности кода лучше выделять постоянные, общие и неочевидные для остальных разработчиков величины. Обычно их записывают через UPPER_CASE и хранят в отдельном файле/папке

Рассмотрим 3 примера.

### Постоянные величины

Можно выносить постоянные значения в константы:

```jsx
// constants.ts
export const TABLET_SCREEN = 768
export const DAY_IN_MS = 24 * 60 * 60 * 1000

// component.tsx

// ❌ Wrong:
<div>Delivery: {delivery / 24 * 60 * 60 * 1000} days</div>

// ✅ Correct:
<div>Delivery: {delivery / DAY_IN_MS} days</div>
```

### Неочевидные величины

В читаемости кода ниже есть проблема - требуется время, чтобы понять, откуда взялась цифра 5:
```jsx
    fields.length < 5 &&
    <Button onClick={() => append({})}>Add address</Button>
```

Константы значительно улучшают читаемость и в дальнейшем при появлении аналогичных полей с адресами на других страницах можно настраивать лимит, изменив константу.  
```jsx
    fields.length < MAX_ADDRESSES_LIMIT &&
    <Button onClick={() => append({})}>Add address</Button>
```

### Общие значения

Игнорирование констант также может привести к ошибкам, которые не так легко исправить:

```jsx
// component.tsx

// ❌ Wrong:
<div>Commission: {service.commision || 15}</div>
```
При использовании hard-code значения 15 в разных частях проекта в итоге приведет к ошибке, когда размер комиссии изменится, лучше:

```jsx
// constants.ts
export const DEFAULT_COMMISSION = 15

// component.tsx
// ✅ Correct:
<div>Commission: {service.commision || DEFAULT_COMMISSION}</div>
```

### Дополнительно

 Также в константы можно выносить не только числа: например, дефолтное значение объекта формы, чтобы каждый раз его не прописывать, или строки, чтобы случайно не опечататься(для этого также подходит [enum](/Typescript/Enum.md)):

```ts
export const DEFAULT_TRAVELLER = {
    name: '',
    age: new Date,
    addresses: [],
    isAgent: false
}

export const SPECIAL_OFFER = 'special_offer';

export enum Sort {
    BY_PRICE: 'price',
    BY_NAME: 'name'
}
```