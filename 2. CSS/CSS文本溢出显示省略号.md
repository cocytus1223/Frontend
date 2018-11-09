# 1. CSS 文本溢出显示省略号

## 1.1. 单行

语法

```css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

## 1.2. 多行

### 1.2.1. 直接用 css 属性设置(只有-webkit 内核才有作用)

```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
```

移动端浏览器绝大部分是 webkit 内核的，所以该方法适用于移动端；

- -webkit-line-clamp 用来限制在一个块元素显示的文本的行数，这是一个不规范的属性（unsupported WebKit property），它没有出现在 CSS 规范草案中。

- display: -webkit-box 将对象作为弹性伸缩盒子模型显示。

- -webkit-box-orient 设置或检索伸缩盒对象的子元素的排列方式。

- text-overflow: ellipsis 以用来多行文本的情况下，用省略号“…”隐藏超出范围的文本。

### 1.2.2. 利用伪类

语法

```html
<div id="con">
  <span id="txt"
    >文本溢出显示省略号,文本溢出显示省略号,文本溢出显示省略号,文本溢出显示省略</span
  >

  <span class="t"></span>
</div>

<style>
  #txt {
    display: inline-block;

    height: 40px;

    width: 250px;

    line-height: 20px;

    overflow: hidden;

    font-size: 16px;
  }

  .t:after {
    display: inline;

    content: "...";

    font-size: 16px;
  }
</style>
```

### 1.2.3. 利用绝对定位和 padding;(跨浏览器解决方案)

```html
<p id="con2">
  文本溢出显示省略号,文本溢出显示省略号,文本溢出显示省略号,文本溢出显示省略<span
    class="t2"
    >...</span
  >
</p>

<style>
  #con2 {
    position: relative;

    height: 40px;

    width: 250px;

    line-height: 20px;

    overflow: hidden;

    padding-right: 12px;
  }

  .t2 {
    position: absolute;

    right: 0;

    bottom: 0;
  }
</style>
```

这个方法的原理是：首先在包含文字的元素里，嵌入一个`<span>...</span>`，然后包含文字的元素右侧留出...的位置(padding-right),最后利用绝对定位将...定位至右侧的 padding-right 区域
