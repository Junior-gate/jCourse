# Constants

В препроцессорах, таких как sass, scss есть ряд возможностей, таких как создания переменных. Переменные позволяют проще обновлять тему в проекте, например цвета, шрифты и делают код чище.

> CSS также имеет поддержку переменных, причем в них также есть ряд преимуществ над переменными в sass/scss

### Example of vars

Обычно переменные используют для цветов, реже для жирности, размеров и z-index. Вот несколько примеров.

```scss
// colors
$color-white: #fff;
$color-grey-f358: #f3f5f8;

$shadow-standard-a06: 0px 10px 34px rgba(8, 15, 52, 0.06);

// font weight
$fw-extrabold: 800;

// font 
$font-Pangram: Pangram, Montserrat, -apple-system, BlinkMacSystemFont, Segoe UI,
  Roboto, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue,
  sans-serif;

// z-index
$z-index-modal: 1000;

// size
$checkbox-size: 22px;
```

### Usage

Обычно все переменные хранятся в одном файле/папке, затем их можно использовать через @use из нужного файла:

```scss
@use 'styles/style.scss' as *; // Import vars

// ❌ Bad:
.title {
  color: $fff;
  font-weight: 700;
}

// ✅ Good:
.title {
  color: $color-primary; // color var
  font-weight: $fw-bold;
}

```