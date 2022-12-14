# js-portfolio

馃挍 Babel Loader para JavaScript
<h4>Apuntes</h4>
Babel te permite hacer que tu c贸digo JavaScript sea compatible con todos los navegadores
Debes agregar a tu proyecto las siguientes dependencias
NPM

npm install -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
Yarn

yarn add -D babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime
babel-loader nos permite usar babel con webpack
@babel/core es babel en general
@babel/preset-env trae y te permite usar las ultimas caracter铆sticas de JavaScript
@babel/plugin-transform-runtime te permite trabajar con todo el tema de asincronismo como ser async y await
Debes crear el archivo de configuraci贸n de babel el cual tiene como nombre .babelrc
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-transform-runtime"
  ]
}
Para comenzar a utilizar webpack debemos agregar la siguiente configuraci贸n en webpack.config.js
{
...,
module: {
    rules: [
      {
        // Test declara que extensi贸n de archivos aplicara el loader
        test: /\.js$/,
        // Use es un arreglo u objeto donde dices que loader aplicaras
        use: {
          loader: "babel-loader"
        },
        // Exclude permite omitir archivos o carpetas especificas
        exclude: /node_modules/
      }
    ]
  }
}
RESUMEN: Babel te ayuda a transpilar el c贸digo JavaScript, a un resultado el cual todos los navegadores lo puedan entender y ejecutar. Trae 鈥渆xtensiones鈥? o plugins las cuales nos permiten tener caracter铆sticas m谩s all谩 del JavaScript com煤n


HtmlWebpackPlugin
Es un plugin para inyectar javascript, css, favicons, y nos facilita la tarea de enlazar los bundles a nuestro template HTML.

Instalaci贸n
npm

npm i html-webpack-plugin -D
yarn

yarn add html-webpack-plugin -D
Al webpack config queda asi

const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'production', // LE INDICO EL MODO EXPLICITAMENTE
    entry: './src/index.js', // el punto de entrada de mi aplicaci贸n
    output: { // Esta es la salida de mi bundle
        path: path.resolve(__dirname, 'dist'),
        // resolve lo que hace es darnos la ruta absoluta de el S.O hasta nuestro archivo
        // para no tener conflictos entre Linux, Windows, etc
        filename: 'main.js', 
        // EL NOMBRE DEL ARCHIVO FINAL,
    },
    resolve: {
        extensions: ['.js'] // LOS ARCHIVOS QUE WEBPACK VA A LEER
    },
    module: {
        // REGLAS PARA TRABAJAR CON WEBPACK
        rules : [
            {
                test: /\.m?js$/, // LEE LOS ARCHIVOS CON EXTENSION .JS,
                exclude: /node_modules/, // IGNORA LOS MODULOS DE LA CARPETA
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    },
    // SECCION DE PLUGINS
    plugins: [
        new HtmlWebpackPlugin({ // CONFIGURACI脫N DEL PLUGIN
            inject: true, // INYECTA EL BUNDLE AL TEMPLATE HTML
            template: './public/index.html', // LA RUTA AL TEMPLATE HTML
            filename: './index.html' // NOMBRE FINAL DEL ARCHIVO
        })
    ]
}


Loaders
Fuera de contexto, webpack solamente entiende JavaScript y JSON. Los loaders nos permite procesar archivos de otros tipos para convertirnos en m贸dulos v谩lidos que ser谩n consumidos por nuestras aplicaciones y agregadas como dependencias.

En alto nivel, los loaders poseen 2 configuraciones principales:

test - propiedad que identifica cu谩les archivos deber谩n ser transformados
use - propiedad que identifica el loader que ser谩 usado para transformar a dichos archivos
Plugins
Mientras los loaders transforman ciertos tipos de m贸dulos, los plugins _son utilizados para extender tareas espec铆ficas, como la optimizaci贸n de paquetes, la gesti贸n de activos y la inyecci贸n de variables de entorno.

Una vez importado el plugin, podemos desear el personalizarlos a trav茅s de opciones.

npm i copy-webpack-plugin -D

--en construcci贸n--