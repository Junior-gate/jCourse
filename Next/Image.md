# Image

### Public

Все статичные картинки должны лежать в public папке:

```
public/
    assets/
        img/
            logo.svg
            star.png
            ...
```

### Image component

В Next.js не получится использовать привычный `<img/>` тэг, нужно импортировать `Image ` компонент:

```jsx
import Image from 'next/image'
import arrow from '/public/assets/img/arrow.svg'

const Demo = ({ img }) => {
    return 
    <div>
        <Image src={arrow} alt='' />
    </div>
}

```

### Types

Типизация image src:

```jsx
import Image, { ImageProps } from 'next/image'

type DemoProps = {
    img: ImageProps['src'] // тип src картинки в next.js
}
const Demo = ({ img }) => {
    return 
    <div>
        <Image src={img} alt='' />
    </div>
}

```

### Image Props

Немного о свойствах:
```js
import Image, { ImageProps } from 'next/image'

const Demo = ({ img }) => {
    const customLoader = ({ src, width, quality }) => {
        return `https://example.com/${src}?w=${width}&q=${quality || 75}`
    }
    return 
    <div>
        <Image 
        src={img} //src
        alt=''  // текст когда картинка не загрузилась
        width={12} // размеры
        height={12} 
        layout='fixed' // масштабирование, подробнее в документации
        placeholder='blur' // эффект blur пока картинка не загрузилась
        quality={75} // качество изображение 1-100
        unoptimized // картинка отобразится как есть, без оптимизации
        loader={customLoader} // функция преобразования src
        />
    </div>
}

```