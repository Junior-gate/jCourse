### Работа с гит.

#### Именования

В большинстве проектов есть четкая договоренность по именованию веток и коммитов, ее необходимо соблюдать.

Вот, как мы называем ветки и сообщения коммитов в наших проектах.

Ветка:
тип задачи + 2 нижних подчеркивания + имя задачи(слова отделяются нижним подчеркиванием, нижний регистр)

Например:
```
feat__button_component
```
Основные типы задач feat, bug, refactor.
Например:
```
fix__bug_with_reload
refactor__profile_page
```

Коммит:
глагол(настоящее время) + описание

Например,
```
add modal component

fix bug with container

refactor logo component
```
И т.д

Для тех кто раньше не работал с ветками:
(сначало клонируем репо)
1. Перейти в ветку develop:
>`git checkout develop`
2. Получаем актуальную версию ветки
>`git pull`
3. Создаем ветку для задачи:
>`git checkout -b feat__task_name`
4. Сохранить написанный код для будущего коммита
>`git add file1.js file2.js`

либо сохраняем все файлы но только когда это необходимо:
>`git add .`
5. Делаем коммит:
>`git commit -m ‘add header component’`
6. Отправить ветку в github:
>`git push origin feat_task_name`
7. Вернуться в develop:
>`git checkout develop`
8. Обновить данные с репо:
>`git pull`

В гитхаб добавить pull request вашей ветки:
1. Открываете в гитхаб /pulls
2. Нажимаете create pull request (зеленая кнопка)
3. Выбираете base: develop , compare: your_branch_name 