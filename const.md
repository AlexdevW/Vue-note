const 关键字并不能定义真正的常量对象

真正的常量对象应该是：**不可扩展、不可修改、不可删除**

实现常量对象：

**Object.freeze()**  冻结一个对象，  表示该对象不可扩展、不可删除、不可修改，并且不可修改该对象已有属性的可枚举性、可配置性、可写性。

```javascript
Object.freeze(obj) //冻结object对象
```

**Object.isFrozen() ** 判断一个对象是否被冻住；

```javascript
Object.ifFrozen(obj) //返回obj是否被冻住
```

**Object.seal()**  让一个对象变得不可扩展不可删除（封闭），也就是永远不能删除已有属性，添加新属性。

```javascript
Object.seal(obj) //让obj对象封闭起来
```

**Object.isSealed()**  返回一个对象是否被封闭

```javascript
Object.isSealed(obj) //返回obj是否别封闭
```

**Object.preventExtensions()** 让一个对象变得不可扩展，也就是永远不能在添加新属性。

object.isExtensible(obj)   //返回obj是否可扩展



