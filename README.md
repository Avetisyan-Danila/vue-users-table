# vue-users-table

- Таблица вызывает модальное окно с формой.
- Данные из формы сохраняются в таблицу. Данные сохраняются в LocalStorage при обновлении страницы.
- В форме существует select с выбором родителя (любого из уже сохранённых пользователей).
- Таблица поддерживает вложенные уровни. Глубина вложенности неограниченна, то есть родителем может быть любой существующий пользователь.
- Данные в таблице сортируются по клику на заголовок колонки. Сортировка работает по подуровням.

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
