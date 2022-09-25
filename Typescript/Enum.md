# Enum


### Intro
Enum может потребоваться для перечислений, когда есть несколько ограниченных значений:

```ts
enum Roles {
    CUSTOMER = 'customer',
    ADMIN = 'admin',   
}
// такая запись удобна, так как помогает избежать опечаток
if(user.role === Roles.CUSTOMER) {...}
```

### Numeric enum
По умолчанию значения enum являются числа от 0:

```ts
enum Statuses {
    request, // 0
    success, 
    error 
}

console.log(Statuses.error) // 2
```
> Это очень популярный случай, так как с API могут приходить статусы в числовом формате

### Statuses

Вот несколько примеров работы с числовыми enum:

```ts

enum LoginStatuses {
    request, // 0
    success = 200,
    unknown_email = 422, 
    error = 500
}
```

```ts
// Иногда с API приходят статусы с пропуском значений, нвпример нет статуса "3", можно сделать так:
enum PaymentStatus {
    requested, 
    in_progresss,
    paid, // 2
    canceled = 4,
    failed, // 5
}
```

> Указывать числа по умолчанию излишне:

```ts
// ❌ Wrong:
enum Statuses {
    request = 0, 
    success = 1, 
    error = 2
}
// ✅ Correct:
enum Statuses {
    request, 
    success, 
    error 
}
```

### Тип enum

```ts

enum BidStatus {
  Winning = 'winning',
  Outbid = 'outbid',
  Lost = 'lost',
  Won = 'won',
}

// ✅ Тип любого значения:
interface Props {
    bidStatus: BidStatus // 'winning' | 'outbid' ... 
}

// ✅ Тип любого ключа enum:
// "Winning" | "Outbid" | "Lost" | "Won" :
type bidKey = keyof BidStatus;

```

### Cases

enum может быть полезен для разных перечислений - статусов, ролей, фильтров(by_price, by_date), сортировов(asc, desc), направлений(up, down), вебсокетов и т.д