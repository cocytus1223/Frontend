# 1. CSS 预处理器

## 1.1. 为什么要有 CSS 预处理器

CSS 基本上是设计师的工具，不是程序员的工具。在程序员的眼里，CSS 是很头痛的事情，它并不像其它程序语言，比如说 PHP、Javascript 等等，有自己的变量、常量、条件语句以及一些编程语法，只是一行行单纯的属性描述，写起来相当的费事，而且代码难以组织和维护。

很自然的，有人就开始在想，能不能给 CSS 像其他程序语言一样，加入一些编程元素，让 CSS 能像其他程序语言一样可以做一些预定的处理。这样一来，就有了“CSS 预处器（CSS Preprocessor）”。

## 1.2. 什么是 CSS 预处理器

是 CSS 语言的超集，比 CSS 更丰满。
CSS 预处理器定义了一种新的语言，其基本思想是：用一种专门的编程语言，为 CSS 增加了一些编程的特性，将 CSS 作为目标生成文件，然后开发者就只要使用这种语言进行编码工作。

通俗的说，CSS 预处理器用一种专门的编程语言，进行 Web 页面样式设计，然后再编译成正常的 CSS 文件，以供项目使用。CSS 预处理器为 CSS 增加一些编程的特性，无需考虑浏览器的兼容性问题，例如你可以在 CSS 中使用变量、简单的逻辑程序、函数等等在编程语言中的一些基本特性，可以让你的 CSS 更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。

CSS 预处理器技术已经非常成熟，而且也涌现出了很多种不同的 CSS 预处理器语言，比如说：Sass（SCSS）、LESS、Stylus、Turbine、Swithch CSS、CSS Cacheer、DT CSS 等。如此之多的 CSS 预处理器，那么“我应该选择哪种 CSS 预处理器？”也相应成了最近网上的一大热门话题，在 Linkedin、Twitter、CSS-Trick、知呼以及各大技术论坛上，很多人为此争论不休。相比过计我们对是否应该使用 CSS 预处理器的话题而言，这已经是很大的进步了。

到目前为止，在众多优秀的 CSS 预处理器语言中就属 **Sass**、**LESS** 和 **Stylus** 最优秀，讨论的也多，对比的也多。本文将分别从他们产生的背景、安装、使用语法、异同等几个对比之处向你介绍这三款 CSS 预处理器语言。相信前端开发工程师会做出自己的选择——我要选择哪款 CSS 预处理器。

## 1.3. Less 简介

> CSS 需要书写大量看似没有逻辑的代码，不方便维护及扩展，不利于复用。成这些困难的很大原因源于 CSS 是一门非程序式语言，没有变量、函数、SCOPE（作用域）等概念。LESS/sass 为 Web 开发者带来了福音，它在 CSS 的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了 CSS 的编写，并且降低了 CSS 的维护成本，就像它的名称所说的那样，LESS 可以让我们用更少的代码做更多的事情。

本质上，LESS 包含一套自定义的语法及一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的 CSS 文件。LESS 并没有裁剪 CSS 原有的特性，更不是用来取代 CSS 的，而是在现有 CSS 语法的基础上，为 CSS 加入程序式语言的特性。

