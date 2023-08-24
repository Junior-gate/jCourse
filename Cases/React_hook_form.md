## React-hook-form & React

react-hook-form - это интуитивно понятный, многофункциональный API, обеспечивающий бесперебойную работу  при создании форм..


### Подключение npm пакета

```
npm install react-hook-form
```

### Базовое подключение

```jsx
// импортируем  хук useForm, Controller - интерфейс с методами useForm
import { Controller, useForm } from "react-hook-form";

const { control } = useForm() // control - объект который содержит методы для регистрации компонентов в React Hook Form.  
                              // !!ВАЖНО не обращатся на прямую к свойствам этого объекта  


export const Input = () => {
  return (
    <Controller
      name='yourName' // уникальное имя инпута
      control={control} // объект управления
      render={({ field: { onChange, value } }) => ( /* рендеринг, объект filed возможные свойства { onChange, value, onBlur, name, ref}
                                                                  объект filedState возможные свойста {invalid, isTouched, isDirty, error,}*/
        <input
          placeholder='test'
          type='text'
          onChange={onChange}
          value={value}
        />
      )}
    />
  );
};
```


### Пример использования 

```jsx

import { Controller, useForm } from "react-hook-form";

const { control, handleSubmit } = useForm() 

const onSumbit = data => console.log(data) // {firstName: }


export const Input = () => {
  return (
    <Controller
            name='firstName'
            control={control}
            render={({ field: { value, onChange } }) => (
              <input
                placeholder='firt name'
                value={value}
                onChange={onChange}
                type='text'
              />
            )}
            defaultValue=''
          />
    <Controller
            name='lastName'
            control={control}
            render={({ field: { value, onChange } }) => (
              <input placeholder='firt name' value={value} onChange={onChange} type='text' />
            )}
            defaultValue=''
          />
    <Button
            title='Отправить'
            onClick={handleSubmit(onSubmit)}
          />
  );
};
 
```
