# Cases handling

В работе на реальных проектах часто приходится сталкиваться с большим количеством проверок: являются ли данные пустые, авторизован ли пользователь, пустой ли список, идет ли загрузка данных, и т.д

Ниже представлен ряд советов по работе с проверками

### Long check 

```js
// ❌ Wrong:
if(user && user.profile && user.profile.orders){
    user.profile.orders.map((order) => ...)
}
// ✅ Correct:
user?.profile?.orders.map((order) => ...)

```

### Nulish operator

```tsx
// ❌ Wrong:
<Card image={image ? image : thumb} />

// ✅ Correct:
<Card image={image ?? thumb} />
```

### Missing check of length

```tsx
// ❌ Wrong - for empty list, error "Cannot read property "checked" of undefined"
items.filter((item) => item.checked).map((item) => ...)

// ✅ Correct:
items.length ? items.filter((item) => item.checked).map((item) => ...) : null
```

### Forgeting to handle empty data

При работе над задачами, где вы работаете с данными, которые могут оказаться пустыми, проверяйте условие задачи, что нужно отображать для пустых данных. В этом плане проверяйте длину списков и наличие данных у объекта.

### Unpredictable 1

```tsx
// ❌ Wrong 
items.length && items.map((item) => ...) // отобразится длина списка вместо данных

// ✅ Correct:
items.length ? items.map((item) => ...) : null
```

### Display Loading Process

При работе с запросами API помните об отображении загрузки - "loading..", loader, skeleton и тд

### Default props

См. [Default props](../React/DefaultProps.md)
