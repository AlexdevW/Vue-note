### $ router

1.router是VueRouter的一个对象，通过Vue.use(VueRouter)和VueRouter构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由包含了许多关键的对象和属性。

#### $ route

2.route是一个跳转的路由对象，每一个路由都会有一个route对象，是一个局部的对象，可以获取对应的name,path,params,query等

**component**是注册全局组件，在实例化VUE前调用，注册后可以全局使用

**components**是局部注册组件，注册后只能在当页调用。

### 嵌套路由

```javascript
{
      path: '/list',
      name: 'list',
      component: List,
      children: [
        {
          path: ':cateName',
          name: 'category',
          components: {
            default: Category,
            a: Test
          }
        }
      ]
    },
```

### 编程式导航

除了使用 `<router-link>` 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。

```javascript
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
```

**注意：如果提供了 path，params 会被忽略，上述例子中的 query 并不属于这种情况。取而代之的是下面例子的做法，你需要提供路由的 name 或手写完整的带有参数的 path：**

```javascript
const userId = '123'
router.push({ name: 'user', params: { userId }}) // -> /user/123
router.push({ path: `/user/${userId}` }) // -> /user/123
// 这里的 params 不生效
router.push({ path: '/user', params: { userId }}) // -> /user
```

## `router.go(n)`

这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 `window.history.go(n)`。

```javascript
// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)

// 后退一步记录，等同于 history.back()
router.go(-1)

// 前进 3 步记录
router.go(3)

// 如果 history 记录不够用，那就默默地失败呗
router.go(-100)
router.go(100)
```

### 命名路由

有时候，通过一个名称来标识一个路由显得更方便一些，特别是在链接一个路由，或者是执行一些跳转的时候。你可以在创建 Router 实例的时候，在 `routes` 配置中给某个路由设置名称

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})
```

要链接到一个命名路由，可以给 `router-link` 的 `to` 属性传一个对象：

```javascript
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```

这跟代码调用 `router.push()` 是一回事：

```javascript
router.push({ name: 'user', params: { userId: 123 }})
```

### 命名视图

有时候想同时 (同级) 展示多个视图，而不是嵌套展示，例如创建一个布局，有 `sidebar` (侧导航) 和 `main` (主内容) 两个视图，这个时候命名视图就派上用场了。

如果 `router-view` 没有设置名字，那么默认为 `default`。

```javascript
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
```

一个视图使用一个组件渲染，因此对于同个路由，多个视图就需要多个组件。确保正确使用 `components`配置 (带上 s)：

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
      }
    }
  ]
})
```

### 重定向

重定向也是通过 `routes` 配置来完成 下面例子是从 `/a` 重定向到 `/b`：

```javascript
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})
```

重定向的目标也可以是一个命名的路由：

```javascript
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: { name: 'foo' }}
  ]
})
```

甚至是一个方法，动态返回重定向目标：

```javascript
redirect: to => {
    if (to.meta.isAuthRequired) {
        // 这个组件需要权限验证
        if (!isLogin) {
            return '/login'
        } else {
            return '/list/category'
        }
    }
},
```

### 别名 alias

```javascript
path: '/home',
alias: '/'
```

### HTML5 History 模式

`vue-router` 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。

  如果不想要很丑的 hash，我们可以用路由的 **history 模式**，这种模式充分利用 `history.pushState` API 来完成 URL 跳转而无须重新加载页面。

```js
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

**History** 需要后端配置

##### Apache  、 nginx 、原生 Node.js

# 导航守卫

`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

### 全局前置守卫

可以使用 `router.beforeEach` 注册一个全局前置守卫：

```javascript
const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
  // ...
})
```

```js
// 全局导航守卫
// 在每一次导航发生改变（路由跳转）之前都会进入这个钩子函数，在这个函数里只有调用了next才会跳转
// 一般可以用于全局的权限验证
router.beforeEach((to, from, next) => {
  // console.log({ to, from, next })
  // 判断当前要跳转的那个组件是否需要权限
  if (to.meta.isAuthRequired) {
    // 验证是否已经登录
    if (isLogin) {
      next()
    } else {
      // 没有登录就中断当前导航，进入新的导航（登录）
      next({path: '/login'})
    }
  } else {
    // 不需要权限验证，直接进入当前导航
    next()
  }
})
```



每个守卫方法接收三个参数：

- **to: Route**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1)

- **from: Route**: 当前导航正要离开的路由

- **next: Function**: 一定要调用该方法来 **resolve** 这个钩子。

  **next()**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。

  **next(false)**: 中断当前的导航

  **next('/') 或者 next({ path: '/' })**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。

## 路由独享的守卫

你可以在路由配置上直接定义 `beforeEnter` 守卫：

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

## 组件内的守卫

可以在路由组件内直接定义以下路由导航守卫

- `beforeRouteEnter`
- `beforeRouteUpdate` (2.2 新增)
- `beforeRouteLeave`

```js
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```

`beforeRouteEnter` 守卫 **不能** 访问 `this`，因为守卫在导航确认前被调用,因此即将登场的新组件还没被创建。

不过，你可以通过传一个回调给 `next`来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。

```js
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```

```js
export default {
  data () {
    return {
      cateName: ''
    }
    
  },
  created () {
    console.log('created')
  },
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建

    // 在next里可以传递一个回调函数，这个回调函数的第一个形参就是this
    next(vm => {
      console.log(vm)
      vm.cateName = to.params.cateName
      vm.getData()
    })
  },
  beforeRouteUpdate (to, from, next) {
    // console.log({to, from, next})
    // console.log(to.params.cateName)
    this.cateName = to.params.cateName
    this.getData()
    next()
  },
  methods: {
    getData () {
      // 发送ajax请求渲染当前分类页
    }
  }
}
```

# 路由元信息

定义路由的时候可以配置 `meta` 字段：

```js
meta: { requiresAuth: true }
```

# 路由懒加载

当打包构建应用时，JavaScript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

结合 Vue 的[异步组件](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#%E5%BC%82%E6%AD%A5%E7%BB%84%E4%BB%B6)和 Webpack 的[代码分割功能](https://doc.webpack-china.org/guides/code-splitting-async/#require-ensure-/)，轻松实现路由组件的懒加载。

## 把组件按组分块

有时候我们想把某个路由下的所有组件都打包在同个异步块 (chunk) 中

```js
const Home = () => import(/* webpackChunkName: "group-foo" */ './views/Home')
const Category = () => import(/* webpackChunkName: "group-foo" */ './views/Category')
const List = () => import(/* webpackChunkName: "group-bar" */ './views/List')
```

