## #使用router的步骤

router.js

```javascript
import Vue from 'vue'
import Router from 'vue-router'
// 引入需要配置的组件
import Home from './views/Home.vue'
import About from './views/About.vue'
// 使用Router
Vue.use(Router)
// 得到一个Router的实例，并且导出
export default new Router({
  // 通过routes字段配置路由
  routes: [
    {
      path: '/home', // 跳转的路由路径
      name: 'home', // 给组件起个名字
      component: Home // 这个路由对应的组件
    },
    {
      path: '/about',
      name: 'about',
      component: About
    }
  ]
})
```

main.js

```javascript
import Vue from 'vue'
import App from './App.vue'
// 引入了tourer.js
import router from './router'

Vue.config.productionTip = false

new Vue({
  // 实例化vue的时候把router配置进来，我们#app这个实例里就能使用配置好的router了
  router,
  render: h => h(App)
}).$mount('#app')
```

App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <!-- router-link默认会渲染成a标签，to相当于href，就是要跳转的那个组件的path -->
      <router-link to="/home">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <!-- 必须的，组件跳转的显示位置,点击home这儿就显示home组件，点击about这儿就显示about组件 -->
    <router-view/>
  </div>
</template>
```



