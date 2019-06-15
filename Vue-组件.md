## component组件

注册的组件大驼峰命名，在html里面使用这个组件的时候需要把大写变为小写，然后使用中线连接

全局注册组件,在每一个Vue实例里都能使用

局部注册组件，那么就只能在当前实例里面使用

```html
<div id="app">
    <!-- 注册的组件大驼峰命名，在html里面使用这个组件的时候需要把大写变为小写，然后使用中线连接 -->
    <hello-world></hello-world>
    <hello-vue></hello-vue>
</div>
```

```javascript
// 全局注册组件，在每一个Vue实例里都能使用
Vue.component('HelloWorld', {
    template: '<div>hello world</div>'
})

// 定义一个组件
const HelloVue = {
    template: '<h1>hello Vue</h1>'
}

// 全局注册组件
Vue.component('HelloVue', HelloVue)

// 局部注册组件，那么只能在当前示例里面使用
const app = new Vue({
    el: '#app',
    // 局部注册组件
    components: {
        HelloVue
    }
})
```

组件的data必须是一个方法，因为每个组件的数据都是独立的，使用方法可以保证不共享，return一个对象

```javascript
Vue.component('HelloWorld', {
    template: '<div>{{msg}}</div>',
    // 组件的data必须是一个方法，因为每个组件的数据是独立的，使用方法可以保证不共享，return一个对象
    data () {
        return {
            msg: 'hello'
        }
    }
})
```

### **props ** 接收和转入值

组件内部的props可以直接作为data使用

```html
<div id="app">
    <!-- 使用这个组建的时候把msg传递给组件内部，在组件内部通过props类接收 -->
    <hello-world msg="hello component"></hello-world>
    <!-- 绑定的方式在传递，所以这个时候把data里面的msg1传递过去了 -->
    <hello-world :msg="msg1"></hello-world>
</div>
```

```javascript
const HelloWorld = {
    template: '<div>{{msg}}</div>',
    // 组件内部的props可以直接作为data使用
    props: ['msg']
}
const app = new Vue({
    el: '#app',
    data: {
        msg1: 'hello'
    },
    components: {
        HelloWorld
    }
})
```

props数据检验

```html
<!--传递数字或 者boolean需要绑定，否则传递过去以后解析成字符串 -->
<hello-world msg="hello component" :num="3"></hello-world>
```

```javascript
 props: {
     msg: {
         // 校验数据类型，是否必传
         type: String,
         required: true
     },
     num: {
         type: Number,
         // 默认值
         default: 0
     },
         isCompleted: Boolean
   }
}
```

props绑定驼峰的方式要改成中线

```html
<div id="app">
    <!-- props绑定驼峰方式要改写成中线 -->
    <!-- html属性名用中线，javascript使用驼峰 -->
    		  <!-- userName -->
    <hello-world :user-name="userName"></hello-world>
</div>
```

## emit  

子组件可以通过调用内建的 [**$emit** 方法](https://cn.vuejs.org/v2/api/#vm-emit) 并传入事件名称来触发一个事件

使用用一个事件来抛出一个特定的值

由于props是单向的数据流，所以父组件并不能响应子组件对props的修改

```html
<div id="app">
    <!-- 监听子组件的自定义事件，当子组件emit这个事件的时候，父组件这个方法就会响应执行 -->
    <hello-world :num="num" @num-add="onParentAddNum"></hello-world>
</div>
```

```javascript
const HelloWorld = {
    template: '<div>{{num}}<button @click="onAddNum">Add</button></div>',
    // 组件内部props可以直接作为data使用
    props: ['num'],
    methods: {
        onAddNum () {
            // 子组件的props一般不允许直接修改
          	// this.num++
            // 子组件向父组件触发了一个numAdd事件
            // 自定义事件也要用中线而不用驼峰
            this.$emit('num-add', {
                num: this.num+1
            })
        }
    },
    // 由于props是单向的数据流，所以父组件并不能响应子组件对props的修改
    // created () {
    //   console.log(this.num)
    // }
}

const app = new Vue({
    el: '#app',
    data: {
        num: 1
    },
    methods: {
        onParentAddNum (num) {
            // 函数第一个参数就是自定义事件传过来的参数
            // 就可以响应子组件对数据的修改
            this.num = num.num;
            console.log(this.num)
        }
    },
    components: {
        HelloWorld
    }
})
```

**event bus**  事件总线(空的vue实例来进行两个兄弟组件之间的数据传输)

两个相邻的组件之间传值

```html
 <div id="app">
     <ge></ge>
     <di></di>
</div>
```

```javascript
// event bus 事件总线(空的vue示例来进行两个兄弟组件之间的数据传输)
const bus = new Vue()

const ge = {
    template: '<div><span @click="onDwd">打我弟</span></div>',
    methods: {
        onDwd  () {
            // 在点击的时候触发这个wuwuwu事件，di这个组件就能响应这个事件
            // 让bus触发一个自定义事件
            bus.$emit('wuwuwu', {
                kusheng: 'yinyinyin'
            })
        }
    }
}
const di = {
    template: '<div><span>{{ku}}<span></div>',
    data () {
        return {
            ku: ''
        }
    },
    created () {
        // 一上来就要监听事件总线的wuwuwu
        bus.$on('wuwuwu', (data) => {
            // 响应ge组件里通过bus给我emit的这个wuwuwu事件
            // 接听到传递给我的参数data
            console.log(data)
            this.ku = data.kusheng
        })
    }
}
const app = new Vue({
    el: '#app',
    components: {
        ge,
        di
    }
})
```

### template

```html
<div id="app">
    <product
      :price="90"
      title="这是最贵的小姐姐"
      :src="src"
    ></product>
  </div>

  <template id="product">
    <div>
      <div class="img">
        <img :src="src" alt="">
      </div>
      <p>{{title}}</p>
      <p>￥<span>{{price}}</span></p>
    </div>
  </template>
```

```javascript
 const Product = {
      template: '#product',
      props: ['src', 'title', 'price']
      // props: {
      //   src: String,
      //   title: String,
      //   price: Number
      // }
    }

    const app = new Vue({
      el: '#app',
      data: {
        src: 'http://pic25.nipic.com/20121205/10197997_003647426000_2.jpg'
      },
      components: {
        Product
      }
    })
```

