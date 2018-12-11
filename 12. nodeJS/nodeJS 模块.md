# NodeJS 模块

## global 全局模块

浏览器 JavaScript 当中 `window` 是全局对象，**NodeJS 中全局对象是 global**，`global` 最根本的作用是作为全局变量的宿主（即所有的全局变量都是 `global` 对象的属性），因此在所有模块中都可以直接使用而无需包含。

NodeJS 中不可能在代码最外层定义全局变量，因为所有自定义代码都是属于当前模块的，而模块本身不是 NodeJS 最外层的上下文。

> 尽量显式的使用 let、const 关键字声明变量，避免直接声明将变量引入全局，污染命名空间，提高耦合风险。

- `global`：全局变量的宿主。
- `Class: Buffer`：用来与 TCP 数据流、文件系统操作等八位二进制流进行交互的类型。
- `__filename`：表示当前正在执行的脚本的**文件名**。
- `__dirname`：表示当前执行脚本所在的**目录**。

- `console`： debug 信息打印控制台。
- `require()`：获取 NodeJS 模块。
- `exports()`：导出 NodeJS 模块，该方法是引用了 module.exports 的快捷类型。
- `module`：当前 NodeJS 模块的引用。
- `process`：用于描述当前 NodeJS 进程状态的对象。

- `setImmediate(callback[, ...args])` / `clearImmediate(immediateObject)`：将一些需要长时间运行的操作放在回调函数内，在浏览器完成后面的其他语句后，立刻执行该回调函数。
- `setInterval(callback, delay[, ...args])` / `clearInterval(intervalObject)` ：在指定的毫秒数后重复执行指定回调函数，除非显示调用 clearInterval 关闭。
- `setTimeout(callback, delay[, ...args])` / `clearTimeout(timeoutObject)`：在指定的毫秒数后执行一次指定的回调函数。

## fs 文件模块

fs 模块封装了文件操作，提供了文件读取、写入、更名、删除、遍历、链接等 POSIX 文件系统操作，该模块中所有操作都提供了异步和同步 2 个版本。

fs 不是全局模块，不能直接使用，需要先导入 fs 模块，再使用。

```JavaScript
// 引入模块
const fs = require('fs');
```

### 读取文件

> fs.readFile(path,[encoding],[callback(err,data)])

**参数**：

- path 表示要读取的文件名或文件描述符
- encoding 表示文件的字符编码
- callback 是回调函数，用于接收文件内容
  - err：错误
  - data：文件内容。如果指定 encoding，data 将是 1 个解析后的字符串，否则 data 将会是以 `Buffer` 形式表示的二进制数据。

**示例**：

```JavaScript
fs.readFile('./data.txt', 'utf-8', (err, data) => {
    if (err) {
       return console.log('读取失败', err);
    }
    console.log(data);    //输出的是字符串
})
```

### 写入文件

> fs.writeFile(file, data, [encoding], [callback(err,data)])

注：写入文件，如果文件已存在，则覆盖文件。

**参数**：

- file 表示要写入的文件名或文件描述符
- data 内容
- encoding 表示文件的字符编码

**示例**：

```JavaScript
fs.writeFile('./data1.txt', '菊花残，满地伤', (err) => {
    if (err) {
        return console.log('写入失败');
    }
    console.log('写入成功');
});
```

## path 模块

```JavaScript
// 1. 引入path模块
const path = require('path');

path.join(__dirname, 'data.txt');
path.basename(path[, ext])  // 返回文件名的最后一部分
path.dirname(path)  // 返回路径的目录名
path.extname(path)  // 获取路径的扩展名
```

## mine 模块

获取对应文件的 mime 类型 ，设置 content-type

```JavaScript
// 1. 下载
// npm i mime
// 2. 引入
const mime = require('mime');
// 3. 使用api
//获取文件的mime类型
// mime.getType(文件名);
console.log(mime.getType('aa.html'));
console.log(mime.getType('aa.css'));
console.log(mime.getType('aa.jpg'));
console.log(mime.getType('aa.png'));
console.log(mime.getType('aa.avi'));
console.log(mime.getType('aa.mp3'));

// text/html
// text/css
// image/jpeg
// image/png
// video/x-msvideo
// audio/mpeg
// 根据mime类型获取 拓展名
console.log(mime.getExtension('text/html'));
console.log(mime.getExtension('text/css'));
console.log(mime.getExtension('audio/mpeg'));
```

## http 模块
