### Default Props

#### Зачем нужны default props ?

<a name="default_props_reasons"></a> 
Есть ряд причин, когда задавать props по умолчанию. Примеры смотрите ниже.
- Избежать лишних проверок на undefined (например, type)
- Наглядно показать какое значение применится по умолчанию(например, isDisabled)
- Избежать ошибок (errors, например в случае errors.map)
- Для classnames во избежании "undefined" класса в некоторых случаях

Есть два основных способа задать значения props по умолчанию.

#### Destructusing

Подход, который мы используем всегда

```ts

interface ButtonProps {
    name: string,
    type?: "primary" | "secondary",
    isDisabled?: boolean
    classnames?: string,
    errors?: Error[]
}

export const Button: FC<ButtonProps> = ({ 
    name = 'Text',
    isDisabled = false,
    type = 'primary', 
    errors = []
}) => (<div>{name}</div>)

```

Вот тот же вариант, но с другим code-style:

```ts

interface ButtonProps {
    name: string,
    type?: "primary" | "secondary",
    isDisabled?: boolean
    classnames?: string,
    errors?: Error[]
}

export const Button: FC<ButtonProps> = (props) => {
    {   name = 'Text',
        isDisabled = false,
        type = 'primary', 
        errors = []
    } = props;
    return <div>{name}</div>
}

```

#### DefaultProps

Этот подход мы не используем никогда в наших проектах, к тому же он плохо работает с FC типом.

```ts

interface ButtonProps {
    name: string,
    type?: "primary" | "secondary",
    isDisabled?: boolean
    classnames?: string,
    errors?: Error[]
}

export const Button = (props: ButtonProps) => {<div>{props.name}</div>}

Button.defaultProps = {
    name: "Text",
    type: "primary",
    isDisabled: false
    classnames: '',
    errors: []
}
```

### Common issues

- Задавать значения по умолчанию там, где это не [нужно](#default_props_reasons) (например, в примере выше name будет лишним)
- сlassname по умолчанию:
```js
const Icon ({classnames = 'icon'}) => <div className={classnames}></div>
// в надежде что 'icon' класс применится всегда,
// даже когда classnames prop передан ('icon' перезапишется)
```