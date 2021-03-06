# vue-router

## SPA

单页 Web 应用（single page application，SPA），就是只有一个 Web 页面的应用，
是加载单个 HTML 页面，并在用户与应用程序交互时动态更新该页面的 Web 应用程序。
对于传统的多页面应用程序来说, 每次请求服务器返回的都是一个完整的页面, 需要加载很多资源文件，css js 图片

对于单页应用程序来说, 只有第一次会加载页面, 以后的每次请求, 仅仅是获取必要的数据。然后, 由页面中 js 解析获取的数据, 展示在页面中

### 优势

1. 减少了请求体积，加快页面响应速度，降低了对服务器的压力
2. 更好的用户体验，让用户在 web app 感受 native app 的流畅

### 缺点

1. 由于加载了多个页面所需的框架、应用代码和资源，导致初始页面加载时间较长。
2. 服务器还需要进行额外的工作，需要将所有请求路由配置到单个入口点，然后由客户端接管路由。
3. SPA 依赖于 JavaScript 来呈现内容，但并非所有搜索引擎都在抓取过程中执行 JavaScript，他们可能会在你的页面上看到空的内容。这无意中损害了应用的搜索引擎优化（SEO）。

### 主要技术点

1. ajax / axios
2. 哈希值（锚点）的使用（window.location.hash #）
3. hashchange 事件

### 实现思路

监听锚点值变化的事件，根据不同的锚点值，请求相应的数据

1. 锚点（#）原本用作页面内部进行跳转，定位并展示相应的内容
2. SPA 中，锚点被用作请求不同资源的标识，请求数据并展示内容

## vue-router 是什么？

这里的路由并不是指我们平时所说的硬件路由器，这里的路由就是 **SPA（单页应用）的路径管理器**。再通俗的说，`vue-router` 就是 WebApp 的链接路径管理系统。
`vue-router` 是 Vue.js 官方的路由插件，它和 vue.js 是深度集成的，适合用于构建单页面应用。vue 的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。传统的页面应用，是用一些超链接来实现页面切换和跳转的。在 `vue-router` 单页面应用中，则是路径之间的切换，也就是组件的切换。路由模块的本质就是**建立起 url 和页面之间的映射关系**。

### 为什么不用 a 标签？

因为用 Vue 做的都是单页应用，当你的项目准备打包时，运行 npm run build 时，就会生成一个 dist 文件夹，这里面只有静态资源和一个 index.html 页，所以写的`<a></a>`标签是不起作用的，必须使用 `vue-router` 来进行管理。

## vue-router 实现原理

vue-router 在实现单页面前端路由时，提供了两种方式：Hash 模式和 History 模式；根据 mode 参数来决定采用哪一种方式。

### Hash 模式

vue-router 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，当 URL 改变时，页面不会重新加载。
hash（#）是 URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说 hash 出现在 URL 中，但不会被包含在 http 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说 Hash 模式通过锚点值的改变，根据不同的值，渲染指定 DOM 位置的不同数据。
hash 模式的原理是 onhashchange 事件(监测 hash 值变化)，可以在 window 对象上监听这个事件。

### History 模式

由于 hash 模式会在 url 中自带#，如果不想要很丑的 hash，我们可以用路由的 history 模式，只需要在配置路由规则时，加入"mode: 'history'",这种模式充分利用了 html5 history interface 中新增的 pushState() 和 replaceState() 方法。这两个方法应用于浏览器记录栈，在当前已有的 back、forward、go 基础之上，它们提供了对历史记录修改的功能。只是当它们执行修改时，虽然改变了当前的 URL ，但浏览器不会立即向后端发送请求。

```js
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

当你使用 history 模式时，URL 就像正常的 url，例如 `http://yoursite.com/user/id`，也好看！

不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 `http://oursite.com/user/id` 就会返回 404，这就不好看了。

所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 `index.html` 页面，这个页面就是你 app 依赖的页面。

## 传参的三种方式

### 方案一：\$router.push

```js
getDescribe(id) {
//   直接调用$router.push 实现携带参数的跳转
  this.$router.push({
    path: `/describe/${id}`,
  })
```

需要对应路由配置如下：

```js
{
  path: '/describe/:id',
  name: 'Describe',
  component: Describe
}
```

很显然，需要在 `path` 中添加`/:id` 来对应 `$router.push` 中 `path` 携带的参数。在子组件中可以使用来获取传递的参数值。

```js
$route.params.id
```

### 方案二：

父组件中：通过路由属性中的 name 来确定匹配的路由，通过 params 来传递参数。

```js
this.$router.push({
  name: 'Describe',
  params: {
    id: id
  }
})
```

对应路由配置: 注意这里不能使用:/id 来传递参数了，因为父组件中，已经使用 params 来携带参数了。

```js
{
  path: '/describe',
  name: 'Describe',
  component: Describe
}
```

子组件中: 这样来获取参数

```js
$route.params.id
```

### 方案三：

父组件：使用 path 来匹配路由，然后通过 query 来传递参数
这种情况下 query 传递的参数会显示在 url 后面?id=？

```js
this.$router.push({
  path: '/describe',
  query: {
    id: id
  }
})
```

对应路由配置：

```js
{
path: '/describe',
name: 'Describe',
component: Describe
}
```

对应子组件: 这样来获取参数

```js
$route.query.id
```

这里要特别注意 在子组件中 获取参数的时候是\$route.params 而不是
