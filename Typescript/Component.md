### Как типизировать react компонент?

Есть ряд подходов, которые используются при типизации компонентов, рассмотрим самые популярные

### FC - встроенный тип в react 

Это подход, который мы используем в данный момент.

Без пропсов:

```ts
import { FC } from 'react'

export const Button: FC = () => {<div>Text</div>}
```

С пропсами:
```ts
import { FC } from 'react'

interface ButtonProps {
  name: string
  children: ReactNode
}

export const Button: FC<ButtonProps> = ({ name, children }) => {<div>{name}</div>}
```

Компонент-страница в Next.js:

```ts
import { NextPage } from 'next'

export const HomePage: NextPage = () => {<Home />}
```

Альтернативные способы типизации:

### VFC - не имеет children по умолчанию

```ts
import { VFC } from 'react'

interface ButtonProps {
  name: string
}
// компонент нельзя использовать как <Button>Text</Button>
// если выше не указать children prop

export const Button: VFC<ButtonProps> = ({ name }) => {<div>{name}</div>}
```

### Отказ от FC

 [Подробно о минусах FC](https://fettblog.eu/typescript-react-why-i-dont-use-react-fc/)

```ts
const Component = (props: ComponentProps): JSX.Element => {
}
```

