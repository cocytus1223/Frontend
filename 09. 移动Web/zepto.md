# 1. zepto 介绍

> **Zepto**是一个轻量级的**针对现代高级浏览器的 JavaScript 库， **它与 jquery**有着类似的 api**。 如果你会用 jquery，那么你也会用 zepto。

## 1.1. 官网网站

[github 地址](https://github.com/madrobby/zepto)

[中文文档](http://www.css88.com/doc/zeptojs_api/)

## 1.2. zepto 与 jquery 的区别

- jquery 针对 pc 端，主要用于解决浏览器兼容性问题，zepto 主要针对移动端。
- zepto 比 jquery 轻量，文件体积更小
- zepto 封装了一些移动端的手势事件

## 1.3. zepto 的基本使用

zepto 的使用与 jquery 基本一致，zepto 是分模块的，需要某个功能，就需要引入某个 zepto 的文件。

```javascript
<script src="zepto/zepto.js"></script>
<script src="zepto/event.js"></script>
<script src="zepto/fx.js"></script>

<script>

  $(function () {

    $(".box").addClass("demo");

    $("button").on("click", function () {

      $(".box").animate({width:500}, 1000);

    });
  });

</script>
```

## 1.4. zepto 的定制

安装 Nodejs 环境

1、下载 zepto.js

2、解压缩

3、cmd 命令行进入解压缩后的目录

4、执行`npm install`命令

5、编辑 make 文件的`41行`,添加自定义模块并保存，

7、然后执行命令 `npm run-script dist`

8、查看目录 dist 即构建好的 zepto.js

## 1.5. zepto 手势事件

zepto 中根据`touchstart touchmove touchend`封装了一些常用的手势事件

```javascript
tap; // 轻触事件,用于替代移动端的click事件，因为click事件在老版本中会有300ms的延迟
//穿透的问题    fastclick:
swipe; //手指滑动时触发
swipeLeft; //左滑
swipeRight; //右滑
swipeUp; //上滑
swipeDown; //下滑
```

**关于 tap 事件与 click 事件**：

1. click 事件在 pc 端非常用，但是在移动端会有 300ms 左右的延迟，比较影响用户的体验，300ms 用于判断双击还是长按事件，只有当没有后续的的动作发生时，才会触发 click 事件
2. tap 事件只要轻触了，就会触发，体验更好。
