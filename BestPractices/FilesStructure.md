### The main rule

Самое главное правило, которое стоит усвоить из этой главы: 

ВСЕГДА СОБЛЮДАЙ СТРУКТУРУ ПРОЕКТА!


Это значит:

- Создавай нужные файлы, папки, модули по аналогии с тем как созданы другие файлы, папки, модули в проекте
- Именуй файлы так, как принято в проекте

```js

Components/
// Existing components:
    Tabs/ 
        index.ts
        Tabs.tsx
        Tabs.module.css
    ...
// ✅ Good:
    Button/ 
        index.ts
        Button.tsx
        Button.module.css
// ❌ Bad:
    Tag/
        Tag.tsx
        tag.module.css 
```

### Project structure example:

Существует бесчисленное множество вариаций того, как структурировать файлы проекта. В этом разделе мы приведем пример популярной структуры:

```js
public/
    assets/
    translation/
    ...
src/
    components/
    features/
    pages/
    shared/
    store/
    styles/
    ...
package.json
package-lock.json
// other config files
// ...
```
Public

> Шрифты, статичные изображения, переводы и прочее:
```
public/
    assets/
        fonts/
        images/
    translation/
        en/
            translation.json
        ru/
        ...
    favicon.ico
```

Src

> О содержании каждой папке ниже
```
src/
    components/
    features/
    pages/
    shared/
    store/
    styles/
```

Components (aka "ui")
> Также альтернативные названия папки - ui, UIKit, etc.

В такой папке содержатся переиспользуемые компоненты, обычно абстрактные UI элементы, такие как Button, Icon, Tabs, Accordeon и тд.

```js
components/
    Badge/ // folder
    Button/
    Input/
    icons/
        CloseIcon/
        ArrowIcon/
    Tabs/
    ...
    index.ts // for exports

```

Features

В этой папке также лежат компоненты, но они отличаются от компонентов папки Сomponents следующими особенностями:

- Они не абстракты 
> "Modal" - component, "OrderModal" - feature
- Часто содержат логику, привязку к global state, api
> например, CookiesAlert проверяющий разрешение на использование cookies
- Они используют ui компоненты внутри себя но добавляют конкретику
> OrderList рендерит ui List компонент, но отображает данные о заказах

Pages

Папка компонентов - страниц
> В Next.js страницы рендерятся на основе корневой папки pages/ (не путать с src/pages/ ), тем не менее для удобства часто создают и src/pages, об этом подробнее в наших разделах Next.js
```
pages/
    Home/
        HomePage.tsx
    About/
    ...
```

Shared (aka "Common")

Очень важная папка, которая содержит различные переиспользуемые сущности

```js
constants/
    actions.ts
    form.ts
```
  Что могут содержать файлы:
  - постоянные величины, обычно in uppercase 
  >  TABlET_WIDTH, DAY_IN_MILISECONDS, ...
  - общие значения, которые потом можно перенастроить
  > PASSWORD_LENGHT, DEFAULT_FETCH_STATUS, REQUEST_MAX_LIMIT, SLIDER_ROTATION_TIME, ...
  - названия redux action
  > GET_USERS, RESET_FORM, etc.
  - enums
  > UserRoles, Statuses, ...

Helpers (aka utils)

Хелперы - полезные функции, которые могут пригодится в разных частях проекта, а также функции, которые могут выполнять сложные алгоритмы и их использование напрямую в компонентах загрязнит код и сделает его громоздким

```js
helpers/
    capitalize.ts
    filter.ts
    transforms.ts
```
Примеры таких функций:
```js
export function capitalize = (args) => {..};
export function convertLinks = (args) => {..};
export function isNull = (args) => {..};
export function isMobile = (args) => {..};
export function isSensorDevice = (args) => {..};
export function validateEmail (email) => {...}
...
```
Hooks 

Папка с хуками проекта, вот часть популярных:
```ts
hooks/
    useAppSelector.tsx
    useAppDispatch.tsx
    useTranslate.tsx
    useClickOutside.tsx
    useWindowDimensions.tsx
    useCrumbs.tsx
```

mocks

Папка для моков - фейковых данных, которые используются когда api не готово/невозможно использовать в момент разработки

```
mocks/
    categories.json
    profile.json
    products.json
    ...
```

api/

Папка, в которой представлены функции и другие необходимые элементы для работы с сервером и получением данных, о ней подробее в разделе api/

types/

Общие типы проекта - существует лишь в typescript приложениях


styles

В этой папке лежат общие стили проекта

```js
styles/
    style.scss // общий файл с импортами 
    reset.scss // aka globals, normalize - сброс стилей
    breakpoints.scss // breakpoints для адаптива
    colors.scss // константы цветов
    mixins.scss // миксины
    fonts.scss // константы для шрифтов и жирности
```

store (aka redux)

Папка содержит все файлы связанные с redux, структура может отличаться, например:

```js
store/
    index.ts // rootReducer
    slices/ // or reducers/
        productSlice.ts
        userSlice.ts
        ...
    thunks/ //for async calls, using thunk
    sagas/ //for async calls, using saga
    actions/ // obsolete for RTK
    constants/ // obsolete for RTK
    selectors/ // functions to get state
```
