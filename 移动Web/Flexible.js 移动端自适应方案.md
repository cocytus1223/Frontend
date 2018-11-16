# Flexible.js 移动端自适应方案

## 一些基本概念

**视窗 viewport**：

简单的理解，viewport 是严格等于浏览器的窗口。在桌面浏览器中，viewport 就是浏览器窗口的宽度高度。但在移动端设备上就有点复杂。
移动端的 viewport 太窄，为了能更好为 CSS 布局服务，所以提供了两个 viewport:虚拟的 `viewportvisualviewport` 和布局的 `viewportlayoutviewport`。

**物理像素(physical pixel)**：

物理像素又被称为设备像素，他是显示设备中一个最微小的物理部件。每个像素可以根据操作系统设置自己的颜色和亮度。正是这些设备像素的微小距离欺骗了我们肉眼看到的图像效果。

**设备独立像素(density-independent pixel)**：

设备独立像素也称为密度无关像素，可以认为是计算机坐标系统中的一个点，这个点代表一个可以由程序使用的虚拟像素(比如说 CSS 像素)，然后由相关系统转换为物理像素。

**CSS 像素**：

CSS 像素是一个抽像的单位，主要使用在浏览器上，用来精确度量 Web 页面上的内容。一般情况之下，CSS 像素称为与设备无关的像素(device-independent pixel)，简称 DIPs。

**屏幕密度**：

屏幕密度是指一个设备表面上存在的像素数量，它通常以每英寸有多少像素来计算(PPI)。

**设备像素比(device pixel ratio)**：

设备像素比简称为 dpr，其定义了物理像素和设备独立像素的对应关系。它的值可以按下面的公式计算得到：

```html
设备像素比 ＝ 物理像素 / 设备独立像素
```

在 JavaScript 中，可以通过 `window.devicePixelRatio` 获取到当前设备的 dpr。而在 CSS 中，可以通过`-webkit-device-pixel-ratio`，`-webkit-min-device-pixel-ratio` 和 `-webkit-max-device-pixel-ratio` 进行媒体查询，对不同 dpr 的设备，做一些样式适配(这里只针对 webkit 内核的浏览器和 webview)。

dip 或 dp,（device independent pixels，设备独立像素）与屏幕密度有关。dip 可以用来辅助区分视网膜设备还是非视网膜设备。

## flexible 是什么？

`lib-flexible`是一个制作 H5 适配的开源库，可以点击这里下载相关文件，获取需要的 JavaScript 和 CSS 文件。

github 地址：<https://github.com/amfe/lib-flexible>
官方文档地址：<https://github.com/amfe/article/issues/17>

## flexible 的实质

flexible 实际上就是通过 JS 来动态改写 meta 标签，代码类似这样：

```js
var metaEl = doc.createElement("meta");
var scale = isRetina ? 0.5 : 1;
metaEl.setAttribute("name", "viewport");
metaEl.setAttribute(
  "content",
  "initial-scale=" +
    scale +
    ", maximum-scale=" +
    scale +
    ", minimum-scale=" +
    scale +
    ", user-scalable=no"
);
if (docEl.firstElementChild) {
  document.documentElement.firstElementChild.appendChild(metaEl);
} else {
  var wrap = doc.createElement("div");
  wrap.appendChild(metaEl);
  documen.write(wrap.innerHTML);
}
```

事实上他做了这几样事情：

- 动态改写<meta>标签
- 给<html>元素添加 data-dpr 属性，并且动态改写 data-dpr 的值
- 给<html>元素添加 font-size 属性，并且动态改写 font-size 的值
