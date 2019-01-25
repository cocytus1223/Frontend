<!-- TOC -->

- [1. JQuery](#1-jquery)
  - [1.1. 基本概念](#11-基本概念)
  - [1.2. 选择器](#12-选择器)
    - [1.2.1. 什么是 jQuery 选择器](#121-什么是-jquery-选择器)
    - [1.2.2. css 选择器](#122-css-选择器)
    - [1.2.3. 过滤选择器](#123-过滤选择器)
    - [1.2.4. 筛选选择器(方法)](#124-筛选选择器方法)
  - [1.3. CSS 操作](#13-css-操作)
  - [1.4. DOM 操作](#14-dom-操作)
    - [创建节点](#创建节点)
    - [添加节点](#添加节点)
    - [删除节点](#删除节点)
  - [1.5. 属性操作](#15-属性操作)
    - [1.5.1. attr() 方法](#151-attr-方法)
    - [1.5.2. prop() 方法](#152-prop-方法)
    - [1.5.3. val() 方法](#153-val-方法)
    - [1.5.4. html() 方法](#154-html-方法)
    - [1.5.5. text()方法](#155-text方法)
  - [1.6. JQuery 事件](#16-jquery-事件)
  - [1.7. JQuery 动画](#17-jquery-动画)

<!-- /TOC -->

# 1. JQuery

## 1.1. 基本概念

## 1.2. 选择器

### 1.2.1. 什么是 jQuery 选择器

jQuery 选择器是 jQuery 为我们提供的一组方法，让我们更加方便的获取到页面中的元素。注意：jQuery 选择器返回的是 jQuery 对象。

jQuery 选择器有很多，基本兼容了 CSS1 到 CSS3 所有的选择器，并且 jQuery 还添加了很多更加复杂的选择器。【查看 jQuery 文档】

jQuery 选择器虽然很多，但是选择器之间可以相互替代，就是说获取一个元素，你会有很多种方法获取到。所以我们平时真正能用到的只是少数的最常用的选择器。

### 1.2.2. css 选择器

> jQuery 完全兼容 css 选择器

| 名称       | 用法               | 描述                                                           |
| ---------- | ------------------ | :------------------------------------------------------------- |
| ID 选择器  | $(“#id”);          | 获取指定 ID 的元素                                             |
| 类选择器   | $(“.class”);       | 获取同一类 class 的元素                                        |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素                                       |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。                           |
| 交集选择器 | $(“div.redClass”); | 获取 class 为 redClass 的 div 元素                             |
| 子代选择器 | $(“ul>li”);        | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素    |
| 后代选择器 | $(“ul li”);        | 使用空格，代表后代选择器，获取 ul 下的所有 li 元素，包括孙子等 |

> 跟 CSS 的选择器一模一样。

### 1.2.3. 过滤选择器

> 这类选择器都带冒号:

| 名称         | 用法                                     | 描述                                                                |
| ------------ | ---------------------------------------- | :------------------------------------------------------------------ |
| :eq（index） | $(“li:eq(2)”).css(“color”, ”red”);       | 获取到的 li 元素中，选择索引号为 2 的元素，索引号 index 从 0 开始。 |
| :odd         | $(“li:odd”).css(“color”, ”red”);         | 获取到的 li 元素中，选择索引号为奇数的元素                          |
| :even        | $(“li:even”).css(“color”, ”red”);        | 获取到的 li 元素中，选择索引号为偶数的元素                          |
| :first       | $(“li:first”).css(“color”, ”red”);       | 获取到的 li 元素中的第一个                                          |
| :last        | $(“li:last”).css(“color”, ”red”);        | 获取到的 li 元素中的最后一个                                        |
| :gt(index)   | $(“li:gt(2)”).css(“color”, ”red”);       | 匹配所有大于给定索引值的元素                                        |
| :lt(index)   | $(“li:lt(2)”).css(“color”, ”red”);       | 匹配所有小于给定索引值的元素                                        |
| :header      | $(“li:header(2)”).css(“color”, ”red”);   | 匹配如 h1, h2, h3 之类的标题元素                                    |
| :animated    | $(“li:animated(2)”).css(“color”, ”red”); | 匹配所有正在执行动画效果的元素                                      |

### 1.2.4. 筛选选择器(方法)

> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，`筛选选择器`主要是方法。

| 名称               | 用法                        | 描述                                  |
| ------------------ | --------------------------- | :------------------------------------ |
| children(selector) | $(“ul”).children(“li”)      | 获取当前元素的所有子元素中的 li 元素  |
| find(selector)     | $(“ul”).find(“li”);         | 获取当前元素中的后代元素中的 li 元素  |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。        |
| parent()           | $(“#first”).parent();       | 查找父亲                              |
| eq(index)          | $(“li”).eq(2);              | 相当于`$(“li:eq(2)”)`,index 从 0 开始 |
| next()             | $(“li”).next()              | 找下一个兄弟                          |
| prev()             | $(“li”).prev()              | 找上一次兄弟                          |

## 1.3. CSS 操作

## 1.4. DOM 操作

### 创建节点

### 添加节点

### 删除节点

## 1.5. 属性操作

### 1.5.1. attr() 方法

1. 设置单个属性

   ```javascript
   //第一个参数：需要设置的属性名
   //第二个参数：对应的属性值
   attr(name, value);
   //用法举例
   $(“img”).attr(“title”,”哎哟，不错哦”);
   $(“img”).attr(“alt”,“哎哟，不错哦”);
   ```

2. 设置多个属性

   ```javascript
   //参数是一个对象，包含了需要设置的属性名和属性值
   attr(obj);
   //用法举例
   $("img").attr({
     title: "哎哟，不错哦",
     alt: "哎哟，不错哦",
     style: "opacity:.5"
   });
   ```

3. 获取属性

   ```javascript
   //传需要获取的属性名称，返回对应的属性值
   attr(name);
   //用法举例
   var oTitle = $("img").attr("title");
   alert(oTitle);
   ```

4. 移除属性

   ```javascript
   //参数：需要移除的属性名，
   removeAttr(name);
   //用法举例
   $("img").removeAttr("title");
   ```

### 1.5.2. prop() 方法

> 在 jQuery1.6 之后，对于 checked、selected、disabled 这类 boolean 类型的属性来说，不能用 attr 方法，只能用 prop 方法。

```javascript
//返回属性的值：
$(“:checked”).prop(“checked”)

//设置属性和值：
$(“:checked”).prop(“checked”,true)

//使用函数设置属性和值：
$(“:checked”).prop(“checked”,function(index,currentvalue))

//设置多个属性和值：
$(“:checked”).prop({checked:true, selected:true,...})

//移除属性
$(“:checked”).removeProp(“checked”)
```

### 1.5.3. val() 方法

val() 方法返回或设置被选元素的值。

元素的值是通过 value 属性设置的。该方法大多用于 `input` 元素。

如果该方法未设置参数，则返回被选元素的当前值。

```JavaScript
//设置属性和值
$(selector).val(value)

//获取属性
$(selector).val()
```

### 1.5.4. html() 方法

html() 方法返回或设置被选元素的内容 (inner HTML)。

```JavaScript
//设置属性和值
$(selector).html(content)

//获取属性
$(selector).html()

//使用函数来设置元素内容
$(selector).html(function(index,oldcontent))
```

### 1.5.5. text()方法

text() 方法设置或返回被选元素的文本内容。

```JavaScript
//返回文本内容：
$(selector).text()

//设置文本内容：
$(selector).text(content)

//使用函数设置文本内容：
$(selector).text(function(index,currentcontent))
```

## 1.6. JQuery 事件

## 1.7. JQuery 动画
