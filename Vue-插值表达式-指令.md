### **插值表达式**

表达式：通过计算后能得到一个结果

插值表达式里面不能放语句

1. 插值表达式里面放的是javascript表达式
2. 插值表达式不会解析html字符串，当作普通文本在解析
3. 当指令和插值表达式同时存在的时候，指令生效

```html
 <div id="app">
     <!-- 差值表达式里面代表javascript表达式 -->
     {{'a'}}<br>
     {{1+2}}<br>
     {{message && 'hello Vue'}}<br>
     {{message > 1 ? '你算对了' : '你算错了'}}
 </div>
```

```javascript
<script>
    const app = new Vue({
        el: "#app",
        data: {
            message: 2
        }
    })
</script>
```

### tbody里只能是tr，所以这个地方需要使用动态组件，加上is属性 

```html
is='组建名'
<tr is="my-tr"></tr>
```



### 指令

1. **v-text="str"** v-text不会解析html字符串当, 作普通文本来解析

2. **v-html="str**"  v-html能解析html字符串

```html
<div id="app">
    <!-- 插值表达式不会解析html字符串，当作普通文本在解析 -->
    {{str}}<br>
    <!-- 指令里面是javascript -->
    <p v-text="str"></p>
    <!-- 由于指令里面只能放javascript,所以会把内容当成属性和方法去读取，因此我们需要给内容加上引号 -->
    <p v-text="'你好'"></p>
    <!-- 当指令和插值表达式同时存在的时候，指令生效 -->
    <p v-text="'你好'"> {{str}}</p>
    <!-- v-html能解析html字符串 -->
    <p v-html="str"></p>
</div>
```

```javascript
<script>
    const app = new Vue({
      el: '#app',
      data: {
        str: '<b>hello</b>'
      }
    })
</script>
```

3. **v-if="true"**  通过javascript的值来决定这个元素是否被渲染 

   **v-if** 是通过是否渲染来决定显示隐藏

4. **v-else** 只作用于上一个兄弟元素的v-if

5. **v-show="true"** 通过javascript的值来决定这个元素是否被渲染 如果一个元素要频繁切换显示隐藏用v-show **v-show** 是通过display样式来决定是否显示，他一定会被渲染

```html
<div id="app">
    <!-- 通过一个javascript的值来决定这个元素是否渲染 -->
    <!-- v-if是通过是否渲染来决定显示隐藏 -->

    <div v-if="false">这是一个弹框1</div>
    <div v-if="1 + 1 === 2">这是一个弹框2</div>
    <div v-if="0">这是一个弹框3</div>
    <div v-if="isModelShow">这是一个弹框4</div>
    <!-- v-else只作用与上一个兄弟元素的v-if -->
    <div v-else>这事跟弹框4相反的一个显示</div>
    <!-- v-show是通过display样式来决定是否显示，也就是说他是一定会渲染的 -->
    <div v-show="true">这是一个弹框5</div>
    <div v-show="1 + 1 === 3">这是一个弹框6</div>

    <!-- 如果一个元素要频繁的切换显示隐藏，用v-show -->
</div>
```

6. **v-for="(item, index) in items"**  循环data标签等到元素值和索引，循环渲染当前列表

```html
<div id="app">
    <ul>
        <!-- 循环data数据，得到元素值和索引，循环渲染当前标签 -->
        <li v-for="(like, index) in likes">
            {{index}} : {{like.name}}
        </li>
    </ul>
    
    <!-- v-for 可以循环数字 -->
    <p v-for="n in 10">
        {{n}}
    </p>
    
    <!-- 可以循环字符串 -->
    <p v-for="item in 'hello'">
        {{item}}
    </p>
   
    <ul>
         <!-- 可以循环对象 -->
         <li v-for='(value, key) in person'>
       		 {{key}}, {{value}}
    	</li>
    </ul>
</div>
```

7. **v-model** 输入框的v-model指令负责绑定value

   双向绑定，用户在input里面输入值会自动绑定到data上

```html
<div id="app">
    <!-- 输入框的v-model指令负责绑定value -->
    <!-- 双向绑定，用户在input里输入值会自动绑定到data上 -->
    <input type="text" v-model="username">
    {{username}}
</div>
```

​	**v-model** 用在select上，绑定的就是被选中的那个option的value

​	**v-model** 可以使用一个数组来绑定多选按钮，选中的value值就会存在这个

​	**v-model** 使用在checkbox上的时候代表多选框的选中状态，绑定的就是checked的属性

```html
<div id="app">
    <!-- v-model用在select上，绑定的就是选中的那个option的value -->
    <select v-model="city">
      <option>--请选择--</option>
      <option value="cd">成都</option>
      <option value="bj">北京</option>
      <option value="sh">上海</option>
    </select>
    {{city}}
    <!-- v-model使用在checkbox上的时候代表多选框的选中状态，绑定的是checked属性 -->
    <input type="checkbox" v-model="isChecked">
    <br>
    <!-- v-model可以使用一个数字来绑定多选按钮，选中的value值就会存在这个数组里 -->
    城市列表
    成都：<input type="checkbox" value="成都" v-model="arrCities">
    北京：<input type="checkbox" value="北京" v-model="arrCities">
    上海：<input type="checkbox" value="上海" v-model="arrCities">
    <br>
    <input type="radio" >
 </div>
```

```javascript
<script>
    const app = new Vue({
        el: '#app',
        data: {
            city: 'cd',
            isChecked: false,
            arrCities: []
        }
    })
</script>
```

