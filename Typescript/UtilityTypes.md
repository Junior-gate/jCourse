# Utility Types

## Intro

В typescript есть ряд типов, которые помогут решить популярные преобразования.

> Данные типы легко сделать самостоятельно, ведь они используют встроенные возможности typescript, такие как [Generic](../Typescript/Generic.md) и `Mapped Types`

## Base

Ниже представлены 4 самых популярных utility types:

### Partial

`Partial<Type>`

Делает все поля необязательными:

```ts
// ❌ Wrong:
type ContactForm = {
    name?: string,
    age?: number,
    date?: Date,
    comment?: string
}
// ✅ Correct:
type ContactForm = Partial<{
    name: string,
    age: number,
    date: Date,
    comment: string
}>
```


```ts
// Можно использовать Partial и для существующих типов:
interface Todo {
  title: string;
  description: string;
}
 
function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

```

### Required

`Required<Type>`

Тип с противоположным назначением:

```ts
interface Params {
    search: string,
    price?: number
}

type AllParams = Required<Params>;  
// =>
// {
//   search: string,
//   price: number
// }
```

### Record

`Record<Keys, Type>`

Как типизировать объект у которого могут быть любые поля:

```ts
// ❌ Wrong:
let anyObject: object;

// ✅ Correct:
let anyObject: Record<string, any>;

```

> Это также может быть полезно при создании хелперов или при работе с динамическими полями из API

### Omit 

`Omit<Type, Keys>`

Данный тип позволяет создать на основе одного интерфейса другой, без некоторых полей

```ts
interface User {
  id: number
  name: string;
  avatar: string;
  orders: Order[];
}

type UserShorten = Omit<User, 'orders'>; // интерфейс User без orders 
``` 
 
> Это бывает полезно когда, например, на странице пользователя/товара мы получаем все данные, 
> а на странице списков пользователей/товаров мы получаем лишь часть данных

## Advanced

Следующие utility types используются значительно реже:

### Pick

`Pick<Type, Keys>`

Противоположный Omit тип - создает тип с частью полей

```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}
 
type TodoPreview = Pick<Todo, "title" | "completed">; // интерфейс только с полями title, completed
```

### Exclude

`Exclude<UnionType, ExcludedMembers>`

Позволяет создать новый тип без некоторых значений

```ts
// Общие значения вариаций интерфейса, можно применить к button, input..
type Theme = 'primary' | 'secondary' | 'error' | 'disabled'

// Например, для компонентов, у которых нет error, disabled вариации:
type BadgeVariant = Exclude<Theme, 'error' | 'disabled'> //  'primary' | 'secondary'
```

> Выше показан пример лишь для демонстрации, обычно Exlude применяется в более сложных кейсах

### Capitalize

`Capitalize<StringType>`

Данный тип может быть полезен при работе с типами, у которых есть конкретные значения - union type (`'male' | 'female'`), [enum](Enum.md).

```ts
type Gender = 'male' | 'female'

function sendUserGender = (gender: Capitalize<Gender>) => {...} // MALE, FEMALE
```

> Есть также Uppercase, Lowercase, Uncapitalize типы, они могут быть полезны когда регистр имеет 
> значение - отображение значений на сайте, API которая принимает определенный регистр

## More

На данной странице представлены лишь часть подобных типов, полную информацию вы можете найти на [оффициальной странице документации]('https://www.typescriptlang.org/docs/handbook/utility-types.html')