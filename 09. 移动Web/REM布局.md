# REM

## 各种布局特征的对比

由于市面上手机种类繁多，导致移动端的屏幕种类非常的混乱，比如有常见的`320px 360px 375px 384px 480px 640px`等。在开发中，美工一般只会提供750px或者是640px的设计稿，这就要求我们通过一张设计稿能够适配所有的屏幕。

通常解决方案如下：

- 流式布局：可以让各种屏幕都适配，只是在大屏幕中显示效果不是非常的友好,  即使这样, 由于开发效率高, 成本低, 目前使用流式布局的公司还是非常多的，比如 [亚马逊](https://www.amazon.cn/) 、[京东](https://m.jd.com/) 、[携程](https://m.ctrip.com/)
- 响应式布局：国内很少有大型网站使用，主要原因是**工作大，可维护性不好** 。所以一般都是中小型的门户或者博客类站点会采用响应式，因为这样可以节约成本。
- rem布局：rem能够适配所有的屏幕, 目前使用rem布局的有：[淘宝](https://m.taobao.com) 、 [苏宁](https://m.suning.com/)

## rem是什么？

`rem`（font size of the root element）是指相对于`根元素`的字体大小的单位。它是一个相对单位。

`em`（font size of the element）是指相对于当前元素的字体大小的单位。它也是一个相对单位。

```css
html{
  font-size:16px;
}
body {
  font-size:20px;
}
div.em {
  /*em的计算方式参照的当前元素的font-size，如果不设置，默认继承自父盒子*/
  width:2em;
  height:2em;
  background-color:red;
}
/*rem的计算方式参照的是html的font-size*/
div.rem {
  width:2rem;
  height:2rem;
  background-color:blue;
}
```

## rem与响应式

因为rem的基准点是根元素html的字体大小，因此我们只需要设置不同屏幕的html的font-size大小不一样就可以达到不同屏幕的适配了。

### rem与媒体查询

使用rem配合媒体查询可以适配多个终端

```css
    @media (min-width: 320px) {
      html {
        /*font-size: 100/750 * 320px*/
        font-size: 42.67px;
      }
    }
    @media (min-width: 375px) {
      html {
        font-size: 50px;;
      }
    }
    @media (min-width: 414px) {
      html {
        font-size: 55.2px;;
      }
    }
    @media (min-width: 480px) {
      html {
        font-size: 64px;;
      }
    }
    @media (min-width: 640px) {
      html {
        font-size: 85.33px;
      }
    }
    @media (min-width: 750px) {
      html {
        font-size: 100px;;
      }
    }
```

优点：使用媒体查询适配，速度快。

缺点：适配多个终端时，需要添加响应的代码。

### rem与javascript

通过javascript获取可视区的宽度，计算font-size的值，也可以适配多个终端。

```javascript
var base = 100;
var design = 750;

function responsive() {
  var pageWidth = window.innerWidth;

  if ( pageWidth <= 320 ) {
    pageWidth = 320;
  }

  if ( pageWidth >= 750 ) {
    pageWidth = 750;
  }

  var size = base / design * pageWidth;
  document.documentElement.style.fontSize = size + "px";
}

responsive();
window.addEventListener("resize", responsive);
```

优点：直接适配所有的终端

缺点：必须在页面加载之前设置html的font-size值，不然会出现文字大小调动的情况。