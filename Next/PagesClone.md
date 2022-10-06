# Pages Clone

Как вы уже знаете, роутинг в Next.js строится на основе корневой папки `pages`, в которой лежат страницы. По этой причине писать код компонента страницы не очень удобно внутри самих файлов папки pages, так как роуты могут быть вложенными, диначескими и создание вспомогательного файла приведет к созданию нового роута. Проблема решается путем создания папки pages в src и импорта компонентов из нее в pages:

```js
pages/
    blogs/
        [id].tsx //BlogPage
        index.tsx //BlogsPage
src/
    pages/
        BlogPage/
            BlogPage.tsx
            BlogPage.scss
            helper.ts
        BlogsPage/
            BlogsPage.tsx
            BlogsPage.scss
```

Далее компонент из `src/pages` просто импортируется в нужный роут `/pages`:
```jsx
/// pages/blogs/[id].tsx
import { NextPage } from 'next'
import { BlogPage } from 'src/pages'

const Blog: NextPage = () => {
  return <BlogPage />
}

export default Blog

```