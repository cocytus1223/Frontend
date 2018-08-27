<!-- TOC -->

- [1. 文档对象类型(DOM)](#1-文档对象类型dom)
  - [1.1. DOM节点`node`](#11-dom节点node)
  - [1.2. DOM节点属性](#12-dom节点属性)
    - [1.2.1. 标签的内容属性](#121-标签的内容属性)
      - [1.2.1.1. `innerHTML`](#1211-innerhtml)
      - [1.2.1.2. `innerText`](#1212-innertext)
      - [1.2.1.3. 区别](#1213-区别)
    - [1.2.2. 节点的属性](#122-节点的属性)
      - [1.2.2.1. `nodeName`](#1221-nodename)
      - [1.2.2.2. `nodeValue`](#1222-nodevalue)
  - [1.3. 获取元素的方法](#13-获取元素的方法)
    - [1.3.1. `getElementById()`](#131-getelementbyid)
    - [1.3.2. `getElementByTagName()`](#132-getelementbytagname)
    - [1.3.3. `getElementsByClassName()`](#133-getelementsbyclassname)
    - [1.3.4. `getElementsByTagName()`](#134-getelementsbytagname)

<!-- /TOC -->

# 1. 文档对象类型(DOM)

> DOM ( Document Object Model ) 文档对象模型,  是`W3C组织`推荐的一套操作网页元素的应用程序接口(API)。

`D`（文档）可以理解为整个Web加载的网页文档，`O`（对象）可以理解为类似window对象只来的东西，可以调用属性和方法，这里我们说的是document对象，`M`（模型）可以理解为网页文档的树形结构，DOM树由节点构成

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div></div>
  <p></p>
  <span></span>
</body>
</html>
```

## 1.1. DOM节点`node`

![node](images/node.png)

网页中的所有内容都是节点 (标签、属性、文本)

```JavaScript
  <ul class="box">
    <!-- 这是一些测试 -->
    <li>测试</li>
    <li>测试</li>
    <li>测试</li>
  </ul>
  //  ul : 标签节点
  //  class="box" : 属性节点
  //   <!-- 这是一些测试 --> : 注释节点
  //  测试 : 文本节点
```

## 1.2. DOM节点属性

### 1.2.1. 标签的内容属性

#### 1.2.1.1. `innerHTML`

以HTML代码格式获取或设置节点的内容

获取标签内容的时候，不管标签还是文本，都能获取到
`innerHTML`设置内容的时候，覆盖原来内容，标签也能生效，浏览器能解析这个标签

#### 1.2.1.2. `innerText`

获取或设置节点的文本内容

获取标签内容的时候，只会获取文本，标签扔掉了
设置标签内容的时候，覆盖原来内容，对标签进行转义（目的：把标签直接当文本来用）

兼容性

1. `innerText`是IE提出来的属性，因此低版本的火狐浏览器不支持这个属性。
2. 火狐有一个`textContent`属性，效果跟`innerText`一样，但是IE678不支持这个属性

innerText的兼容性代码:

```JavaScript
function getInnerText(element){
  if(typeof element.innerText === "string"){
    return element.innerText;
  } else {
    return element.textContent;
  }
}
```

#### 1.2.1.3. 区别

- 共同点 : 都是用来获取和设置标签的内容的
- 区别 :
  - `innerHTML`可以用于获取和设置标签的所有内容，包括标签和文本内容
  - `innerText`只识别文本，标签会被转义。（可以防止xss攻击）

### 1.2.2. 节点的属性

#### 1.2.2.1. `nodeName`

#### 1.2.2.2. `nodeValue`

## 1.3. 获取元素的方法

文档节点(document)、元素节点可以通过`getElementById`、`getElementsByName`、`getElementsByClassName`以及`getElementsByTagName`方法获取元素节点。

### 1.3.1. `getElementById()`

获取指定ID的元素

**参数**：

①id {string} ：元素ID。

**返回值**：

{HtmlElement} 元素节点对象。若没有找到，返回null。

**示例**：

```JavaScript
document.getElementById()
//功能：通过id 获取元素
document : 文档对象
get : 得到  
element:元素
by:通过
id:id值
// 参数 : 字符串类型的id
//返回值 : 一个元素 一个对象
var div = document.getElementById('div');
console.dir(div);
```

**注意**：

① HTML元素ID是区分大小写的。

② 若没有找到指定ID的元素，返回null。

③ 若一个父节点下面有多个相同ID元素时，默认选取第一个(而不是层级最高的)。

### 1.3.2. `getElementByTagName()`

获取指定标签的元素。

**参数**：

① name {string} ：name名称。

**返回值**：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。

**示例**：

```JavaScript
var ps = document.getElementsByTagName('p');
```

**注意**：

① `getElementsByTagName()`方法返回元素的顺序是它们在文档中的顺序。

② 返回值有没有获取到元素，都是一个伪数组，即便元素只有一个。

③ 传递给`getElementsByTagName()`方法的字符串可以不区分大小写。

④ 如果把特殊字符串 "*" 传递给`getElementsByTagName()`方法，它将返回文档中所有元素的列表，元素排列的顺序就是它们在文档中的顺序。

### 1.3.3. `getElementsByClassName()`

获取所有指定类名的元素。

**参数**：

① className {string} ：class名称。

**返回值**：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。

**示例**：

```JavaScript
var show = document.getElementsByClassName('show'); // 返回一个class包含show的元素数组
```

**注意**：

① `getElementsByClassName( )`方法在几个重要的浏览器中支持的最低版本
谷歌 |IE |火狐
---|---|---
4.0|9.0|3.0

### 1.3.4. `getElementsByTagName()`

通过标签名获取元素。

**参数**：

① elementName {string} ：标签名称。如：div、a等等

**返回值**：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。

**示例**：

```JavaScript
document.getElementsByTagName('div'); // 返回一个标签为div的元素数组
```

**注意**：

① 返回值有没有获取到元素，都是一个伪数组，即便元素只有一个