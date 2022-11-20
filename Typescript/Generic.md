# Generics

Дженерики в typescript позволяют использовать "параметры" в типах, создавая более сложную типизацию.

Ниже можно увидеть общий тип Array с параметром T (Type), который позволяет создать тип строкового, числового массива и тд:

```ts
// Type:
type Array<T> = T[];
// Usage:
const StringArr: Array<string> = ["hello", "hi"];
const NumberArr: Array<number> = [3, 4];
```

### Syntax

Generics записываются рядом с названием типа, интерфейса или названия функции в треугольных скобках:

```ts
type Array<T> = T[];

interface TypedObj<T> {
  [key: string]: T;
}

function makeArrayFrom<T>(item: T): T[] {
  // ...
}
```

> Можно называть параметр любым именем, например `type Array<Item> = Item[];`, `T` лишь общепринятое название

### Usage

В целом, у дженериков 2 назначения:

- Они позволяют создавать динамичные типы, такие как `Array<T>`. Вообще, большинство встроенных типов, таких как `Requied<T>`, `Partial<T>` используют Generic
- С помощью них можно более точно типизировать функции, как вы увидите ниже

Предположим у нас есть функция, которая принимает значение и возвращает массив из таких значений:

```js
function makeArrayFrom(item, quantity) {
  let arr = [];
  for (let i = 0; i < quantity; i++) {
    arr.push(item);
  }
  return arr;
}

makeArrayFrom("hi", 3); // ["hi", "hi", "hi"]
```

Без дженериков мы не сможем явно указать, что результат функции `makeArrayFrom` будет массив типа параметра `item`:

```ts
function makeArrayFrom(item: unknown, quantity: number): unknown[] {}
```

Дженерики решают эту проблему:

```ts
function makeArrayFrom<T>(item: T, quantity: number): T[] {}
```

### Advanced

Можно ограничить тип параметра, например, можно сделать чтобы функция выше принимала либо строки, либо числа:

```ts
function makeArrayFrom<T extends string | number>(
  item: T,
  quantity: number
): T[] {
  //...
}

makeArrayFrom(null, 2); // Error, "item" should be string or number
```

Также можно использовать сразу несколько параметров:

```ts
interface Record<Key extends string | number, Value: any> {
    [key in Key]: Value
}
// Ниже мы создаем объект с ключами-числами(массив) и значениями строками:
const StringArray: Record<number, string> = ['hi', 'world']
```
