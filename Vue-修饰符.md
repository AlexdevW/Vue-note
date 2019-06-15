## 事件修饰符

.**stop** 阻止事件冒泡

**.prevent** 阻止默认事件

**.capture** 添加事件监听时使用捕获模式

​	即元素自身触发的事件现在自己身上触发，然后在交由内部元素进行处理

**.self**  当元素自身被触发（点击）时，才会执行处理函数 子元素不会触发

```javascript
使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用
v-on:click.prevent.self 会阻止所有的点击，而
v-on:click.self.prevent 只会阻止对元素自身的点击。
```

**.once** 事件将只会被触发一次

**.passive**  修饰符尤其能够提升移动端的性能

​	不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略，同时浏览器可能会向你展示一个警告

```html
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

## 按键修饰符

.enter

.tab

.delete

.esc

.space

.up

.down

.left

.right

你还可以通过全局 `config.keyCodes` 对象[自定义按键修饰符别名](https://cn.vuejs.org/v2/api/#keyCodes)：

```javascript
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

## 系统修饰键

.ctrl

.alt

.shift

.meta

## 鼠标按钮修饰符

.left

.right

.middle