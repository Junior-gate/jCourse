# jCourse

## classnames

Мы используем библитеку classnames в большинстве проектов для удобства работы с css классами


### overview

Библиотека classnames позволяет присоединяться к разным classes исходя из разных условий более простым способом.

мы используем фунцию classnames(cn) которая принимает строки и объекты и собирает из них строку с классами:

```js
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'
```

### import

Используем сокращенный импорт:

```js
// ❌ Wrong:
import classnames from 'classnames'
const buttonClasses = classnames('primary', 'disabled')

// ✅ Correct:
import cn from 'classnames'
const buttonClasses = cn('primary', 'disabled')

```

### basic usage

Собираем все нужные классы в переменную и передаем в classname элемента:

```jsx
 const buttonClass = cn(s.button, props.className)

 return (
    <Button className={buttonClass} />
 )

```
### dynamic class

Иногда нам нужно добавлять класс в зависимости от условия, например добавить disabled класс, когда props.disabled === true

```js
 const buttonClass = cn(s.button, {[disabled]: isDisabled})
 // => 'button disabled', если isDisabled === true, 
 // иначе 'button'
```

Еще одна возможность, добавлять нужный класс по значению:

```js
let buttonType = 'primary'; 
const buttonClass = cn({ [`btn-${buttonType}`]: true });
// => 'btn-primary',
```

### common mistakes

```js

const isDisabled = props.disabled;

// ❌ Wrong:
const buttonClasses = cn('button', isDisabled ? 'disabled' : '')

// ❌ Wrong:
const buttonClasses = cn('button', [disabled]:  isDisabled === true)

// ✅ Correct:
const buttonClasses = cn('button', {[disabled]: isDisabled})

```

```js
// ❌ Wrong:
const buttonClasses = cn('button' + ' ' + 'primary')

// ✅ Correct:
const buttonClasses = cn('button', 'primary')

```