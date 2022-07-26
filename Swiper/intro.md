## Swiper & React

swiper - это библиотека с современными мобильными слайдерами.


### Подключение npm пакета

```
npm i swiper
```

### Базовое подключение

```jsx
import { Swiper, SwiperSlide } from 'swiper/react';

import 'swiper/css';

export const Slider = () => {
  return (
    <Swiper>
      <SwiperSlide>Slide 1</SwiperSlide>
      <SwiperSlide>Slide 2</SwiperSlide>
    </Swiper>
  );
};
```

## Подключение модулей


```jsx
// импортируем сами модули
import { Navigation, Pagination } from 'swiper';

//импортируем стили для модулей
import 'swiper/css/navigation';
import 'swiper/css/pagination';

export const Slider = () => {
  return (
    <Swiper
        // обязательно добавить здесь модули, которые мы используем 
        modules={[Navigation, Pagination]}
        // для настройки пагинации (точки)
        pagination={{ clickable: true }}
        // для настройки навигации (стрелки)
        navigation
    >
      <SwiperSlide>Slide 1</SwiperSlide>
      <SwiperSlide>Slide 2</SwiperSlide>
    </Swiper>
  );
};
```
## Кастомная пагинация (точки)

```jsx
export const Slider = () => {
    const pagination = {
        clickable: true,
        renderBullet: function (index, className) {
            return '<span class="' + className + '">' + (index + 1) + "</span>";
        },
    };
    return (
        <Swiper
            modules={[Pagination]}
            pagination={pagination}
        >
        <SwiperSlide>Slide 1</SwiperSlide>
        <SwiperSlide>Slide 2</SwiperSlide>
        </Swiper>
    );
};
```
## Кастомная навигация (стрелки)

```jsx
export const Slider = () => {
    return (
        <div>
            <Swiper
                modules={[Navigation]}
                navigation={{
                    // сюда прописываем классы элементов которые мы хотим использовать в роли кнопок
                    nextEl: '.custom-button-next',
                    prevEl: '.custom-button-prev',
                }}
            >
                <SwiperSlide>Slide 1</SwiperSlide>
                <SwiperSlide>Slide 2</SwiperSlide>
            </Swiper>

            // добавляем кнопки с соответствующими классами, которые мы прописали в (nextEl и prevEl)
            // обязательно вне компонента Swiper
            <div className='custom-button-prev'></div>
            <div className='custom-button-next'></div>

        </div>
    );
};
```

## Swiper Thumbs
Thumbs - это пагинация слайдера в виде галереи картинок

---
Для обычного React приложения
```jsx
  import { useState } from 'react';
  import { Swiper, SwiperSlide } from 'swiper/react';
  import { Thumbs } from 'swiper';

  export const SliderWithThumbs = () => {
    const [thumbsSwiper, setThumbsSwiper] = useState(null);

    return (
        <>
            // основной слайдер
            <Swiper 
                modules={[Thumbs]} 
                thumbs={{ swiper: thumbsSwiper }}
            >
                {/* ... */}
            </Swiper>
            // слайдер галерея для пагинации
            <Swiper
                modules={[Thumbs]}
                onSwiper={setThumbsSwiper}
            >
                {/* ... */}
            </Swiper>
        </>
    )
  }
```
Для приложения с Next.js
```jsx
export const SliderWithThumbsForNext = ({ images }) => {

  const swiperRef = useRef<HTMLDivElement | null>(null)
// функция котрая будет переключать слайды
  const changeSlide = (slideId: number) => {
    swiperRef.current?.swiper.slideTo(slideId)
  }

  return (
    <div>
        <div onClick={e => e.stopPropagation()}>
        // это основной слайдер
            <Swiper
                ref={swiperRef}
                spaceBetween={10}
                navigation={true}
                modules={[FreeMode, Navigation, Thumbs]}
            >
                {images.map((item, index) => (
                    <SwiperSlide key={index}>
                    <div className={s.galleryModalSlide}>
                        <Image
                        onClick={e => e.stopPropagation()}
                        width={1062}
                        height={624}
                        src={item}
                        />
                    </div>
                    </SwiperSlide>
                ))}
            </Swiper>
        </div>
        // Здесь через Array.map() рендерим картинки для галерии
        <div className={s.sliderThumbs}>
            {images.map((image, id) => (
                <div
                    key={id}
                    onClick={e => {
                    e.stopPropagation()
                        changeSlide(id)
                    }}
                >
                    <Image width={60} height={36} src={image} />
                </div>
            ))}
        </div>
    </div>
   )
  
}
```


