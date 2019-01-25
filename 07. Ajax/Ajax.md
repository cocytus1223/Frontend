# Ajax

## 什么是 Ajax？

Ajax 即`Asynchronous Javascript And XML`（异步 JavaScript 和 XML）,是指一种创建交互式网页应用的网页开发技术。AJAX 不是一门的新的语言，而是使用现有标准的新方法。AJAX 可以在不重新加载整个页面的情况下，与服务器交换数据。这种异步交互的方式，使用户单击后，不必刷新页面也能获取新数据。使用 Ajax，用户可以创建接近本地桌面应用的直接、高可用、更丰富、更动态的 Web 用户界面。

## XMLHttpRequest 对象

XMLHttpRequest 对象是浏览器提供的一个 API，用来顺畅地向服务器发送请求并解析服务器响应，当然整个过程中，浏览器页面不会被刷新。

XMLHttpRequest 只是一个 JavaScript 对象，确切的说，是一个构造函数。换句话说，它一点也不神秘，它的特殊之处只在于它是由客户端(即浏览器)提供的（而不是 JavaScript 原生的），除此之外，它有属性，有方法，需要通过 new 关键字进行实例化，我们只需掌握它们就好；
XMLHttpRequest 对象是不断被扩展的。随着 XML 对象被广泛的接收，W3C 也开始着手制定相应的标准来规范其行为。目前，XMLHttpRequest 有两个级别：1 级提供了 XML 对象的实现细节，2 级进一步发展了 XML 对象，额外添加了一些方法，属性和数据类型。但是，并不是所有浏览器都实现了 XML 对象 2 级的内容；

让我们先从剖析 XMLHttpRequest 实例的属性和方法开始，先创建一个 XML 对象的实例：

```JavaScript
var xhr = new XMLHttpRequest();
```

该实例的属性，方法有：

**方法**：

- `.open()`：准备启动一个 AJAX 请求；
- `.setRequestHeader()`：设置请求头部信息；
- `.send()`：发送 AJAX 请求；
- `.getResponseHeader()`: 获得响应头部信息；
- `.getAllResponseHeader()`：获得一个包含所有头部信息的长字符串；
- `.abort()`：取消异步请求；

**属性**：

- `.responseText`：包含响应主体返回文本；
- `.responseXML`：如果响应的内容类型时 text/xml 或 - `application/xml`，该属性将保存包含着相应数据的 XML DOM 文档；
- `.status`：响应的 HTTP 状态；
- `.statusText`：HTTP 状态的说明；
- `.readyState`：表示“请求”/“响应”过程的当前活动阶段

另外，浏览器还为该对象提供了一个 `onreadystatechange` 监听事件，每当 `XML` 实例的 `readyState` 属性变化时，就会触发该事件的发生。

## GET 请求

GET 是最常见的请求类型，最常用于向服务器查询某些信息。必要时，可以将查询字符串参数追加到 URL 的末尾，以便将信息发送给服务器。对 XHR 而言，位于传入 open()方法的 URL 末尾的查询字符串必须经过正确的编码才行。

```JavaScript
//1. 创建一个XMLHttpRequest对象
var xhr = new XMLHttpRequest();

//2. 设置请求行
// 第一个参数:请求方式  get/post
// 第二个参数:请求的地址 需要在url后面拼上参数列表
xhr.open("get", "01.php?name=haha");

//3. 设置请求头(get不用设置)
//请求头中可以设置Content-Type,用以说明请求主体的内容是如何编码
//get请求时没有请求体,无需设置请求头

//4. 设置请求体
//get请求的请求体为空,因为参数列表拼接到url后面了
xhr.send(null);
```

## POST 请求

POST请求通常用于向服务器发送应该被保存的数据，POST请求应该把数据作为请求的主体提交。

```JavaScript
var xhr = new XMLHttpRequest();

// 1. 设置请求行 post请求的参数列表在请求体
xhr.open("post", "02.php");

// 2. 设置请求头, POST请求必须要设置 content-type, 标记请求体内容的解析方式, 不然后端无法解析获取数据
xhr.setRequestHeader( "content-type", "application/x-www-form-urlencoded" );
//在请求发送过程中会对数据进行序列化处理，以键值对形式？key1=value1&key2=value2的方式发送到服务器

// 3. 设置请求体
xhr.send( "name=zs&age=18" );
```