[官网](http://lesscss.org/)

[中文网](http://lesscss.cn/)

[Bootstrap 网站的 less 文档](https://less.bootcss.com/)

[推荐文章](http://www.w3cplus.com/css/less)

## 1.4. LESS 安装

## 1.5. Less 语法

### 1.5.1. 注释

less 的注释可以有两种。

1. 第一种注释：模板注释

   ```less
   // 模板注释，这里的注释转换成CSS后将会删除
   ```

2. 第二种注释：CSS 注释语法

   ```less
   /*这个注释是CSS中的注释，因此会编译到css中*/
   ```

**总结**：如果在 less 中写注释，我们推荐写第一种注释。除非是类似于版权等内容，就采用第二种注释。

### 1.5.2. 变量

我们可以把重复使用或经常修改的值定义为变量，在需要使用的地方引用这个变量即可。这样可以避免很多重复的工作量。

```less
@变量名: 变量值; //格式
@charset "UTF-8";
@wjs_color: #e92322;
body {
  background-color: @wjs_color;
}

div {
  width: 400px;
  height: 400px;
  border: 1px solid @wjs_color;
}
```

### 1.5.3. mixin 混入

Mixin 的作用是把重复的代码放到一个类当中，每次只要引用类名，就可以引用到里面的代码了，非常方便。

```less
@charset "UTF-8";
//混入
.btn {
  width: 200px;
  height: 50px;
  background-color: #fff;
}

.btn_border {
  border: 1px solid #ccc;
}

.btn_danger {
  background-color: red;
}

.btn_block {
  display: block;
  width: 100%;
}

//混入其他类的样式。
.my_btn {
  .btn();
  .btn_block();
  .btn_border();
  .btn_danger();
}
```

编译后的 css

```css
@charset "UTF-8";
.btn {
  width: 200px;
  height: 50px;
  background-color: #fff;
}
.btn_border {
  border: 1px solid #ccc;
}
.btn_danger {
  background-color: red;
}
.btn_block {
  display: block;
  width: 100%;
}
.my_btn {
  width: 200px;
  height: 50px;
  background-color: #fff;
  display: block;
  width: 100%;
  border: 1px solid #ccc;
  background-color: red;
}
```

缺点：写了很多类，但是都编译到 css 文件中了，其实我们需要的仅仅是.my_btn 这一个类。

**混入函数**：

不带参数的函数

```less
@charset "UTF-8";

//不会被编译
.btn() {
  width: 200px;
  height: 200px;
  background-color: #ccc;
}
.my_btn {
  .btn();
}
```

带参数的函数

```less
.btn_border(@width) {
  border: @width solid #000;
}
.my_btn {
  //如果函数定义了参数，调用的时候必须传入参数，否则会报错
  .btn_border();
  //传入参数，就不会报错
  .btn_border(10px);
}
```

带默认值的函数

```less
.btn_border(@width:1px) {
  border: @width solid #000;
}
.my_btn {
  //因为有默认值，所以不会报错
  .btn_border();
  //传入参数，会覆盖1px，也不会报错
  .btn_border(10px);
}
```

### 1.5.4. 嵌套

> 我们可以在一个选择器中嵌套另一个选择器来实现继承，这样很大程度减少了代码量，并且代码看起来更加的清晰。

- 使用伪类的时候 可以使用 `&` 表示自己

```less
/*
  less中的嵌套:
  1. 如果是后代选择器, 直接嵌套编写
  2. 如果是子代选择器, 加上 >
  3. 如果是交集选择器, &表示自己
  4. 如果是伪元素, &表示自己
*/
// 模块1
.father {
  width: 500px;
  height: 500px;
  &:before {
    content: "hehe";
  }
  &.active {
    background-color: red;
  }
  > .son {
    width: 300px;
    height: 300px;
    .box {
      width: 150px;
      height: 150px;
    }
  }
  > .son2 {
    width: 300px;
    height: 300px;
  }
  .box1,
  .box2 {
    background-color: blue;
  }
}

// 模块2
.father2 {
  .son2 {
  }
  .son3 {
  }
}
```

### 1.5.5. 导入

在开发阶段，我们可以将不同的样式放到多个文件中，最后通过@import 的方式合并。意思就是，当出现多个 less 文件时，怎么引用它们。

```less
// 语法: @import "less文件路径";  // 相对路径
@import "01-variable";

@import "02-maxin";

@import "03-mixin02";

@import "04-book";
```

模块化的思想，分模块进行管理这些 less 文件，最终只需要使用 import 将 less 引入到一起即可。

### 1.5.6. 函数（运算）

> 在我们的 CSS 中充斥着大量的数值型的 value，less 可以直接支持运算，也提供了一系列的函数提供给我们使用。

[函数手册](http://www.1024i.com/demo/less/reference.html)
