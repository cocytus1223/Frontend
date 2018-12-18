# Vue 指令

## 差值表达式

## v-bind

v-bind 用来**动态的绑定一个或者多个特性**。没有参数时，可以绑定到一个包含键值对的对象。常用于动态绑定 class 和 style。以及 href 等。

**缩写**：`：`

**用法**：

1. 对象语法

   ```html
   <div id="app">
     <!--
       当data里面定义的isActive等于true时，is-active这个类才会被添加起作用
     -->
     <!--
       当data里面定义的hasError等于true时，text-danger这个类才会被添加起作用
     -->
     <div :class="{'is-active':isActive, 'text-danger':hasError}"></div>
   </div>
   <script>
     const vm = new Vue({
       el: '#app',
       data: {
         isActive: true,
         hasError: false
       }
     })
   </script>
   ```

2. 数组语法

   ```html
   <div id="app">
     <!-- 数组语法：errorClass在data对应的类一定会添加 -->
     <!-- is-active是对象语法，根据activeClass对应的取值决定是否添加 -->
     <p :class="[{'is-active':activeClass},errorClass]">12345</p>
   </div>
   <script>
     const vm = new Vue({
       el: '#app',
       data: {
         activeClass: false,
         errorClass: 'text-danger'
       }
     })
   </script>
   ```

3. 直接绑定数据对象

   ```html
   <div id="app">
     <!--
       在vue实例的data中定义了classObject对象，这个对象里面是所有类名及其真值
     -->
     <!-- 当里面的类的值是true时会被渲染 -->
     <div :class="classObject">12345</div>
   </div>
   <script>
     const vm = new Vue({
       el: '#app',
       data: {
         classObject: {
           'is-active': false,
           'text-danger': true
         }
       }
     })
   </script>
   ```

## v-model

这个指令用于在表单上创建**双向数据绑定**。
v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值。因为它选择 Vue 实例数据做为具体的值。

```html
<div id="app">
  <p>{{msg}}</p>
  <input type="text" v-model="msg" />

  <hr />
  <h3>textarea中使用</h3>
  <p>{{desc}}</p>
  <textarea cols="30" rows="10" v-model="desc"></textarea>

  <hr />
  <h3>select框</h3>
  <p>{{city}}</p>
  <select v-model="city">
    <option value="1">北京</option>
    <option value="2">上海</option>
    <option value="3">广州</option>
    <option value="4">深圳</option>
  </select>

  <hr />
  <h3>checkbox</h3>
  <p>{{isCheck}}</p>
  <input type="checkbox" v-model="isCheck" />
</div>

<script src="vue.js"></script>
<script>
  const vm = new Vue({
    el: '#app',
    data: {
      msg: 'hello vue',
      desc: '',
      city: 3,
      isCheck: true
    }
  })
</script>
```

**v-model 修饰符**：

1. `lazy`：默认情况下，v-model 同步输入框的值和数据。可以通过这个修饰符，转变为在 change 事件再同步。
2. `number`：自动将用户的输入值转化为数值类型
3. `trim`：自动过滤用户输入的首尾空格

## v-on

v-on 绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。

用在普通元素上时，只能监听原生 DOM 事件。用在自定义元素组件上时，也可以监听子组件触发的自定义事件。

**缩写**：`@`

```html
<!-- @click="事件的函数名字"  缺点：不能传递参数， 默认参数，事件对象 -->
<!--
  @click="事件函数名()   优点：可以在()中传递参数 缺点：没有默认的事件对象，手动传入$event"
-->
<div id="app"><button @click="consoleLog"></button></div>
<script>
  const vm = new Vue({
    el: '#app',
    methods: {
      consoleLog: function(event) {
        console.log(1)
      }
    }
  })
</script>
```

**事件修饰符**：

- `.stop` 调用 `event.stopPropagation()`。阻止事件继续传播
- `.prevent` 调用 `event.preventDefault()`。阻止默认行为
- `.capture` 使用事件捕获模式
- `.self` 只当在 event.target 是当前元素自身时触发处理函数
- `.once` 事件将只会触发一次
- `.passive` 告诉浏览器你不想阻止事件的默认行为
- `.left` - (2.2.0) 只当点击鼠标左键时触发。
- `.right` - (2.2.0) 只当点击鼠标右键时触发。
- `.middle` - (2.2.0) 只当点击鼠标中键时触发。

```html
<!-- 阻止单击事件继续传播 -->
<a @click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form @submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a @click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form @submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
<div @click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div @click.self="doThat">...</div>

<!-- 点击事件将只会触发一次 -->
<a @click.once="doThis"></a>

<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成 -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div @scroll.passive="onScroll">...</div>
```

**注意**：

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用`@click.prevent.self`会阻止所有的点击，而 `@click.self.prevent` 只会阻止对元素自身的点击。

**按键修饰符**：

在监听键盘事件时，我们经常需要检查常见的键值。Vue 允许为  `v-on`  在监听键盘事件时添加按键修饰符：

