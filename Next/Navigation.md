# Navigation

Немного о работе с навигацией по приложению

### Link

Чтобы создавать ссылки на другие страницы, мы используем `Link` компонент из Next.js:

```jsx
import Link from 'next/link'

const Demo = () => {
    return 
    <div>
         <Link href='/'>
            <a className={styles.link}>
              Click me
            </a>
          </Link>
          <Link href={`/blogs/${id}`}> 
           <Button text='click me' />
          </Link>
    </div>
}
```

### Get current pathname

Чтобы определить текущую страницу, мы можем использовать `useRoute` hook из Next.js:

```jsx
import { useRouter } from 'next/router'

const Demo = () => {
    const { pathname } = useRouter()  //  '/about'
    return 
    <div>
        {pathname}  
    </div>
}
```

### Push route

Чтобы сделать редирект пользователя, не используя ссылки, мы можем использовать `push` метод. 
Например, мы можем делать редирект на главную после попадания на 404 страницу:


```jsx
import { useRouter } from 'next/router'

const NotFoundPage = () => {
    const router = useRouter()  

    useEffect(() => {
        setTimeout(() => {
            router.push('/')
        }, 3000);
    }, [router])

    return 
    <div>404 page</div>
}
```

### Query

О работе с Queries в Next.js можно почитать в отдельной [статье](Query.md)