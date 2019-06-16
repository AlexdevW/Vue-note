## nextTick()

 **$nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM**

#### 应用场景

在Vue生命周期的`created()`钩子函数进行的DOM操作一定要放在`Vue.nextTick()`的回调函数中

```js
this.$nextTick().then(() => {
    this.initSwiper()
})
```

### Proxy 代理跨域

如果前端应用和后端 API 服务器没有运行在同一个主机上，需要在开发环境下将 API 请求代理到 API 服务器。

在根目录下建一个名为 `vue.config.js` 的文件，写入下面这段代码

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: '<url>',
        ws: true,
        changeOrigin: true
      },
      '/foo': {
        target: '<other_url>'
      }
    }
  }
}
```

### 图片大小适配

```css
div {
    width: 100%;
    height: ((图片)w / （图片）h) * 100%； 
}
img {
    width: 100%;
}
```

### exact修饰符

`.exact` 修饰符允许你控制由精确的系统修饰符组合触发的事件。

```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

#### router-link-exact-active 是精确匹配规则，即只有当前点击router被匹配

#### router-link-active 默认是全包含匹配规则，即path名全包含在当前router path名开头的router也会被匹配到。

```html
　　　　　　　1. <router-link to='/'>

　　　　　　　2. <router-link to='/a'>

　　　　　　　3. <router-link to='/b'>

　　　　　　　4. <router-link to='/ab'>

　　　　　　　2/3号被选中 1号也会被匹配到router-link-active，4号被选中1号2号两个也会被匹配到router-link-active。

　　　　　　　可以通过在router添加exact属性改变为精精确匹配。
```

### 验证登录信息 Validate

- 可以在github 或 npm 上找

#### 工作中token和登录信息分别存储

token一般是后端存

### 在用户做其它的数据请求的时候token会自动的带上

- 在完成登录之后后端会返回一个token
- 这个token大部分情况下不用前端自己存，一般后端会帮我们存到cookie里
- 在做其它的数据请求的时候会自动带上token
- 一般数据请求都是post, 因为post会自动带上token
- 我们前端只验证有没有token,token对不对我们验证不了

#### 路由里配置的是路由的name