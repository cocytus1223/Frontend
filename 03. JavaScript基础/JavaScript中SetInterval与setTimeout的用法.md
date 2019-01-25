# 1. JavaScript中`SetInterval()`与`setTimeout()`的用法

## 1.1. `setInterval()`

**语法** ：
setInterval(code,interval)

**参数** ：
① code：必须。要调用的函数或要执行的代码串。
② interval：必须。周期的时间跨度，以毫秒计。

**返回值** ：
定时器的id,  用于清除

**示例** ：

```JavaScript
var timer = setInterval(function(){
  //重复执行的代码
},1000);
```

## 1.2. `setTimeout()`

**语法** ：
setTimeout(code,millisec)

**参数** ：
① code：必须。要调用的函数或要执行的 JavaScript 代码串。
② millisec：必须。在执行代码前需等待的毫秒数。

**返回值** ：
定时器的id,用于清除

**示例** ：

```JavaScript
var timer = setTimeOut(function(){
//1秒后将执行的代码。
}, 1000);
```

## 1.3. JavaScript的堆栈调用

```JavaScript
function a() {
    setTimeout(function() {alert(1)}, 0);
    alert(2);
}
a();//执行结果：先弹出2，然后在弹出1
```

　　首先，JavaScript是单线程的，即同一时间只执行一条代码，所以每一个JavaScript代码执行块会“阻塞”其它异步事件的执行。
　　其次，和其他的编程语言一样，Javascript中的函数调用也是通过堆栈实现的。在执行函数a的时候，a先入栈，如果不给alert(1)加setTimeout，那么alert(1)第2个入栈，最后是alert(2)。但现在给alert(1)加上setTimeout后，alert(1)就被加入到了一个新的堆栈中等待，并“尽可能快”的执行。这个尽可能快就是指在a的堆栈完成后就立刻执行，
　　因此实际的执行结果就是先alert(2)，再alert(1)。在这里setTimeout实际上是让alert(1)脱离了当前函数调用堆栈。