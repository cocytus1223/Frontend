# 1. bootstrap 框架

> Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JAVASCRIPT 的，特点是：灵活简洁、代码优雅、美观大方。使得 Web 开发更加快捷。

[bootstrap 官方网站](https://getbootstrap.com/)

[bootstrap 中文网](http://www.bootcss.com/)

**特点**：

- 组件简洁大方、代码规范精简、界面自定义性强。
- Bootstrap 是基于 HTML5 和 CSS3 开发的，它在 jQuery 的基础上进行了更为个性化和人性化的完善，形成一套自己独有的网站风格，并兼容大部分 jQuery 插件。
- Bootstrap 中包含了丰富的 Web 组件，根据这些组件，可以快速的搭建一个漂亮、功能完备的网站。

**优点**：

- 有自己的生态圈，不断的更新迭代
- 提供了一套简洁、直观、强悍的组件
- 标准化的 HTML+CSS 编码规范
- 让开发更简单，提高了开发效率。
- 扩展性强，虽然界面组件样式已经定义好了，我们还可以自定义，修改默认样式。

## 1.1. Bootstrap 版本：

目前市面上使用的最多的是 3.x.x 版本。各个版本的介绍：

- 2.3.2 版本：
  - 2013 年之后停止维护
  - 优点：兼容性好，支持更广泛的浏览器
  - 缺点：代码不够简洁、功能不够完善
- 3.x.x 版本：
  - 优点：稳定，偏向于开发响应式布局，移动设备优先的 WEB 项目
  - 缺点：放弃了 IE67，对 IE8 支持但是界面效果不友好
- 4.x.x 测试阶段

## 1.2. 基本模板

目录结构说明

![目录结构](G:/z_work/21%E6%9C%9F/02-%E7%A7%BB%E5%8A%A8web-day03/02-%E7%AC%94%E8%AE%B0/image/2.png)

```html
<!DOCTYPE html>
<!-- 使用HTML5文档，使用中文简体 -->
<html lang="zh-CN">
  <head>
    <!-- meta1. 使用utf-8编码 -->
    <meta charset="utf-8" />
    <!-- meta2. 当前页面在在IE浏览器访问时，使用最新的ie浏览器内核进行渲染 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <!-- meta3. 视口设置 -->
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, user-scalable=no"
    />
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都必须跟随其后！ -->
    <title>bootstrap基本模板</title>

    <!-- 引入bootstrap的核心样式文件 -->
    <link href="lib/bootstrap/css/bootstrap.min.css" rel="stylesheet" />

    <!-- html5shiv是用来解决IE8以下浏览器不支持HTML5语义化标签的问题 -->
    <!--
      respond是用来解决IE8以下浏览器不支持媒体查询的问题，注意：respond不支持file协议打开
    -->
    <!-- 条件注释：IE浏览器专属 -->
    <!--[if lt IE 9]>
      <script src="lib/html5shiv/html5shiv.min.js"></script>
      <script src="http://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

    <!-- bootstrap依赖与jquery，因此需要在bootstrap之前引入jquery文件 -->
    <script src="lib/jquery/jquery-1.12.4.js"></script>
    <!-- 引入bootstrap的核心js文件 -->
    <script src="lib/bootstrap/js/bootstrap.min.js"></script>
  </body>
</html>
```

## 1.3. 全局样式

### 1.3.1. normalize.css

> Normalize.css 是一种 CSS reset 的替代方案。经过@necolas 和@jon_neal 花了几百个小时来努力研究不同浏览器的默认样式的差异，这个项目终于变成了现在这样。

[官网](http://necolas.github.io/normalize.css/)

[github 网址](https://github.com/necolas/normalize.css)

normalize 的特点：

- **保护有用的浏览器默认样式**而不是完全去掉它们
- **一般化的样式**：为大部分 HTML 元素提供
- **修复浏览器自身的 bug**并保证各浏览器的一致性
- **优化 CSS 可用性**：用一些小技巧

**`Normalize.css`支持包括手机浏览器在内的超多浏览器，同时对 HTML5 元素、排版、列表、嵌入的内容、表单和表格都进行了一般化。尽管这个项目基于一般化的原则，但我们还是在合适的地方使用了更实用的默认值。**

[Normalize.css 与 CSS reset 区别](http://www.cnblogs.com/webpush/p/4974063.html)

### 1.3.2. container 容器

Bootstrap 需要为页面内容和栅格系统包裹一个 .container 容器。默认带了 15px 的 padding 值。

`.container` 类用于固定宽度并支持响应式布局的容器。

```html
<div class="container">...</div>
```

`.container-fluid` 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<div class="container-fluid">...</div>
```

### 1.3.3. 栅格系统

栅格系统，也叫网格系统

- `.row`用于抵消`.container`容器的 15px 的 padding 值
- 可以在`.row`中嵌套`column`

栅格系统常用类（总共 12 列）

| 类名       | 例子      | 解释                     |
| ---------- | --------- | ------------------------ |
| .col-xs-xx | .col-xs-6 | 在超小屏幕（及以上）生效 |
| .col-sm-xx | .col-sm-6 | 在小屏幕（及以上）生效   |
| .col-md-xx | .col-md-6 | 在中屏幕（及以上）生效   |
| .col-lg-xx | .col-lg-3 | 在大屏幕及生效，占 1/4   |
| .col-lg-xx | .col-lg-4 | 在大屏幕及生效，占 1/3   |
| .col-lg-xx | .col-lg-6 | 在大屏幕及生效，占 1/2   |

【案例：响应式栅格系统】

```html
<!--
  需求：
    1. 在大屏时显示6个等分的列
    2. 在中屏时显示4个等分的列
    3. 在小屏时显示3个等分的列
    4. 在超小屏时显示2个等分的列
-->
```

```html
<div class="col-lg-4">
  <!-- 栅格系统无处不在，只要父盒子有宽度，就可以使用栅格系统 -->
  <div class="row">
    <div class="col-lg-6"></div>
    <div class="col-lg-6"></div>
  </div>
</div>
```

```html
<!-- 使用 .col-md-offset-* 类可以将列向右侧偏移。 -->
<div class="row">
  <div class="col-lg-3"></div>
  <!-- col-lg-offset-3:在大屏下，这个div将向右侧偏移3个单位 -->
  <div class="col-lg-6 col-lg-offset-3"></div>
</div>
```

### 1.3.4. 响应式工具

```javascript
//1. 大屏显示
//2. 中屏不显示
//3. 小屏显示
//4. 超小屏不显示
```

推荐使用 hidden 相关的属性

### 1.3.5. 其他

bootstrap 内置的东西是在太多，不可能每一个都详细的讲，但是 bootstrap 文档简洁明了，当我们用到了相关的东西的时候，再来详细的进行讲解。
