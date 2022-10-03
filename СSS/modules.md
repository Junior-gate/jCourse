# CSS Modules

Быстрое руководство для тех кто никогда не использовал Модульный CSS

### Intro

Cуть в том, что css module под капотом модифицирует каждое название класса, например `.item`  трансформируется в класс с хэшем типа `.item__1OUvt`. Поэтому мы спокойно можем использовать классы `.item` в разных файлах и стили не будут конфликтовать. Модули решают ту же проблему что и `BEM`.


### File naming

Файлы со стилями именуются cо словом module:

```
button.module.css
Button.module.css
Logo.module.scss
Logo.module.sass
...
```

### Usage

Написание стилей ничем не отличается.

Container.module.css:
```css
.container {
  padding-top: 60px;
  margin-bottom: 60px;
}
```
Стили импортируем как объект (в примере, `s`) и передаем нужному тэгу/компоненту.

Container.tsx:
```jsx
import s from './TraderPage.module.scss'

const Container = (props) => {
     <div className={s.container}>{props.children}</div>
}
```

> Можно импортировать стили как угодно, например `import style from '../'` , `classname={style.container}`, но импорт через `s` более лаконичный, мы используем его во всех проектах. 


### Class naming

Обычно используется `camelCase` нотация, она удобна и позволяет избежать такой неудобной записи:
```js
// ❌ Bad:
s['component-name']

// ✅ Good:
s.componentName
```

Также мы не используем BEM стилистику, по причинам [выше](#intro)