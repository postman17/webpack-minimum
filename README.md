- Создаем папку front
- yarn init (прописываем поля)
- создаем папку src, в ней index.js и style.scss
- Добавляем в package.json под main 
```  
  "scripts": {
    "build": "webpack --config webpack.js --progress --colors --mode=development"
  }
```
- создаем webpack.js, добавляем в него 
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
- в style.scss добавляем
```
@import "~bootstrap/scss/bootstrap";
@import "scss/default";
```
- создаем папку scss в ней файл default
- создаем в папке src файл index.html, в него добавляем 
```
<script src="build/bundle.js"></script>
```
- делаем yarn run build
- можно работать
