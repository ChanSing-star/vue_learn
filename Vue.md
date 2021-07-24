# watch
```js
watch:{
   name(newValue, oldValue) { 

   }
}
```
1. 当被监视的属性调用时，回调函数自动调用
2. 属性必须存在，才能进行监视
3. 监视的两种写法  
   1. new Vue时传入watch配置
   2. 通过vm.$watch监视
### 备注： 
1. 所有被Vue所调用的函数不要用箭头函数  
   例如：watch中的函数、computed中的函数
2. 所有不是被Vue所调用的函数，都要写成箭头函数。  
   例如：定时器的回调、ajax的回调等等

# 数组更新检测
## 变更方法
Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：
* push()
* pop()
* shift()
* unshift()
* splice()
* sort()
* reverse()  

你可以打开控制台，然后对前面例子的 items 数组尝试调用变更方法。比如 example1.items.push({ message: 'Baz' })。
## 替换数组
例如 filter()、concat() 和 slice()。它们不会变更原始数组，而总是返回一个新数组。
```js
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```
### 注意事项
由于 JavaScript 的限制，**Vue 不能检测数组和对象的变化**。深入响应式原理中有相关的讨论

# 事件修饰符
* .stop
* .prevent
* .capture
* .self
* .once
* .passive
```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```
