# CORS

На практике часто приходится сталкиваться с проблемами CORS.

Иногда достаточно верно настроить headers для запроса, но в некоторых ситуациях приходится запускать проект без CORS.

Проще всего это сделать в гугл хром, запустив его через командную строку:

Mac
```
open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security --ignore-certificate-errors
```
> Убедитесь, что гугл хром лежит у вас именно по пути выше или замените его на свой

Windows
```
```