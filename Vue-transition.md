## transition

```html
<template id="guonei">
    <p>国内新闻</p>
</template>
<template id="guoji">
    <p>国际新闻</p>
</template>

<div id="app">
    <button @click='show = !show'>切换</button>
    <transition name='news' mode="out-in">
        <div :is="show ? 'guoji' : 'guonei'"></div>
    </transition>
    <transition mode="out-in">
        <div :is="show ? 'guoji' : 'guonei'"></div>
    </transition>
</div>
```

```javascript
const guonei = {
    template: '#guonei',
}

const guoji = {
    template: '#guoji'
}

const app = new Vue({
    el: '#app',
    data: {
        show: true
    },
    components: {
        guoji,
        guonei
    }
})
```

```css
<style>
/* 这种写法会给当前示例里的所有的transition应用加上过度 */
/* .v-enter-active,
.v-leave-active {
transition: opacity 3s
}

.v-enter,
.v-leave-to {
opacity: 0;
}

.v-enter-to,
.v-leave {
opacity: 1;
} */

/* 如果只希望只有一个transition应用这个过渡的话就在transition上加上name属性 class就写成(.news-enter-active) */
.news-enter-active,
.news-leave-active {
    transition: opacity 3s
}

.news-enter,
.news-leave-to {
    opacity: 0;
}

.news-enter-to,
.news-leave {
    opacity: 1;
}
</style>
```

### animate css动画库

```html
 <link rel="stylesheet" href="animate.css">

<template id="guonei">
    <div >
        <h3>国际新闻</h3>
    </div>
</template >
<template id="guoji">
    <div >
        <h3>国内新闻</h3>
    </div>
</template>

<div id="app">
    <button @click="show = !show">切换</button>
    <transition
                mode="out-in"
                enter-to-class="zoomOutRight"
                enter-active-class="animated"
                leave-active-class="animated"
                leave-to-class="zoomOutLeft"
                >
        <div :is="show ? 'guonei' : 'guoji'"></div>
    </transition>
</div>
```

```javascript
<script>
    const guonei = {
        template: '#guonei'
    }
const guoji = {
    template: '#guoji'
}

const app = new Vue({
    el: '#app',
    data: {
        show: true
    },
    components: {
        guonei,
        guoji
    }
})
</script>
```

给多个元素使用过度

```html
<transition-group></transition-group>
```

