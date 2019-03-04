# 1. webpack

> *webpack*  是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler* )

[webpack 中文网](https://www.webpackjs.com/)

[webpack 官网](https://webpack.js.org/)

## webpack 做了点什么？

1. 代码转换功能

   - less/sass ====> css
   - ES6~ES9 语法 ====> ES3/ES5 保证所有浏览器都兼容
   - typescript ====> js 代码

2. 代码压缩、合并，把一些无用的代码删除
3. 提供了一个开发的环境
   - 自动打开浏览器，自动热更新
4. 开发完毕使用 webpack 先进行打包，再放到服务器进行部署

## 1.1. webpack 打包器说明

![webpack](../images/webpack.png)

## 1.2. webpack 模块说明

webpack 会把所有的资源都当成模块

- css
- js
- 图片
- 字体图标

webpack 给前端开发提供了模块化的开发环境

- 对于 js 文件，webpack 中支持 AMD、CMD、commonJS、ES6 模块化等语法
- 有了 webpack，我们可以在前端代码中使用任意的模块化语法

## 1.3. webpack 安装

- 项目初始化

```bash
yarn init -y
```

- 安装

```bash
yarn add webpack webpack-cli -D
```

- 配置 scripts

```js
  "scripts": {
    "build": "webpack index.js -o ./dist/bundle.js"
  },
```

- 使用命令

```bash
yarn build  # 就可以使用webpack进行打包了
```

## 1.4. 配置文件-webpack.config.js

> 如果所有的参数都拼接到 webpack-dev-server 的后面，非常的麻烦，因此可以提供 webpack.config.js 来进行配置

- 在项目的根目录下面新建`webpack.config.js`文件

```bash
const path = require('path')
// 这是一个nodejs文件
module.exports = {
  // 设置入口文件
  entry: path.join(__dirname, 'index.js'),
  // 设置出口
  output: {
    // 设置输出目录
    path: path.join(__dirname, 'dist'),
    // 输出文件
    filename: 'bundle.js'
  }
}
```

- 执行命令

```bash
webpack  // webpack会自动读取当前目录下的配置文件
```

- 模式的配置

```js
// 设置打包的模式
//'production'
//development
mode: 'production'
```

## 1.5. webpack-插件

> webpack 有着丰富的插件接口(rich plugin interface)。webpack 自身的多数功能都使用这个插件接口。这个插件接口使 webpack 变得**极其灵活**。

- 安装

```bash
yarn add  html-webpack-plugin -D
```

- `webpack.config.js`导入

```json
var HtmlWebpackPlugin = require('html-webpack-plugin');
```

- 使用

```js
module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'src', 'index.html')
    })
  ]
}
```

## 1.6. webpack-loaders

> webpack 可以使用  [loader](https://www.webpackjs.com/concepts/loaders)  来预处理文件。这允许你打包除 JavaScript 之外的任何静态资源。你可以使用 Node.js 来很简单地编写自己的 loader。

### 1.6.1. css-loader 处理 css 文件

- 安装

```bash
npm install --save-dev style-loader css-loader
```

- 配置

```js
  module: {
    // loader的规则
    rules: [
      {
        // 正则表达式，用于匹配所有的css文件
        test: /\.css$/,
        // 使用什么样的loader进行解析
        use: [ "style-loader", "css-loader"]
      }
    ]
  },
```

### 1.6.2. less-loader 处理 less 文件

- 安装

```bash
npm install --save-dev less-loader less
```

- 配置

```js
{
    // 匹配所有的less文件
    test: /\.less$/,
        use: [ "style-loader", "css-loader", "less-loader"]
}
```

### 1.6.3. file-loader 处理图片文件

- 安装

```bash
npm install --save-dev file-loader
```

- 配置

```js
{
    // 配置图片加载
    test: /\.(png|jpg|gif)$/,
    use: "file-loader"
}
```

### 1.6.4. url-loader 处理图片文件

> url-loader 与 file-loader 一样，也可以处理图片，但是 url-loader 可以以 base64 编码的方式处理图片

- 安装

```bash
npm install --save-dev url-loader
```

- 配置

```bash
{
    // 配置图片加载
    test: /\.(png|jpg|gif)$/,
        use: [
            {
                loader: 'url-loader'
            }
        ]
}
```

- base64 的优点

```js
1. 精灵图的作用：减小网络请求
2. base64:减少网络请求  通过京东查看base64编码的图片
```

- 设置 limit 参数

```js
{
    // 配置图片加载
    test: /\.(png|jpg|gif)$/,
        use: [
            {
                loader: 'url-loader',
                options: {
                    // 限定文件大小，注意：如果文件超出了大小，会自动调用file-loader，所以安装url-loader通过都要安装file-loader
                    limit: 8192
                }
            }
        ]
}
```

### 1.6.5. url-loader 处理字体图标文件

> 处理字体图标文件与处理图标一模一样

- 配置

```json
{
  // 配置字体图标加载
  "test": /\.(woff|woff2|eot|ttf|otf|svg)$/,
  "use": [
    {
      "loader": "url-loader",
      "options": {
        // 限定文件大小
        "limit": 819200
      }
    }
  ]
}
```

## 1.7. babel 处理高版本的 ES 语法

### 1.7.1. 介绍

Babel 是一个 JavaScript 编译器。

今天就开始使用下一代 JavaScript 语法吧！

[官网](http://babeljs.io/)

[中文网](https://www.babeljs.cn/)

babel 可以把最新版本的语法编译成浏览器能够兼容的代码（ES5）

### 1.7.2. 使用

- 安装

```bash
npm install -D babel-loader @babel/core @babel/preset-env
```

- 配置

```json
{
  "test": /\.js$/,
  "exclude": /(node_modules|bower_components)/,
  "use": {
    "loader": "babel-loader"
  }
}
```

- babel 配置文件

```js
//在项目根目录创建.babelrc配置文件
{
  "presets": ["@babel/preset-env"]
}

```

## 1.8. webpack-dev-server 的使用

在开发期间，会用到 webpack 的一个辅助包：`webpack-dev-server`,

`webpack-dev-server`的作用

- 自动开启 http 服务
- 自动打开浏览器
- 自动监视文件的变化

- 引入，每次修改代码，都需要重新打包

### 1.8.1. 基本使用

- 安装

```bash
npm install --save-dev webpack-dev-server
```

- 配置

```js
// webpack-dev-server提供了一个简单的服务器，并且能够实时重新加载
devServer: {
}
```

- 其他配置

```js
  devServer: {
     port: 9999,
     open: true,
  }
```

### 1.8.2. 热更新的说明

- 开启

```bash
hot: true
```

- 配置

```js
var webpack = require("webpack");

plugins: [
    new HtmlWebpackPlugin({
        template: path.join(__dirname,"src", 'index.html')
    }),
    new webpack.HotModuleReplacementPlugin()
],
```

- 热更新与 dev-server 模式不会在生产环境下用，生产环境还是需要`npm run build`

## 1.9. webpack-配置 vue-router

- 安装 vue-router

```bash
npm install vue-router
```

- 使用 vue-router

```js
// import Vue from "vue"
import Vue from 'vue/dist/vue.esm'

// 引入vue-router
import VueRouter from 'vue-router'

// 使用路由
Vue.use(VueRouter)
```

- 配置路由

```js
const router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home },
    { path: '/list', component: List }
  ]
})
```

- 使用路由

```js
new Vue({
  el: '#app',
  render: c => c(App),
  router
})
```

### 1.9.1. 路由功能模块化提取

vue-router 模块功能提取

```js
// 使用路由
import Vue from 'vue/dist/vue.esm'
import VueRouter from 'vue-router'

import Home from '../components/Home.vue'
import List from '../components/List.vue'
Vue.use(VueRouter)
const router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home },
    { path: '/list', component: List }
  ]
})

export default router
```
