# Features VS Components

Во многих проектах компоненты могут быть разбиты на фичи (features) и ui компоненты (components). Рассмотрим разницу.

### Фичи и компоненты

**UI компоненты** - абстрактные, переиспользуемые компоненты, на основе которых можно создавать готовые части приложения. Это такие популярные элементы как Button, Title, Modal, Accordeon, Breadcrumbs, Switch и т.д. Все компоненты UI библиотек, таких как Material UI, And Design.

Они пишутся с нуля, либо они создаются на основе уже готовых решений - Material UI, Ant Design, и тд.

> Если дизайн проекта сделан с заделом на уже готовые системы, такие как Material UI, то в проект устанавливается соответствующая библиотека. Если дизайн уникальный, то обычно ограничиваются установкой библиотек под конкретные сложные компоненты - react-select, react-calendar, и т.д. На основе компонентов создаются фичи, используя props.

**Фичи** - готовые элементы приложения. В отличие от компонентов, они имеют привязку к контексту. List - компонент, ShopList - фича(привязка к Shop сущности). Modal - компонент, ThankYouModal - фича (содержит конкретный текст). Также фичи могут быть привязаны к redux, содержать конкретную логику.

> фичи лежат в features/ папке, UI компоненты лежат в components/ (или UI/, UIKit/)
### Как определить, куда положить свой компонент?

Если это типичный  UI элемент - Button, Switch, абстрактен (не привязан к конкретным сущностям - user, shop, product, blog и т.д), то это UI компонент, иначе feature.

### Composition

Популярный приём - композиция. Мы используем UI элемент и создаем на основе него фичу - компонент который возвращает UI компонент но уже с готовыми props:

- Modal - UI компонент
- MakeOrderModal - feature

```jsx
// MakeOrderModal.tsx
import { Modal } from 'components'
export const MakeOrderModal = () => 
<Modal>
    <div>Do you want to make an order?</div>
    <Button>Yes</Button>
</Modal>
```

- Card - UI компонент, карточка которая имеет заголовок и контент
- CompanyCard - фича, карточка с названием и описанием компании, большого размера
```jsx
// components/Сard.tsx
export const Card = ({ header, content, isLarge }) => ...
```
```jsx
// features/CompanyСard.tsx
import { Card } from 'components'
export const CompanyCard = ({ name, description }) => 
<Card header={name} content={description} isLarge />
```
> Как можно увидеть, это очень удобно. Если у нас будет ProductCard, мы также можем использовать Card в основе. 