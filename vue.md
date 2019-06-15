# Vue

1. 一套用于构建用户界面的**渐进式框架**
2. Vue 只关注视图层， 采用自底向上增量开发的设计。
3. Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。
4. 易用、灵活，高效

**脏检查**  虚拟DOM元素与旧的虚拟DOM元素之间的差异，只更新不同的那一部分

### **Vue生态系统 全家桶**

#### 1. Vue router

Vue Router是Vue.js的官方路由器。

主要用于单页页面的切换，用路由的好处是不用刷新页面，就可以跳转页面，而且url会变化，便于用户收藏地址

常用于不需要交互数据的页面变化操作。

#### 2. Vuex

Vuex 是一个专为Vue.js应用程序开发的状态管理模式。

专门用于管理数据的一个全局对象。

好处是便于维护，方便和后端交互数据。

### 3. Vue-cli

Vue-cli就是搭建vue项目的一个脚手架，会自动生成webpack的配置，以及大部分项目需要使用到的依赖，只要install就可以了。

### 组件

组件可以扩展 HTML 元素，封装可重用的代码。

页面被分成不同的区域模块,每一个模块就是一个组件

### 响应式数据原理

利用Ojbect.defineProperty方法：

```javascript
var obj = {};
        const xx;

		 const setValue =  () => {
            xx++;
            obj.x = xx;
        }
         
         const setAppText = () => {
            document.querySelector("#app").innerHTML = obj.x;
        }
         
        Object.defineProperty(obj, 'x', {
            // 每一次obj取x的属性的值时候都会调用get
            get () {
                return xx;
            },

            // 每一次在设置obj的x属性的时候都会调用set
            set (newValue) {
                xx = newValue;
                // console.log(newValue)
                setAppText();
            }
        })

        obj.x = 20;
```

利用proxy代理方法  

```javascript
let pro = new Proxy([], {
            // 每一次obj取x的属性的值时候都会调用get
            get (target, name) {
                console.log(target, name);
                return target[name];
            },
			// 每一次在设置obj的x属性的时候都会调用set
            set (obj, prop, value) {
                obj[prop] = value;
                // console.log(obj, prop, value)
                setValue();
            }
        })  
        
        const setValue = () => {
            document.querySelector("#box").innerHTML = pro.x;
        }
        const fn = () => {
            ++pro.x
        }
        pro.x = 10;
```

##### Object.defineProperties （obj， props）//给obj设置属性

##### Object.keys(obj); //获取obj所有的属性名称返回数组

##### object.value(obj); //获取obj所有的属性值返回数组

```javascript
var obj = new Object();
// 给obj设置单个属性
Object.defineProperty(obj, 'name', {
    configurable:false, // 表示能否通过delete删除此属性
    writable： true, // 表示能否修改属性的值
    enumerable: true, // 表示该属性是否可枚举，即能否通过for-in循环或Object.keys()返回属性
    value: '张三'
})

console.log(obj.name)
```

```javascript
var obj = new Object();
// 给obj设置多个属性
Object.defineProperties(obj, {
    name: {
        value: '张三'，
        consfigurable: false, // 表示能否使用delete删除此属性
        writable: true, // 表示能否修改属性的值
        enumerable: true, // 表示该属性是否可枚举，及是通过for-in循环或Object.keys()返回属性
        value: '张三'
    }，
    age: {
    	value: 18,
    	configurable: false // 表示能否通过delete删除该属性
	}
})
```





数据驱动数据做了更新