- `.enter`
- `.tab`
- `.delete` (捕获“删除”和“退格”键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

## v-text

v-text 主要用来更新`textContent`，可以等同于 JS 的 innerText 属性。

```html
<span v-text="msg"></span>
```

这两者等价：

```html
<span>{{msg}}</span>
```

## v-html

双大括号的方式会将数据解释为纯文本，而非 HTML。为了输出真正的 HTML，可以用 v-html 指令。它等同于 JS 的 innerHtml 属性。

```html
<div v-html="rawHtml"></div>
```

**注意**：

在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 XSS 攻击。只在可信内容上使用 v-html，永不用在用户提交的内容上。

## v-if

v-if 可以实现条件渲染，Vue 会根据表达式的值的真假条件来渲染元素。

```html
<a v-if="ok">yes</a>
```

如果属性值 ok 为 true，则显示。否则，不会渲染这个元素。

## v-show

```html
<h1 v-show="ok">hello world</h1>
```

也是用于根据条件展示元素。和 v-if 不同的是，如果 v-if 的值是 false，则这个元素被销毁，不在 dom 中。但是 v-show 的元素会始终被渲染并保存在 dom 中，它只是简单的切换 css 的 dispaly 属性。

**注意**：

- v-if 有更高的切换开销
- v-show 有更高的初始渲染开销。

因此，如果要非常频繁的切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则 v-if 较好。

## v-else

v-else 是搭配 v-if 使用的，它必须紧跟在 v-if 或者 v-else-if 后面，否则不起作用。

```html
<a v-if="ok">yes</a> <a v-else>No</a>
```

## v-else-if

v-else-if 充当 v-if 的 else-if 块，可以链式的使用多次。可以更加方便的实现 switch 语句。

```html
<div v-if="type==='A'">A</div>
<div v-if="type==='B'">B</div>
<div v-if="type==='C'">C</div>
<div v-else>Not A,B,C</div>
```

## v-for

用 v-for 指令根据遍历数组来进行渲染
有下面两种遍历形式

```html
<div v-for="(item,index) in items"></div>
<!-- 使用in，index是一个可选参数，表示当前项的索引 -->
<div v-for="item of items"></div>
<!-- 使用of -->
```

下面是一个例子，并且在 v-for 中，拥有对父作用域属性的完全访问权限。

```html
<ul id="app">
  <li v-for="item in items">{{parent}}-{{item.text}}</li>
</ul>
<script>
  var vm = new Vue({
    el:'#app',
    data:{
      parent:'父作用域'
      items:[
        {text:'文本1'},
        {text:'文本2'}
      ]
    }
  })
</script>
```

会被渲染为：

```html
<ul id="app">
  <li>父作用域-文本1</li>
  <li>父作用域-文本2</li>
</ul>
```

方式一：普通数组的遍历

```html
<li v-for="item in arr1">{{item}}</li>
<!-- 括号里如果写两个参数：第一个参数代表值，第二个参数代表index 索引 -->
<li v-for="(item,index) in arr1">值：{{item}} --- 索引：{{index}}</li>
<script>
  const vm = new Vue({
    el: '#app',
    data: {
      arr1: [2, 5, 3, 1, 1]
    }
  })
</script>
```

方式二：对象数组的遍历

```html
<div id="app">
  <ul>
    <!--
      对象数组的遍历。括号里如果写两个参数：第一个参数代表数组的单个item，第二个参数代表 index 索引
    -->
    <li v-for="(item, index) in dataList">
      姓名：{{item.name}} --- 年龄：{{item.age}} --- 索引：{{index}}
    </li>
  </ul>
</div>

<script>
  const vm = new Vue({
    el: '#app',
    data: {
      //对象数组
      dataList: [
        { name: 'smyh', age: '26' },
        { name: 'vae', age: '32' },
        { name: 'xiaoming', age: '20' }
      ]
    }
  })
</script>
```

方式三：对象的遍历

```html
<div id="app">
  <ul>
    <!-- 括号里如果写两个参数：则第一个参数代表value，第二个参数代表key -->
    <li v-for="(value,key) in obj1">值：{{value}} --- 键：{{key}}</li>

    <!--
      括号里如果写三个参数：则第一个参数代表value，第二个参数代表key，第三个参数代表index
    -->
    <li v-for="(value,key,index) in obj1">
      值：{{value}} --- 键：{{key}} --- index：{{index}}
    </li>
  </ul>
</div>
<script>
  const vm = new Vue({
    el: '#app',
    data: {
      obj1: {
        name: 'smyhvae',
        age: '26',
        gender: '男'
      }
    }
  })
</script>
```

方式四：遍历数字

```html
<ul>
  <!-- 注意：如果使用 v-for 遍历数字的话，前面的 myCount 值从 1 开始算起 -->
  <li v-for="myCount in 10">这是第 {{myCount}}次循环</li>
</ul>
```

**v-for 中 key 的使用注意事项**：

**注意**：在 Vue 2.2.0+ 版本里，当在组件中使用 v-for 时，key 属性是必须要加上的。

这样做是因为：每次 for 循环的时候，通过指定 key 来标示当前循环这一项的**唯一身份**。

> 当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue 将不是移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。
> 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。

key 的类型只能是：string/number，而且要通过 v-bind 来指定。

## v-cloak

解决插值表达式闪烁问题

**原理**：当 vue 没加载之前，v-cloak 给 p 元素添加

```css
[v-cloak] { display: none }
```

当vue加载完成的时候，vue会把所有的v-cloak指令移除

## v-pre

vue 渲染的时候直接跳过。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

## v-once

只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
