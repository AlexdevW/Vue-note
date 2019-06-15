![](https://images.cnblogs.com/cnblogs_com/fly_dragon/276813/o_lifecycle-%E6%A0%87%E6%B3%A8%E7%89%88%E6%9C%AC.png)

**beforeCreate**

在实例初始化之后，数据观测（data observer）和event/watcher事件配置之前被调用。

**Created**

实例已经被创建完成之后被调用。在这一步，实例已完成以下配置：数据观测（data observer），属性和方法的预算，watch/event事件回调。然而挂载阶段还没开始，**$el** 属性目前不可见。

Vue 实例观察的数据对象data已经配置好，已经可以得到app.message的值，但Vue 实例使用的根 DOM 元素el还未初始化

created的时候数据已经和data属性进行绑定（放在data中的属性当值发生改变时视图也会发生改变）

**beforeMount** 

data和el均已经初始化，但从{{message}}等现象可以看出此时el并没有渲染进数据，el的值为“虚拟”的元素节点

在挂载开始之前被调用：相关的render函数首次被调用

此时el已经渲染完成并挂载到实例上

**mounted**

el被新创建的vm.$el替换，并挂载到实例上去之后调用该钩子。

**beforeUpdate**

数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。

**updated**

由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。

该钩子在服务器端渲染期间不被调用。

**beforeDestroy**

实例销毁之前调用。在这一步，实例仍然完全可用。

**destroyed**

Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。