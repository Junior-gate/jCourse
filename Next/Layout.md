### How to create a layout?

В отличие от React приложений, где Layout может создаваться с помощью react-router-dom, используя Outlet, в Next.js он создается иначе.

1) Необходимо создать компонент Layout, который принимает children в качестве props:

```jsx
export const Layout: FC<LayoutProps> = ({ children }) => {
    return (
    <div>
      <Header />
      <main className={s.container}>
        <div className={s.content}>
          {children}
        </div>
      </main>
      <Footer />
    </div>
  )
}
```

2) Компонент необходимо отрендерить в root/pages/_app.tsx:

```jsx
    <Provider store={store}>
        <Layout> <- Наш layout
          <Component {...pageProps} />
        </Layout> <- 
    </Provider>
```

3) Часто в приложениях Layout может зависеть от страницы - где-то хедер другого цвета, где-то есть хлебные крошки, а где-то layout вообще не нужен. Делаем route-based layout:

```jsx
export const Layout: FC<LayoutProps> = ({ children }) => {
  // определяем страницу
  const router = useRouter() 
  const findPath = (element: string) => {
    return router.pathname.startsWith(element)
  }
  // определяем роуты для которых нужен голубой хедер,
  // такое обычно хранится в constants/ 
  const withBlueHeader = ['/', '/products', '/cart'];

  // возвращаем нужный layout
  if (withBlueHeader.find(findPath)) {
    return <BlueLayout>{children}</BlueLayout>
  }
  // можно cоздать множество условий по типу withBlueHeader
  return (
      <CommonLayout bright withBreadCrumbs withSearch>
        {children}
      </CommonLayout>
  )
  // return children - если layout не нужен
}

```
> аналогично, можно сделать Layout зависимый от роли пользователя, например отображать разное меню для продавца/покупателя