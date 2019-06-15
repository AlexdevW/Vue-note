# 计算属性

**computed** 每次数据发生改变的时候才会重新计算，是会缓存的

```javascript
computed: {
    // 计算属性
    // 每次数据发生改变的时候会重新计算
    // 这里的属性可以之间作为data使用
    unCompletedTodo () {
        // 每一个计算属性都是一个方法，return的值就是这个属性值
        return this.todoList.filter(todo => !todo.hasCompleted)
    },
    hasCompletedTodo () {
        return this.todoList.filter(todo => todo.hasCompleted)
    }
}
```

## **侦听属性**

**watch** 监听值得修改 只要值发生能改变，都会执行这个方法

```javascript
watch: {
    // 监听值得修改
    // 只要值发生了改变，都会触发这个方法
    xing (nVal, oVal) {
    			 // 现在  原来
        console.log(nVal, oVal)
        // 性发生了改变
        this.name = nVal + this.ming;
   }
}
```

## 过滤器

**filters**  

```javascript
<!-- 竖线过后写过滤器的名字，就会把前面值传递给过滤器，过滤器处理和在把值作为插值表达式来显示 --><h5>{{goods.title | toUpper}}</h5>
filters: {
		// 定义一个过滤器、接受要过滤的值、返回过滤的结果
        toUpper (val) {
        // console.log(val)
        return val.toUpperCase()
    }
}
```

## fetch

**fetch** 原生支持的fetch  返回的是一个promise

```javascript
// 原生支持的fetch
// 返回的是一个promise
// 在第一个then里得到的是fetch封装过一次的response， 所以需要调用一次json()方法,解析成json数据
// 在第二个then里就能得到后端返回回来的resp了
fetch('https://jsonplaceholder.typicode.com/todos')
    .then(resp => resp.json())
    .then(resp => {
    console.log(resp)
})
```

## axios

**axios** 请求数据的方法



#### Vue获取dom元素

```javascript
// 可以在DOM元素上加上 ref="abc"
// 就可以在js代码中vue示例里，一般就是this.$refs.abc来获取这个元素DOM对象
<p ref="abc"></p>
this.$refs.abc.focus();
```



  