8. **v-cloak** 加上v-cloak这个指令之后，在vue实例化之前div身上就会有v-clock这个属性，实例化之后这个属性就会被移除	

   解决了页面卡顿给用户带来了不好的体验

```html
 <style>
     [v-cloak]{
         display: none;
     }
</style>

 <!-- 加上v-cloak这个指令之后，在Vue在实例化之前就会div身上就会有v-cloak这个属性，实例化之后这个属性就会被移除 -->
    <!-- 解决了页面卡顿给用户带来不好的体验 -->
<div id="app" v-cloak>
    {{msg}}
</div>
```

```javascript
 <script>
     setTimeout(() => {
     const app = new Vue({
         el: '#app',
         data: {
             msg: 'hello world'
         }
     })
     }, 3000)

</script>
```

9. **v-bind：** 用来绑定一个属性值用javascript去执行 **可以简写为：**

```html
<div id="app">
    <!-- v-bind用来绑定一个属性属性值用javascript去执行 -->
    <a v-bind:href="baiduLink">跳转</a>
    <img v-bind:src="imgUrl" alt="">
    <!-- v-bind可以简写为 : -->
    <img :src="imgUrl" alt="">
    <br>

    <ul>
        <!-- 循环data数据，得到索引和元素值，循环渲染当前列表 -->
        <!-- 给没一个循环动态的绑定一个唯一的key,这个key一般是一条数据的id,或者name、title之类的唯一标识 -->
        <li v-for="(like, index) in likes" :key="like.id">
            {{index}} : {{like.name}}
        </li>
    </ul>
</div>
```

```javascript
 <script>
     const app = new Vue({
         el: '#app',
         data: {
             baiduLink: 'http://www.baidu.com',
             imgUrl: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=4135477902,3355939884&fm=26&gp=0.jpg' ,          
             likes: [
                 {
                     id: 1,
                     name: '抽烟'
                 },
                 {
                     id: 2,
                     name: '喝酒'
                 },
                 {
                     id: 3,
                     name: '烫头'
                 }
             ]
         }
     })
</script>
```

​	**v-bind：** 绑定class名称

```html
<div id="app">
    <!-- 绑定class名称 -->
    <div :class="'box'"></div>
    <div :class="className"></div>

    <!-- 可以绑定一个对象,通过isAc的boolean来决定ac是否存在 -->
    <div :class="{ac: isAc}"></div>
    <!-- 普通class和绑定class可以共存,最后把两部分叠加渲染 -->
    <div class="box" :class="{ac: isAc}"></div>
    <!-- 这个是最复杂的用法,绑定一个数组,数组元素可以直接是class名称就能直接绑定,如果另外一个class根据数据决定,那就再写一个对象 -->
    <div :class="[className, {ac: isAc}]"></div>


    <p :style="style">Lorem ipsum dolor sit amet consectetur adipisicing elit. Rem dignissimos in quo sequi ipsa numquam, aspernatur commodi doloremque delectus adipisci! Ex sapiente veritatis quibusdam inventore vel labore atque minima quaerat!</p>

</div>
```

```javascript
<script>
    const app = new Vue({
        el: '#app',
        data: {
            className: 'box',
            isAc: false,
            style: {
                width: '100px',
                height: '100px',
                color: 'red'
            }
        }
    })
</script>
```

10. **v-on:**  监听事件 可以简写为@

```html
<div id="app">
    <button v-on:click="onNumDecrease">decrease</button>
    {{num}}
    <!-- <button v-on:click="++num">Add</button> -->
    <!-- <button v-on:click="onNumAdd(12, $event)">Add</button> -->
    <!-- v-on:click指令可以简写为@click -->
    <button @click="onNumAdd(12, $event)">Add</button>
</div>
```

```javascript
 <script>
     const app = new Vue({
         el: '#app',
         data: {
             num: 1,
         },
         methods: {
             //定义value实例的方法
             onNumDecrease (e) {
                 // 事件处理函数在v-on监听的时候不写括号，函数的第一个参数就是事件对象
                 console.log(e)
                 this.num--
             },
             onNumAdd (n, e) {
                 // 事件处理函数在v-on监听的时候写了括号，那么就可以传参，而且传一个特殊变量$event就是事件对象
                 console.log(n)
                 console.log(e)
             }
         }
     })
</script>
```

.stop 事件修饰符，事件监听的时候就阻止冒泡

.prevent 事件监听的时候阻止默认事件

```html
<div id="app">
    <!-- v-bind可以把data数据绑定给value, @input把用户输入的值取赋给data,这样实现了双向绑定 -->
    <input type="text" :value="username" @input="onInput">
    {{username}}
</div>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            username: '张三'
        },
        methods: {
            onInput (e) {
                console.log(e.target.value)
                this.username = e.target.value
            }
        }
    })
</script>
```

```html
<div id="app">
    <p><label>抽烟<input type="checkbox" value="抽烟" @change='onChange'></label></p>
    <p><label>喝酒<input type="checkbox" value="喝酒" @change='onChange'></label></p>
    <p><label>烫头<input type="checkbox" value="烫头" @change='onChange'></label></p>

    <p>{{likes.toString()}}</p>
</div>
```

```javascript
<script>
    const app = new Vue({
        el: '#app',
        data: {
            likes: []
        },
        methods: {
            onChange(e) {
                const val = e.target.value;
                if (this.likes.includes(val)) {
                    // 这个爱好已经被选中了
                    // 只留下不等于当前爱好的值(把当前的删掉)
                    this.likes = this.likes.filter(like => like !== val)
                } else {
                    this.likes.push(val)
                }
            }
        }
    })
</script>
```

