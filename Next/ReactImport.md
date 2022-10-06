# React Import

В Next.js не нужно импортировать React:

```js
// ❌ Wrong - нет необходимости
import react from 'react'

// ✅ Correct - импортируем нужные модули
import { FC, useState } from 'react'

const Component = () => {...}
```