# Немного об отображении текстов из сервера

### HTML

Иногда с сервера может приходить готовая разметка, её можно отрендерить используя dangerouslySetInnerHTML:

```jsx
 const data = 'lorem <b>ipsum</b>';

  return (
    <div
      dangerouslySetInnerHTML={{__html: data}}
    />
  );
```
### Special symbols

Объемные текстовые данные, такие как description, могут содержать спецсимволы для переносов строк и дополнительных пробелов, например  "\r", "\n", и тд. Если просто вставить такой текст в div, пробелы не будут соблюдены:

```jsx
const textFromAPI = "Hello\nWorld"; 
//Hello
//World

// ❌ Wrong:
return <div>{textFromAPI}</div> 
// Hello World
```
Добавляем css свойство "white-space", в реальном коде такое будет реализовано через className:
```jsx
// ✅ Correct:
return <div style={{whiteSpace: 'pre-wrap'}}>{textFromAPI}</div> 
//Hello
//World
```
> Альтернативное решение - создать helper для парсинга строки наподобие `str.split('/n', <br/>)` и тд
