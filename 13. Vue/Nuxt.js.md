# Nuxt.js

## 概述

## 工作流（生命周期）

![nuxt.js](images/nuxtjs.svg)

1. `incoming Request`：浏览器发出一个请求
2. `nuxtServerInit`：服务端接收到这个请求之后，检查当前有没有 nuxtServeInit 这个配置项，如果有的话就执行这个函数，`store action`是用来操作 vuex 的
3. `middleware`： 中间件，这个中间件和路由相关，可以做任何你想要的功能
4. `validate()` 配合动态路由去做一些高级验证，比如说是否允许跳转到这个页面来
5. `asyncData()&fetch()`：获取数据，asyncData()获取的数据是用来渲染 vue 组件的，fetch 通常是用来修改 vuex 的
6. `Render`：渲染
7. `Navigate(<nuxt-link>)`：发起了一个新的路由循环

## nuxt.js 安装

```bash
npx create-nuxt-app <项目名>
```

它会让你进行一些选择:

1. 在集成的服务器端框架之间进行选择:
   - None (Nuxt 默认服务器)
   - Express
   - Koa
   - Hapi
   - Feathers
   - Micro
   - Adonis (WIP)
2. 选择您喜欢的 UI 框架:
   - None (无)
   - Bootstrap
   - Vuetify
   - Bulma
   - Tailwind
   - Element UI
   - Ant Design Vue
   - Buefy
3. 选择你想要的 Nuxt 模式 (Universal or SPA)
4. 添加 axios module 以轻松地将 HTTP 请求发送到您的应用程序中。
5. 添加 EsLint 以在保存时代码规范和错误检查您的代码。
6. 添加 Prettier 以在保存时格式化/美化您的代码。

当运行完时，它将安装所有依赖项，因此下一步是启动项目:

```bash
npm run dev
```

应用现在运行在 `http://localhost:3000` 上运行。

注意：`Nuxt.js` 会监听 `pages` 目录中的文件更改，因此在添加新页面时无需重新启动应用程序。

## 配置

Nuxt.js 默认的配置涵盖了大部分使用情形，可通过 `nuxt.config.js` 来覆盖默认的配置。

- build
  Nuxt.js 允许你在自动生成的 vendor.bundle.js 文件中添加一些模块，以减少应用 bundle 的体积。如果你的应用依赖第三方模块，这个配置项是十分实用的。

- cache
  该配置项让你开启组件缓存策略以提升渲染性能。

关于 cache 配置项的详细文档

- css
  该配置项用于定义应用的全局（所有页面均需引用的）样式文件、模块或第三方库。

关于 css 配置项的详细文档

- dev
  该配置项用于配置 Nuxt.js 应用是开发还是生产模式。

关于 dev 配置项的详细文档

- env
  该配置项用于定义应用客户端和服务端的环境变量。

关于 env 配置项的详细文档

- generate
  该配置项用于定义每个动态路由的参数，Nuxt.js 依据这些路由配置生成对应目录结构的静态文件。

- head
  该配置项用于配置应用默认的 meta 标签。

- loading
  该配置项用于个性化定制 Nuxt.js 使用的加载组件。

- modules
  该配置项允许您将 Nuxt 模块添加到项目中。

- modulesDir
  该配置项允许您定义 Nuxt.js 应用程序的 node_modules 文件夹。

- plugins
  该配置项用于配置那些需要在 根 vue.js 应用 实例化之前需要运行的 Javascript 插件。

- rootDir
  该配置项用于配置 Nuxt.js 应用的根目录。

- router
  该配置项可用于覆盖 Nuxt.js 默认的 vue-router 配置。

- srcDir
  该配置项用于配置应用的源码目录路径。

- transition
  该配置项用于个性化配置应用过渡效果属性的默认值。

## 路由

Nuxt.js 依据 `pages` 目录结构自动生成 `vue-router` 模块的路由配置。

要在页面之间使用路由，我们建议使用`<nuxt-link>` 标签。

例如:

```html
<template>
  <nuxt-link to="/">首页</nuxt-link>
</template>
```

### 基础路由

假设 `pages` 的目录结构如下：

```bash
pages/
--| user/
-----| index.vue
-----| one.vue
--| index.vue
```

那么，Nuxt.js 自动生成的路由配置如下：

```js
router: {
  routes: [
    {
      name: 'index',
      path: '/',
      component: 'pages/index.vue'
    },
    {
      name: 'user',
      path: '/user',
      component: 'pages/user/index.vue'
    },
    {
      name: 'user-one',
      path: '/user/one',
      component: 'pages/user/one.vue'
    }
  ]
}
```

### 动态路由

```bash
pages/
--| _slug/
-----| comments.vue
-----| index.vue
--| users/
-----| _id.vue
--| index.vue
```

Nuxt.js 生成对应的路由配置表为：

```js
router: {
  routes: [
    {
      name: 'index',
      path: '/',
      component: 'pages/index.vue'
    },
    {
      name: 'users-id',
      path: '/users/:id?',
      component: 'pages/users/_id.vue'
    },
    {
      name: 'slug',
      path: '/:slug',
      component: 'pages/_slug/index.vue'
    },
    {
      name: 'slug-comments',
      path: '/:slug/comments',
      component: 'pages/_slug/comments.vue'
    }
  ]
}
```

### 路由参数校验

Nuxt.js 可以让你在动态路由组件中定义参数校验方法。

举个例子： `pages/users/_id.vue`

```js
export default {
  validate({ params }) {
    // 必须是number类型
    return /^\d+$/.test(params.id)
  }
}
```

如果校验方法返回的值不为 true 或 Promise 中 resolve 解析为 false 或抛出 Error ， Nuxt.js 将自动加载显示 404 错误页面或 500 错误页面。

### 嵌套路由

假设文件结构如：

```bash
pages/
--| users/
-----| _id.vue
-----| index.vue
--| users.vue
```

Nuxt.js 自动生成的路由配置如下：

```js
router: {
  routes: [
    {
      path: '/users',
      component: 'pages/users.vue',
      children: [
        {
          path: '',
          component: 'pages/users/index.vue',
          name: 'users'
        },
        {
          path: ':id',
          component: 'pages/users/_id.vue',
          name: 'users-id'
        }
      ]
    }
  ]
}
```

## 页面模板

layout：公共组件放到模板里面去，新建的 page 声明`layout：''`就可以了

## 异步数据

### asyncData

`asyncData`方法会在组件（限于页面组件）每次加载之前被调用。它可以在服务端或路由更新之前被调用。 在这个方法被调用的时候，第一个参数被设定为当前页面的上下文对象，你可以利用 `asyncData`方法来获取数据，Nuxt.js 会将 `asyncData` 返回的数据融合组件 data 方法返回的数据一并返回给当前组件。

## Vuex
