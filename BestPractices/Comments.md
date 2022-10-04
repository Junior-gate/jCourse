# Comments

Договоренности по написанию комментариев в проекте сильно вариируются в разных компаниях, ниже представлены наши собственные правила:

### Usage

Когда нужно использовать комментарии:

- Объяснить логику работы функции
- Оставить заметку о неисправленом недочете ([TODO](#todo))
- Проянить нюансы, из за которых выбрана та или иная реализация, которая может вызвать вопросы

> Вам нужно писать чистый, понятный код. Написание комментариев обычно исключение, чем правило. Не пишите их везде подряд, особенно когда всё и так очевидно

### English only

У нас, как и в большинстве компаний, комментарии составляются исключительно на английском языке:

```js
// ❌ Wrong:

// парсим дату в формате YYYY:MM
const parseDate = (date) => {...}

// ✅ Correct:

// parse date in format YYYY:MM
const parseDate = (date) => {...}
```

### TODO

Очень полезно оставлять `TODO` комментарии, чтобы оставить заметку о недочетах которые невозможно исправить в настоящий момент:

```ts
interface Shop {
  products: Product[];
  id: number;
  workingDates: any; // TODO fix types
}
```

### Examples

> Это TODO - то, что не получилось исправить на момент написания кода,
> но надо исправить в будущем:

```ts
function getProducts(): any { // TODO fix when API schema is ready
...}
```

> Это пояснение ошибки:

```ts
function doSomething() {
    ...
    // @ts-expect-error This parseFloat is probably unnecessary
    parseFloat(status)
    ...
}

```

> Это описание работы функции, назначение которой может быть неясно:

```ts
// The same as useEffect hook, but function is not called on mounting
export const useDidUpdate = (...) => {...}

```

> Это пояснение нюанса, неочевидного из кода:

```ts
/*
  To prevent circular dependency issue
   these selectors must not be arrow functions
   https://github.com/reactjs/reselect/issues/169
 * */

export function getCart(state: CartState) {...}
```
