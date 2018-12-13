# 1. express

## 1.1. Express 框架

- **基于 Node.js 平台，快速、开放、极简的 web 开发框架**
- [express 官网](http://expressjs.com/)
- [express 中文网](http://expressjs.com.cn/)

### 1.1.1. 起步

- 安装：`npm i express`

```js
// 导入 express
const express = require('express')
// 创建 express实例，也就是创建 express服务器
const app = express()

// 路由
app.get('/', (req, res) => {
  res.send('Hello World!')
})

// 启动服务器
app.listen(3000, () => {
  console.log('服务器已启动')
})
```

### 1.1.2. API 说明

- `express()`：创建一个 Express 应用，并返回，即：app
- `app.get()`：注册一个 GET 类型的路由
  - 注意：只要注册了路由，所有的请求都会被处理（未配置的请求路径，响应 404）
- `res.send()`：发送数据给客户端，并自动设置 Content-Type
  - 参数可以是：字符串、数组、对象、Buffer
  - 注意：只能使用一次
- `req` 和 `res`：与 http 模块中的作用相同，是扩展后的请求和响应对象

## 1.2. 注册路由的三种方式

- 1 `app.METHOD`：比如：app.get / app.post / app.delete / app.patch
- 2 `app.all(path, callback)`
  - 注意：path 与 请求地址必须完全相同
  - 注意：可以处理任意的请求类型
- 3 `app.use(path, callback)` 更重要的作用是处理中间件
  - 注意：只要是以 path 开头的请求地址，都可以被 use 处理
  - 注意：可以处理任意的请求类型
  - 注意：path 参数可省略，默认值为：`/`

## 1.3. 模拟 Apache 服务器

- `req.path`：请求路径
  - 示例：URL 为'example.com/users?sort=desc'，path 表示：`/users`
- `res.sendFile()`

### 1.3.1. 处理静态资源

- 静态资源：图片、CSS、JavaScript 文件 等
- 如何处理？使用 express.static() 方法来托管静态资源
- 注意：`express.static()`可以调用多次
- 思考：`app.use('/web', express.static('web'))` 的含义？
  - 访问：`http://localhost:3000/web/anoceanofsky.jpg`

```js
// 托管web目录下的静态资源
app.use(express.static('web'))
// 相当于：app.use('/', express.static('web'))

// 访问上述静态资源
// http://localhost:3000/anoceanofsky.jpg

// 当请求达到服务器后，express就会到web目录下，查找anoceanofsky.jpg
// 并读取该文件，返回给浏览器
```

## 1.4. request 常用属性和方法

```js
// 获取请求路基中的参数，是一个对象 ---> Get请求参数
req.query

// 获取POST请求参数，需要配置`body-parser`模块， POST请求参数
req.body
```

- 获取`POST`请求参数

```js
// 导入body-parser模块
var bodyParser = require('body-parser')
// 将POST请求参数转化为对象，存储到req.body中
app.use(bodyParser.urlencoded({ extended: true })) // for parsing application/x-www-form-urlencoded

// 此时，就可以获取到POST请求参数了
console.log(req.body)
```

## 1.5. response 常用属性和方法

```js
// send() 发送数据给客户端，并自动设置Content-Type
res.send()

// 发送文件给浏览器，并根据文件后缀名自动设置Content-Type
// 注意：文件路径必须是绝对路径
res.sendFile(path.join(__dirname, 'index.html'))

// 设置HTTP响应码
res.sendStatus(200) // equivalent to res.status(200).send('OK')

// 设置响应头
res.set('Content-Type', 'text/plain')
res.set({
  'Content-Type': 'text/plain',
  cute: 'fangfang'
})

// 重定向
res.redirect('/index')
```

## 1.6. express 中使用模版引擎

安装

```bash
npm install express
npm install art-template
npm install express-art-template
```

给 express 绑定一个模版引擎

```javascript
//给express设置模版引擎
//参数1： 模版引擎的后缀名，  以后的模版文件都应该是 html结尾
//参数2： 使用什么模版引擎
app.engine('html', require('express-art-template'))
```

通过`res.render()`渲染模版引擎

```javascript
//参数1； 模版文件的路径,相对路径，回去views目录下查找
//参数2： 数据
res.render(path.join(__dirname, 'index.html'), { name: 'zs' })
```

关于模版引擎的配置

```javascript
//模版文件默认去aa目录下查找  默认值：  views
app.set('views', 'aa')

//设置模板引擎的默认后缀
app.set('view engine', 'html')
```

## 1.7. 中间件

**中间件（Middleware）**  是一个函数，它可以访问请求对象`req`, 响应对象`res`, 可以通过`next`参数将中间件传递给下一个中间件

中间件作用： 给 req 和 res 拓展功能

中间件的功能包括：

- 执行任何代码。
- 修改请求和响应对象。
- 终结请求-响应循环。
- 调用堆栈中的下一个中间件。

定义一个中间件

```javascript
//添加一个中间件
//中间件是啥：中间件就是一个函数，中间件可以访问到req和res，可以通过next发送给下一个中间件
app.use(function(req, res, next) {
  req.aa = 'zs'
  res.bb = '123'
  //中间件可以通过next传递给下一个中间件
  next()
})
```

## 1.8. body-parser 中间件的使用

- 获取 get 请求的参数：`req.query`
- 获取 post 请求的参数`req.body`，但是需要借助`body-parser`中间件

安装：

```bash
npm install body-parser
```

使用

```javascript
//1. 导入body-parser中间件
var bodyParser = require('body-parser')
//使用body-parser中间件
//extended:true 表示使用qs库来解析查询字符串  extended：false表示使用querystring库来解析字符串
app.use(bodyParser.urlencoded({ extended: false }))

//3. 通过req.body获取参数
app.post('/', (req, res) => {
  console.log(req.body)
  res.send('哈哈')
})
```

**注意：中间件是有执行顺序的**。

## 1.9. 实现自己的 body-parser 中间件

```javascript
//bodyParser.json(); 返回一个函数（中间件），会处理json数据
app.use((req, res, next) => {
  //给req增加一个body属性
  var result = ''
  req.on('data', chunk => {
    result += chunk
  })

  req.on('end', () => {
    req.body = querystring.parse(result)
    next()
  })
})
```

## 1.10. 外置路由的使用

目的：将路由封装到一个独立的路由模块中，有利于代码的封装和模块化

```javascript
/*
  router.js 文件代码如下:
*/

// 1 加载 express 模块
const express = require('express')

// 2 调用 express.Router() 方法，得到一个路由容器实例
const router = express.Router()

// 3 为 router 添加不同的路由
router.get('/', (req, res) => {
  res.send('hello express')
})

router.get('/add', (req, res) => {})

// 4. 将 router 路由容器导出
module.exports = router
```

```javascript
/*
  在 app.js 文件中：
*/
const express = require('express')

// 1 加载上面自定义的路由模块
const router = require('./router')

const app = express()

// 2. 将自定义路由模块 router 通过 app.use() 方法挂载到 app 实例上
//    这样 app 实例程序就拥有了 router 的路由
app.use(router)

app.listen(3000, () => {
  console.log('running...')
})
```
