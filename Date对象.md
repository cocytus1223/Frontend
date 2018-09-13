# 1. Date 对象

目录

<!-- TOC -->

- [1. Date 对象](#1-date-对象)
  - [1.1. Date 对象属性](#11-date-对象属性)
  - [1.2. 构造函数](#12-构造函数)
    - [1.2.1. `new Date()` ：返回当前的本地日期和时间](#121-new-date-返回当前的本地日期和时间)
    - [1.2.2. `new Date(milliseconds)` ：把毫秒数转换为 `Date` 对象](#122-new-datemilliseconds-把毫秒数转换为-date-对象)
    - [1.2.3. `new Date(dateStr)`：把字符串转换为 `Date` 对象](#123-new-datedatestr把字符串转换为-date-对象)
    - [1.2.4. `new Date(year, month, opt_day, opt_hours, opt_minutes, opt_seconds, opt_milliseconds)` ：把年月日、时分秒转换为 `Date` 对象](#124-new-dateyear-month-opt_day-opt_hours-opt_minutes-opt_seconds-opt_milliseconds-把年月日时分秒转换为-date-对象)
  - [1.3. `Date` 对象方法](#13-date-对象方法)
    - [1.3.1. `get` 方法](#131-get-方法)
    - [1.3.2. `set` 方法](#132-set-方法)
    - [1.3.3. 转换方法](#133-转换方法)
    - [1.3.4. 静态方法](#134-静态方法)
      - [1.3.4.1. `Date.now()`](#1341-datenow)
      - [1.3.4.2. `Date.parse(dateStr)`](#1342-dateparsedatestr)
  - [1.4. 时间戳](#14-时间戳)

<!-- /TOC -->

## 1.1. Date 对象属性

| 属性        | 描述                                 |
| ----------- | ------------------------------------ |
| constructor | 返回对创建此对象的 Date 函数的引用。 |
| prototype   | 使您有能力向对象添加属性和方法。     |

## 1.2. 构造函数

### 1.2.1. `new Date()` ：返回当前的本地日期和时间

**参数**：无

**返回值**：返回一个表示本地日期和时间的 `Date` 对象。

**示例**：

```JavaScript
var dt = new Date();
console.log(dt); // => Wed Sep 12 2018 15:53:21 GMT+0800 (中国标准时间)
```

### 1.2.2. `new Date(milliseconds)` ：把毫秒数转换为 `Date` 对象

**参数**：

毫秒数；表示从'1970/01/01 00:00:00'为起点，开始叠加的毫秒数。

**注意**：起点的时分秒还要加上当前所在的时区，北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00'

**返回值**：返回一个叠加后的 `Date` 对象。

**示例**：

```JavaScript
var dt = new Date(1000 _ 60 _ 1); // 前进 1 分钟的毫秒数
console.log(dt); // => {Date}:1970/01/01 08:01:00
dt = new Date(-1000 _ 60 _ 1); // 倒退 1 分钟的毫秒数
console.log(dt); // => {Date}:1970/01/01 07:59:00
```

### 1.2.3. `new Date(dateStr)`：把字符串转换为 `Date` 对象

**参数**：

可转换为 `Date` 对象的字符串(可省略时间)；字符串的格式主要有两种：

1. yyyy/MM/dd HH:mm:ss （推荐）：若省略时间，返回的 Date 对象的时间为 00:00:00。

2. yyyy-MM-dd HH:mm:ss ：若省略时间，返回的 Date 对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在 IE 中会转换失败!

**返回值**：返回一个转换后的 `Date` 对象。

**示例**：

```JavaScript
var dt = new Date('2014/12/25'); // yyyy/MM/dd
console.log(dt); // => {Date}:2014/12/25 00:00:00
dt = new Date('2014/12/25 12:00:00'); // yyyy/MM/dd HH:mm:ss
console.log(dt); // => {Date}:2014/12/25 12:00:00

dt = new Date('2014-12-25'); // yyyy-MM-dd
console.log(dt); // => {Date}:2014-12-25 08:00:00 (加上了东 8 区的时区)
dt = new Date('2014-12-25 12:00:00'); // yyyy-MM-dd HH:mm:ss (注意：此转换方式在 IE 中会报错！)
console.log(dt); // => {Date}:2014-12-25 12:00:00
```

### 1.2.4. `new Date(year, month, opt_day, opt_hours, opt_minutes, opt_seconds, opt_milliseconds)` ：把年月日、时分秒转换为 `Date` 对象

**参数**：

①year {int} ：年份；4 位数字。如：1999、2014

②month {int} ：月份；2 位数字。从 0 开始计算，0 表示 1 月份、11 表示 12 月份。

③opt_day {int} 可选：号； 2 位数字；从 1 开始计算，1 表示 1 号。

④opt_hours {int} 可选：时；2 位数字；取值 0~23。

⑤opt_minutes {int} 可选：分；2 位数字；取值 0~59。

⑥opt_seconds {int} 可选：秒；2 未数字；取值 0~59。

⑦opt_milliseconds {int} 可选：毫秒；取值 0~999。

**返回值**：返回一个转换后的 `Date` 对象。

**示例**：

```JavaScript
var dt = new Date(2014, 11); // 2014 年 12 月(这里输入的月份数字为 11)
console.log(dt); // => {Date}:2014/12/01 00:00:00
dt = new Date(2014, 11, 25); // 2014 年 12 月 25 日
console.log(dt); // => {Date}:2014/12/25 00:00:00
dt = new Date(2014, 11, 25, 15, 30, 40); // 2014 年 12 月 25 日 15 点 30 分 40 秒
console.log(dt); // => {Date}:2014/12/25 15:30:40
dt = new Date(2014, 12, 25); // 2014 年 13 月 25 日(这里输入的月份数字为 12，表示第 13 个月，跳转到第二年的 1 月)
console.log(dt); // => {Date}:2015/01/25
```

## 1.3. `Date` 对象方法

### 1.3.1. `get` 方法

1. `getFullYear()` ：返回 Date 对象的年份值；4 位年份。
2. `getMonth()` ：返回 Date 对象的月份值。从 0 开始，所以真实月份=返回值+1 。
3. `getDate()` ：返回 Date 对象的月份中的日期值；值的范围 1~31 。
4. `getHours()` ：返回 Date 对象的小时值。
5. `getMinutes()` ：返回 Date 对象的分钟值。
6. `getSeconds()` ：返回 Date 对象的秒数值。
7. `getMilliseconds()` ：返回 Date 对象的毫秒值。
8. `getDay()` ：返回 Date 对象的一周中的星期值；0 为星期天，1 为星期一、2 为星期二，依此类推。
9. `getTime()` ：返回 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00') 。

**示例**：

```JavaScript
dt.getFullYear(); // => 2014：年
dt.getMonth(); // => 11：月；实际为 12 月份(月份从 0 开始计算)
dt.getDate(); // => 6：日
dt.getHours(); // => 15：时
dt.getMinutes(); // => 30：分
dt.getSeconds(); // => 40：秒
dt.getMilliseconds(); // => 333：毫秒
dt.getDay(); // => 4：星期几的值
dt.getTime(); // =>1536210598387 ：返回 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00')
```

### 1.3.2. `set` 方法

1. `setFullYear(year, opt_month, opt_date)` ：设置 Date 对象的年份值；4 位年份。
2. `setMonth(month, opt_date)` ：设置 Date 对象的月份值。0 表示 1 月，11 表示 12 月。
3. `setDate(date)` ：设置 Date 对象的月份中的日期值；值的范围 1~31 。
4. `setHours(hour, opt_min, opt_sec, opt_msec)` ：设置 Date 对象的小时值。
5. `setMinutes(min, opt_sec, opt_msec)` ：设置 Date 对象的分钟值。
6. `setSeconds(sec, opt_msec)` ：设置 Date 对象的秒数值。
7. `setMilliseconds(msec)` ：设置 Date 对象的毫秒值。

**示例**：

```JavaScript
var dt = new Date();
dt.setFullYear(2018); // => 2018：年
dt.setMonth(8); // => 8：月；实际为 9 月份(月份从 0 开始计算)
dt.setDate(6); // => 25：日
dt.setHours(15); // => 13：时
dt.setMinutes(30); // => 12：分
dt.setSeconds(40); // => 40：秒
dt.setMilliseconds(333); // => 333：毫秒
console.log(dt); // => Thu Sep 06 2018 13:13:16 GMT+0800 (中国标准时间)
```

### 1.3.3. 转换方法

1. `toString()` ：将 Date 转换为一个'年月日 时分秒'字符串
2. `toLocaleString()` ：将 Date 转换为一个'年月日 时分秒'的本地格式字符串
3. `toDateString()` ：将 Date 转换为一个'年月日'字符串
4. `toLocaleDateString()` ：将 Date 转换为一个'年月日'的本地格式字符串
5. `toTimeString()` ：将 Date 转换为一个'时分秒'字符串
6. `toLocaleTimeString()` ：将 Date 转换为一个'时分秒'的本地格式字符串
7. `valueOf()` ：与 getTime()一样， 返回 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00')

**示例**：

```JavaScript
var dt = new Date();
console.log(dt.toString()); // =>Thu Sep 06 2018 13:28:26 GMT+0800 (中国标准时间) ：将 Date 转换为一个'年月日 时分秒'字符串
console.log(dt.toLocaleString()); // => 2018/9/6 下午1:27:36 ：将 Date 转换为一个'年月日 时分秒'的本地格式字符串

console.log(dt.toDateString()); // => Thu Sep 06 2018 ：将 Date 转换为一个'年月日'字符串
console.log(dt.toLocaleDateString()); // => 2018/9/6 ：将 Date 转换为一个'年月日'的本地格式字符串

console.log(dt.toTimeString()); // => 13:29:27 GMT+0800 (中国标准时间) ：将 Date 转换为一个'时分秒'字符串
console.log(dt.toLocaleTimeString()); // => 下午1:29:40 ：将 Date 转换为一个'时分秒'的本地格式字符串

console.log(dt.valueOf()); // => 1536211797279 返回 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00')
```

### 1.3.4. 静态方法

#### 1.3.4.1. `Date.now()`

**说明**：返回当前日期和时间的 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00')

**参数**：无

**返回值**：当前时间与起始时间之间的毫秒数。

**示例**：

```JavaScript
console.log(Date.now()); // => 1536211797279
```

#### 1.3.4.2. `Date.parse(dateStr)`

**说明**：把字符串转换为 Date 对象 ，然后返回此 Date 对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东 8 区，起点时间实际为：'1970/01/01 08:00:00')

**参数**：

可转换为 Date 对象的字符串(可省略时间)；字符串的格式主要有两种：

1. yyyy/MM/dd HH:mm:ss （推荐）：若省略时间，返回的 Date 对象的时间为 00:00:00。

2. yyyy-MM-dd HH:mm:ss ：若省略时间，返回的 Date 对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在 IE 中返回 NaN(非数字)!

**返回值**：返回转换后的 Date 对象与起始时间之间的毫秒数。

**示例**：

```JavaScript
console.log(Date.parse('2018/9/6 12:00:00')); // => 1536206400000
console.log(Date.parse('2018-9-6 12:00:00')); // => 1536206400000 (注意：此转换方式在 IE 中返回 NaN！)
```

## 1.4. 时间戳

1. 获取未来时间和当前时间，将这两个时间相减得到毫秒数，利用毫秒数/1000，换算成秒数。
2. 将秒数换算成天 时 分 秒
   公式：
   天： s / 86400
   时： s % 86400 / 3600
   分： s % 3600 / 60
   秒： s % 60

```JavaScript
时间戳：从 1970 年距今为止的毫秒数 后期用来防止缓存
var date = +new Date();
console.log(date);

// 获取未来时间
var future = new Date('2018-9-25 12:00:00');
var now = new Date();

console.log(future);
console.log(now);

// 时间 - 时间 = 两个时间之间的毫秒数
console.log(future - now);

// 将毫秒数转换成描述
var s = parseInt((future - now) / 1000)
console.log(s);

// 将秒数转换成 天 时 分 秒

var day = parseInt(s / 86400);
console.log(day);
var hours = parseInt(s % 86400 / 3600)
console.log(hours);
var minutes = parseInt(s % 3600 / 60)
console.log(minutes);
var seconds = s % 60;
console.log(seconds);

console.log('距离 2018-9-25 12:00:00 为止还有' + day + '天' + hours + '小时' + minutes + '分钟' + seconds + '秒');
```
