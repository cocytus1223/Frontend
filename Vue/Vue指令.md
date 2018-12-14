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
<!-- @click="事件函数名()   优点：可以在()中传递参数 缺点：没有默认的事件对象，手动传入$event" -->
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
- `.prevent` 调用 `event.preventDefault()`。组织默认行为
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
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div @scroll.passive="onScroll">...</div>
```

**注意**：

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用`@click.prevent.self`会阻止所有的点击，而 `@click.self.prevent` 只会阻止对元素自身的点击。

**按键修饰符**：

在监听键盘事件时，我们经常需要检查常见的键值。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

- `.enter`
- `.tab`
- `.delete` (捕获“删除”和“退格”键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`