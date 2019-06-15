# mvc

#### MVC是Model-View- Controller的简写。即模型-视图-控制器。

##### 【控制器】Controller指的是页面业务逻辑。

##### 【模型】Model指的是后端传递的数据。

##### 【视图】View指的是所看到的页面。

##### 使用MVC的目的就是将M和V的代码分离。‘MVC是单向通信。也就是View跟Model，必须通过Controller来承上启下。

# mvvm

#### MVVM是Model-View-ViewModel的简写。即模型-视图-视图模型。

##### 【模型】指的是后端传递的数据。

##### 【视图】指的是所看到的页面。

##### 【视图模型】mvvm模式的核心，它是连接view和model的桥梁。

vm负责从model里取出数据，传递给view去显示

它有两个方向：

```
1. 一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。
实现的方式是：数据绑定。

2. 二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据。
实现的方式是：DOM 事件监听。
```

这两个方向都实现的，我们称之为数据的双向绑定。

MVVM流程图如下：

![](C:\Users\qianfeng\Desktop\vue\image\MVVM.jpg)

### 前端三大框架

angular(已经没落)

react

vue

