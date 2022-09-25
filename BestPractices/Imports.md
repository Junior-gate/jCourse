### Import from index file

Плюс импорта из index файла состоит в том, что импорты становятся лаконичнее:

```js
// ❌ Bad:
import Accordion from 'components/Accordion/Accordion'

// ✅ Good:
import Accordion from 'components/Accordion'

```

Для этого нужно создать следующую структуру:
```
Accordion/
    Accordion.tsx
    index.ts 
    ...
```
```js
// index.ts
export * from './Accordion'

// Accordion.tsx
export const Accordion = ...
```

### Import from root folder

Но можно пойти и дальше, импортировать файлы из общей папки, например из Components, Features:


```js
// ❌ Bad:
import Button from 'components/Button'
import Tabs from 'components/Tabs'

// ✅ Good:
import { Tabs, Button } from 'components'

```

Для этого нужно создать index.ts в корневой папке:
```
components/
    index.ts
    Button/
        Button.tsx
        index.ts
        ...
    Tabs/
    ...
```
```js
// components/index.ts
export * from './Button'
export * from './Tabs'
...
```

### No default import

Еще один важный нюанс в том, что импорты по умолчанию бывают опасны (в больших проектах). Если импортировать модули - компоненты, хелперы и тд, меняя их названия, то в будущем это может создать сильную путаницу:

```js
// ❌ Bad:
import { Products } from 'components/OrderList'
import { getProductSum } from 'helpers/sumArray'

// ✅ Good:
import { OrderList } from 'components/OrderList'
import { sumArray } from 'helpers/sumArray'

// если другое название так необходимо, то можно сделать так:
const getProductSum = sumArray;
```

### Conclusion

Выше представлены хорошие практики, которые в частности используются в наших проектах. Необходимо учитывать, что все импорты в проекте должны иметь единый стиль! Если вы начинаете работать над проектом, где файлы не экмпортируются через index, то так делать не нужно, чтобы сохранить стилистику.