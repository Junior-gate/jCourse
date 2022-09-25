# Немного основ Typescript

## Число
```ts
let test: number = 7;
```

## Строка
```ts
let test: string = 'hi';
```

### Перечисления
```ts
let test: 'hi' | 'hello' = 'hi';
```
> иногда для таких ситуаций также подходит enum

### Сложная строка
```ts
let width: `${number}px` = '7px';
let name: `${string} ${string}` = 'Иван Павлов';

```

## Boolean
```ts
let test: boolean = true;
// это может понадобится когда мы отрабатываем разные случаи для true/false:
let test: true = true; 
```

## React элемент
```ts
const Test: ReactNode = 'hi';
const Test: ReactNode = null;
const Test: ReactNode = <div>Hi</div>;
```
> подробнее о типизации компонентов в отдельной главе


## Массив

### Синтаксис
```ts
const test: number[] = [2, 4];
// вместо number может быть любой тип, массив, объект и тд
```

### ```Array<T> VS T[]```

Обе записи возможны, но string[] всегда предпочтительнее:

```ts
// ❌ Wrong:
const test: Array<string> = ['one', 'two']; 

// ✅ Correct:
const test: string[] = ['one', 'two']; 
// Но:
const test: Array<string | number> = ['one', 2]; 
```

### Массив массива

```ts
const test: number[][] = [[2, 4], [2, 4]];
// вместо number может быть любой тип, массив, объект и тд
```

### Tuple 

Когда вы знаете точное число элементов массива, лучше использовать tuple. Такое нужно часто при работе с массивами типа "ключ, значение":

```ts
const test: [string, number] = ['age', 4]; 
```
> такая запись не допустит дополнительных элементов и точнее чем Array<string | number> (Почему?)

## Object

### синтаксис

Обе записи аналогичны, подробнее в отдельной статье:

```ts
// Interface:
interface User {
    name: string;
    age: number;
    friends: User[];
}
const test: User = {...};
// Type:
type User = {
    name: string;
    age: number;
    friends: User[];
}
const test: User = {...};

```

### Любые ключи

```ts
type AdditionalData = {
    [key: string]: any
}
```

## Неизвестный тип

Иногда тип еще точно не известен(например при миграции с js на ts), для этого есть any, unknown:
```ts
const test: any = {name: 'Joe'}
const test2: unknown = {name: 'Joe'}

console.log(test.name) // OK! 

// unknown в отличие от any будет предупреждать о возможных ошибках:
console.log(test2.name) // Error! name может не существовать в неизвестном типе test2

```

### Немного об объектах

```ts
// ❌ Wrong:
const user: object = {name: 'Joe'}

// ❌ Wrong:
const user: {name: string} = {name: 'Joe'}

// ✅ Correct:
interface User {name: string};
const user: User = {name: 'Joe'};
// такая запись позволит повторно использовать тип и легче читается
```

## Функции
```ts
// ❌ Wrong:
const isEmail: Function = (str) => {...}
```

### function declaration
```ts
function isEmail (str: string): boolean {...}
```

### function expression
```ts
const isEmail = (str: string): boolean => {...}
```
or:
```ts
// например, так типизируются компоненты:
type Validator = (str: string) => boolean
const isEmail: Validator = (str) => {...}
```
### function in object
```ts
interface ButtonProps {
    name: string
    // func types example
    onClick: (id: number) => void
    onChange: () => void // no args
    validate: () => boolean 
}
```

## Enum

Это более широкая тема

