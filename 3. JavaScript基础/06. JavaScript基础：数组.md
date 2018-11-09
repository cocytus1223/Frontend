# 1. Array 对象

<!-- TOC -->

- [1. Array 对象](#1-array-对象)
  - [1.1. Array 对象属性](#11-array-对象属性)
  - [1.2. Array 对象方法](#12-array-对象方法)
    - [1.2.1. `push()`:把元素添加到数组尾部](#121-push把元素添加到数组尾部)
    - [1.2.2. `pop()`:移除并返回数组的最后一个元素](#122-pop移除并返回数组的最后一个元素)
    - [1.2.3. `shift()`：移除并返回数组的第一个元素](#123-shift移除并返回数组的第一个元素)
    - [1.2.4. `unshift()`：在数组头部插入元素](#124-unshift在数组头部插入元素)
    - [1.2.5. `join()`：将数组中所有元素通过一个分隔符拼接为一个字符串](#125-join将数组中所有元素通过一个分隔符拼接为一个字符串)
    - [1.2.6. `reverse()`：反转数组元素的顺序](#126-reverse反转数组元素的顺序)
    - [1.2.7. `sort()`：按一定的规则进行排序](#127-sort按一定的规则进行排序)
    - [1.2.8. `concat()`：把元素衔接到数组中。不会修改原先的 array,返回新的数组](#128-concat把元素衔接到数组中不会修改原先的-array返回新的数组)
    - [1.2.9. `slice()`：返回数组的一部分](#129-slice返回数组的一部分)
    - [1.2.10. `splice()`：插入、删除数组元素](#1210-splice插入删除数组元素)
    - [1.2.11. `indexOf()` ：在数组中查找匹配元素。](#1211-indexof-在数组中查找匹配元素)
    - [1.2.12. `lastIndexOf()` ：在数组中反向查找匹配元素。](#1212-lastindexof-在数组中反向查找匹配元素)
    - [1.2.13. `Array.isArray()` ：判断对象是否为数组](#1213-arrayisarray-判断对象是否为数组)
  - [1.3. 遍历数组的 5 种方法](#13-遍历数组的-5-种方法)
    - [1.3.1. `forEach()` ：依次遍历元素，执行指定的函数；无返回值](#131-foreach-依次遍历元素执行指定的函数无返回值)
    - [1.3.2. `filter()` ：依次遍历元素，返回包含符合条件元素的新的数组](#132-filter-依次遍历元素返回包含符合条件元素的新的数组)
    - [1.3.3. `map()` ：依次遍历元素，返回包含符合条件元素的新的数组](#133-map-依次遍历元素返回包含符合条件元素的新的数组)
    - [1.3.4. `some()`：依次遍历元素，判断是否有元素为 true](#134-some依次遍历元素判断是否有元素为-true)
    - [1.3.5. `every()`：依次遍历元素，判断每个元素是否都为 true](#135-every依次遍历元素判断每个元素是否都为-true)

<!-- /TOC -->

数组是值的有序集合。每个值叫做一个元素，而每个元素在数组中有一个位置，以数字表示，称为索引。JavaScript 数组是无类型：数组元素可以是任意类型，并且同一个数组中的不同元素也可能有不同的类型。

## 1.1. Array 对象属性

| 属性        | 描述                               |
| ----------- | ---------------------------------- |
| constructor | 返回对创建此对象的数组函数的引用。 |
| length      | 设置或返回数组中元素的数目。       |
| prototype   | 使您有能力向对象添加属性和方法。   |

## 1.2. Array 对象方法

### 1.2.1. `push()`:把元素添加到数组尾部

**参数**：

任意多个值添加到数组尾部

**返回值**：

新的数组的长度

**示例**：

```JavaScript
    var arr = [1, 2, 3, 4];
    console.log(arr.push(5, 6));        //6
    console.log(arr);                   //[1, 2, 3, 4, 5, 6]
```

### 1.2.2. `pop()`:移除并返回数组的最后一个元素

**参数**：

无

**返回值**：

数组的最后一个元素；若数组为空，返回 undefined

**示例**：

```JavaScript
    var arr = [1, 2, 3, 4];
    console.log(arr.pop());         //4
    console.log(arr);               //[1, 2, 3]

    var arr1 = ['a','b','c'];
    console.log(arr1.pop());//c
    console.log(arr1);//["a", "b"]
```

### 1.2.3. `shift()`：移除并返回数组的第一个元素

**参数**：

无

**返回值**：

数组的第一个元素；若数组为空，返回 undefined。

**示例**：

```JavaScript
    var arr = [1, 2, 3, 4];
    arr.shift();
    console.log(arr);           //[2, 3, 4]

    var arr = ['a', 'b', 'c'];
    arr.shift();
    console.log（arr);          //["b", "c"]
    arr.shift();
    console.log（arr);          //["c"]
    arr.shift();
    console.log（arr);          //[]
```

### 1.2.4. `unshift()`：在数组头部插入元素

**参数**：

任意多个值添加到数组头部

**返回值**：

数组新的长度

**示例**：

```JavaScript
    var arr = [];
    arr.unshift('a');
    console.log(arr);                       //["a"]
    console.log(arr.unshift());             //1
    arr.unshift('b');
    console.log(arr);                       //["b", "a"]
    console.log(arr.unshift());             //2
    arr.unshift('c');
    console.log(arr);                       //["c", "b", "a"]
    console.log(arr.unshift());             //3
```

### 1.2.5. `join()`：将数组中所有元素通过一个分隔符拼接为一个字符串

**参数**：

各元素之间的分隔符，如果省略，默认以因为英文逗号','分隔。

**返回值**：

各元素以 sparator 为分隔符，拼接而成的一个字符串。

**示例**：

```JavaScript
    var arr = ['a', 'b', 'c', 'd'];
    var str = arr.join('|');
    console.log(str);                  //a|b|c|d
```

### 1.2.6. `reverse()`：反转数组元素的顺序

**参数**：

无

**返回值**：

无(在原数组内进行元素顺序反转)。

**示例**：

```JavaScript
  var arr = [1, 2, 3, 4, 5];
  arr.reverse();
  console.log(arr);             //[5, 4, 3, 2, 1]
```

### 1.2.7. `sort()`：按一定的规则进行排序

**参数**：

可选的排序规则函数。若省略，将按照元素的字母进行从小到大排序。

a ：遍历时前面的元素。

b ：遍历时后面的元素。

**排序规则**：

比较 a 和 b，返回一个数字来表示 a 和 b 的排序规则：

小于 0 ：a 小于 b，a 排在 b 的前面。

等于 0 ：a 等于 b，a 排在 b 的前面。

大于 0 ：a 大于 b，a 排在 b 的后面。

**返回值**：

无(在原先数组里进行排序操作)。

**示例**：

```JavaScript
    var arr2 = ['a', 'b', 'z', 'c', 'e', 8, 9];
    arr2.sort();
    console.log(arr2);                          //默认是以ascii码来排列的，[8, 9, "a", "b", "c", "e", "z"]

    var arr3 = [2, 5, 6, 7, 10, 1, 4];
    arr3.sort(function (a, b) {
    return a - b;
    })
    console.log(arr3);                          //[1, 2, 4, 5, 6, 7, 10]

    arr3.sort(function (a, b) {
    return b - a;
    })
    console.log(arr3);                          //[10, 7, 6, 5, 4, 2, 1]
```

### 1.2.8. `concat()`：把元素衔接到数组中。不会修改原先的 array,返回新的数组

**参数**：

任意多个值

**返回值**：

一个新的数组，包含原先的 Array 和新加入的元素。

**示例**：

```JavaScript
    var a = [1, 2];
    var b = [3, 4];
    var newArr = a.concat(b);
    console.log(newArr);        //[1, 2, 3, 4]
```

### 1.2.9. `slice()`：返回数组的一部分

**参数**：

①startIndex ：开始处的序号；若为负数，表示从尾部开始计算，-1 代表最后一个元素，-2 倒数第二个，依此类推。

②endIndex ： 结束处的元素后一个序号，没指定就是结尾。截取的元素不包含此处序号的元素，结尾为此处序号的前一个元素。

**返回值**：

一个新的数组，包含从 startIndex 到 endIndex 前一个元素的所有元素。

**示例**：

当 slice 没有传递参数时，直接复制数组

```JavaScript
    var arr = [1, 2, 3, 4, 5];
    var newArr1 = arr.slice();
    console.log(newArr1);       //[1, 2, 3, 4, 5]
```

当 slice 值传递一个值的时候 从传递的那个下标开始 一直到最后 包括最后

```JavaScript
    var arr = [1, 2, 3, 4, 5];
    var newArr2 = arr.slice(2);
    console.log(newArr2);       //[3, 4, 5]
```

当 slice 值传递两个值 一个代表开始截取的下标 一个代表结束的下标（不包括结束的那个）

```JavaScript
    var arr = [1, 2, 3, 4, 5];
    var newArr3 = arr.slice(2, 4);
    console.log(newArr3);       //[3, 4]
```

### 1.2.10. `splice()`：插入、删除数组元素

**参数**：

①index ：开始插入、删除或替换的起始序号。

②len ：要删除元素的个数，从 start 处开始计算。

③item ：可选参数，表示要插入的元素，从 start 处开始插入。若 ② 参不为 0，那么先执行删除操作，再执行插入操作。

**返回值**：

返回一个包含删除元素的新的数组。若 ② 参为 0，表示没元素删除，返回一个空数组。

**示例**：

```JavaScript
arr = ['a','b','c','d']
删除 ----  item不设置
arr.splice(1,1)   //['a','c','d']     删除起始下标为1，长度为1的一个值，len设置的1，如果为0，则数组不变
arr.splice(1,2)  //['a','d']          删除起始下标为1，长度为2的一个值，len设置的2

替换 ---- item为替换的值
arr.splice(1,1,'ttt')        //['a','ttt','c','d']      替换起始下标为1，长度为1的一个值为‘ttt’，len设置的1
arr.splice(1,2,'ttt')        //['a','ttt','d']         替换起始下标为1，长度为2的两个值为‘ttt’，len设置的1

添加 ----  len设置为0，item为添加的值
arr.splice(1,0,'ttt')        //['a','ttt','b','c','d']         表示在下标为1处添加一项‘ttt’
```

### 1.2.11. `indexOf()` ：在数组中查找匹配元素。

若不存在匹配的元素时，就返回-1。查找的时候使用"==="运算符，所以要区分 1 和'1'

**参数**：

①value ：要在数组中查找的值。

②start ：开始查找的序号位置，如果省略，则为 0.

**返回值**：

返回数组中第一个匹配 value 的序号，若不存在，返回-1。

**示例**：

```JavaScript
['a', 'b', 'c'].indexOf('a'); // 0
['a', 'b', 'c'].indexOf('a', 1); // -1
['a', 'b', 'c'].indexOf('d'); // -1
[1, 2, 3].indexOf('1'); //  -1 ：采用的'==='匹配方式
```

### 1.2.12. `lastIndexOf()` ：在数组中反向查找匹配元素。

若不存在匹配的元素时，就返回-1。查找的时候使用"==="运算符，所以要区分 1 和'1'

**参数**：

①value ：要在数组中查找的值。

②start ：开始查找的序号位置，如果省略，则从最后一个元素开始查找。

**返回值**：

从右到左开始查找数组中第一个匹配 value 的序号，若不存在，返回-1

**示例**：

```JavaScript
['a', 'b', 'c'].lastIndexOf('a'); //  0
['a', 'b', 'c'].lastIndexOf('a', 1); //  0
['a', 'b', 'c'].lastIndexOf('d'); //  -1
[1, 2, 3].lastIndexOf('1'); // => -1 ：采用的'==='匹配方式
```

### 1.2.13. `Array.isArray()` ：判断对象是否为数组

**参数**：

任意对象

**返回值**：

返回判断结果。当为 true 时，表示对象为数组；为 false 时，表示对象不是数组

**示例**：

```JavaScript
Array.isArray([]); // => true
Array.isArray(['a', 'b', 'c']); // => true
Array.isArray('a'); // => false
Array.isArray('[1, 2, 3]'); // => false
```

## 1.3. 遍历数组的 5 种方法

### 1.3.1. `forEach()` ：依次遍历元素，执行指定的函数；无返回值

**参数**：

function(value,index,self){} ：每个元素依次调用此函数

value ：数组遍历的元素

index ：元素序号

self ：Array 本身

**返回值**：

无

**示例**：

```JavaScript
var demoArray = [1, 2, 3];
demoArray.forEach(function (value, index, self) {
    console.log(value); // => 依次输出：1  2  3
});
```

### 1.3.2. `filter()` ：依次遍历元素，返回包含符合条件元素的新的数组

**参数**：

function(value,index,self){} ：每个元素依次调用此函数，返回包含符合条件元素的新的数组。

value ：数组遍历的元素

index ：元素序号

self ：Array 本身

**返回值**：

一个包含符合条件元素的新的数组

**示例**：

```JavaScript
var demoArray = [1, 2, 3];
var rs = demoArray.filter(function (value, index, self) {
    return value > 0;
});
console.log(rs); // => [1, 2, 3]
```

### 1.3.3. `map()` ：依次遍历元素，返回包含符合条件元素的新的数组

**参数**：

function(value,index,self){} ：每个元素依次调用此函数，返回计算好的元素。

value ：数组遍历的元素

index ：元素序号

self ：Array 本身

**返回值**：

一个包含计算好的元素的新的数组

**示例**：

```JavaScript
[1, 2, 3].map(function (value, index, self) {
    return value * 2;
}); // => [2, 4, 6]
```

### 1.3.4. `some()`：依次遍历元素，判断是否有元素为 true

**参数**：

value ：数组遍历的元素

index ：元素序号

self ：Array 本身

**返回值**：

布尔值。如果数组中有元素满足条件返回 true，否则返回 false。

**示例**：

```JavaScript
var demoarr = [1, 2, 3];
var re = demoarr.some(function (value, index, self){
return value >6;
})
console.log(re);// false
```

### 1.3.5. `every()`：依次遍历元素，判断每个元素是否都为 true

**参数**：
function(value,index,self){} ：每个元素都会使用此函数判断是否为 true，当判断到一个为 false 时，立即结束遍历。

value ：数组遍历的元素

index ：元素序号

self ：Array 本身

**返回值**：
只有每个元素都为 true 才返回 true；只要一个为 false，就返回 false。

**示例**：

```JavaScript
var demoArray = [1, 2, 3];
var rs = demoArray.every(function (value, index, self) {
    return value > 0;
});
console.log(rs); // => true
```
