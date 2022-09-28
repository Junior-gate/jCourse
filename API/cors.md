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

Создать новый ярлык для хрома, правой кнопкой, свойства, в поле где стрелка дополнить запись
<br>
Расположения ярлыка(в зависимости от разрядности своей винды):<br>
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"<br>
К нему надо дописать вот это:<br>
```
 --disable-web-security --user-data-dir="C:/ChromeDevSession" --disable-site-isolation-trials
```
Должно выйти примерно так:
```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --disable-web-security --user-data-dir="C:/ChromeDevSession" --disable-site-isolation-trials
```
