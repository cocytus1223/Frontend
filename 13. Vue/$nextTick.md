# \$nextTick 的使用

## 什么是\$nextTick？

因为 Vue 的异步更新队列，\$nextTick 是用来知道什么时候 DOM 更新完成的。

我们先来看这样一个场景：有一个 `div`，默认用 `v-if` 将它隐藏，点击一个按钮后，改变 `v-if` 的值，让它显示出来，同时拿到这个 `div` 的文本内容。如果 `v-if` 的值是 `false`，直接去获取 `div` 内容是获取不到的，因为此时 `div` 还没有被创建出来，那么应该在点击按钮后，改变 `v-if` 的值为 `true`，`div` 才会被创建，此时再去获取，示例代码如下：

```html
<div id="app">
  <div id="div" v-if="showDiv">这是一段文本</div>
  <button @click="getText">获取div内容</button>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      showDiv: false
    },
    methods: {
      getText() {
        this.showDiv = true
        var text = document.getElementById('div').innnerHTML
        console.log(text)
      }
    }
  })
</script>
```

这段代码并不难理解，但是运行后在控制台会抛出一个错误：`Cannot read property 'innnerHTML of null`，意思就是获取不到 `div` 元素。这里就涉及 `Vue` 一个重要的概念：异步更新队列。

## 异步更新队列

Vue 在观察到数据变化时并不是直接更新 DOM，而是开启一个队列，并缓冲在同一个事件循环中发生的所以数据改变。在缓冲时会去除重复数据，从而避免不必要的计算和 DOM 操作。然后，在下一个事件循环 `tick` 中，Vue 刷新队列并执行实际（已去重的）工作。所以如果你用一个 for 循环来动态改变数据 100 次，其实它只会应用最后一次改变，如果没有这种机制，DOM 就要重绘 100 次，这固然是一个很大的开销。

Vue 会根据当前浏览器环境优先使用原生的 `Promise.then` 和 `MutationObserver`，如果都不支持，就会采用 `setTimeout` 代替。
知道了 Vue 异步更新 DOM 的原理，上面示例的报错也就不难理解了。事实上，在执行 this.showDiv = true 时，div 仍然还是没有被创建出来，直到下一个 vue 事件循环时，才开始创建。\$nextTick 就是用来知道什么时候 DOM 更新完成的，所以上面的示例代码需要修改为：

```html
<div id="app">
  <div id="div" v-if="showDiv">这是一段文本</div>
  <button @click="getText">获取div内容</button>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      showDiv: false
    },
    methods: {
      getText() {
        this.showDiv = true
        this.$nextTick(function() {
          var text = document.getElementById('div').innnerHTML
          console.log(text)
        })
      }
    }
  })
</script>
```

这时再点击事件，控制台就打印出 `div` 的内容“这是一段文本“了。
理论上，我们应该不用去主动操作 DOM，因为 Vue 的核心思想就是数据驱动 DOM，但在很多业务里，我们避免不了会使用一些第三方库，比如 popper.js、swiper 等，这些基于原生 `javascript` 的库都有创建和更新及销毁的完整生命周期，与 Vue 配合使用时，就要利用好\$nextTick。
