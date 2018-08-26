![大纲](imgs/1.png)

# 文档对象类型(DOM)

> DOM ( Document Object Model ) 文档对象模型,  是`W3C组织`推荐的一套操作网页元素的API。

DOM又称为文档树模型,v 因为整个HTML文档是一个树形的结构

**代码:**

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

## 节点(node)

### 元素节点

DOM的原子是元素节点(element node)

### 文本节点(Text)

每个XML、HTML元素内的文本

### 属性节点(Arrt)

## 1 获取元素

有三种DOM方法可获取元素节点，分别是通过元素ID、通过标签名字和通过类名字来获取。

### 1.1 getElementById()

获取指定ID的元素

##### 参数：

①id {string} ：元素ID。

##### 返回值：

{HtmlElement} 元素节点对象。若没有找到，返回null。

##### 注意：

① HTML元素ID是区分大小写的。

② 若没有找到指定ID的元素，返回null。

③ 若一个父节点下面有多个相同ID元素时，默认选取第一个(而不是层级最高的)。

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

#### 使用getElementById的注意事项

- 如果id不存在,返回值为null
- 在DOM中, `document.getElementById('box')` 方法需要写在html内容的后面, 保证页面加载完成之后才能获取到内容  (div标签就是)
- `Id` 不能写成 `ID`, 记得这是一个驼峰命名 : `document.getElementById`

### 1.2 getElementByTagName()

返回一个包含指定name名称的的元素数组

##### 参数：

① name {string} ：name名称。

##### 返回值：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。

```JavaScript
//参数：标签名
//返回值：一个伪数组， 伪数组不是数组，不能使用属性的方法，但是可以跟数组一样进行遍历和使用下标进行操作。
var ps = document.getElementsByTagName('p');
```

**注意：返回值有没有获取到元素，都是一个伪数组，即便元素只有一个**

## 1.3 getElementsByClassName()

##### 参数：

① className {string} ：class名称。

##### 返回值：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。

## getElementsByTagName()

##### 参数：

① elementName {string} ：标签名称。如：div、a等等

##### 返回值：

{Array} 符合条件的元素数组。若没有找到符合条件的，返回空数组。