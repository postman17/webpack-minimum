- Создаем папку front
- yarn init (прописываем поля)
- Устанавливаем webpack
```
yarn add webpack -D
```
- Устанавливаем пакеты
```
yarn add bootstrap
yarn add style-loader
yarn add css-loader
yarn add sass-loader
yarn add node-sass
```
- создаем папку src, в ней index.js и style.scss
- Добавляем в package.json под main 
```  
  "scripts": {
    "build": "webpack --config webpack.js --progress --colors --mode=development"
  }
```
- создаем webpack.js(в папке front), добавляем в него 
```
var path = require('path');
var webpack = require('webpack');

module.exports = {
   entry : {
       main: [
           path.join(__dirname, 'src/style.scss')
       ]
   },

   output : {
       path: path.join(__dirname, 'src/build'),
           filename: 'bundle.js',
   },

    module: {
        rules: [
            {
                 test: /\.css$/,
                 use: [
                   'style-loader',
                   'css-loader'
                 ]
            },
            {
                test: /\.(sass|scss)$/,
                exclude: /(node_modules|bower_components)/,
                use: [
                'style-loader', 'css-loader', 'sass-loader'
                ]
            },
        ]
    },
};
```
- в style.scss(в папке src)добавляем
```
@import "~bootstrap/scss/bootstrap";
@import "scss/default";
```
- создаем папку scss(в папке src) в ней файл default.scss
- создаем в папке src файл index.html, в него добавляем 
```
<script src="build/bundle.js"></script>
```
- делаем yarn run build
- можно работать
- для того чтобы webpack автоматически применял изменения добавляем в package.json(во вкладку scripts):
```
"watch": "webpack --config webpack.js --mode development --watch"
```
После добавления верхней строчки можно запускать сборку через команду:
```
yarn run watch
```
И при изменении в файле default webpack будет автоматически собирать bundle.js