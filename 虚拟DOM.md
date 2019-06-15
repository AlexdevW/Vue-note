## 虚拟DOM对象

根据真实DOM构建一个虚拟DOM (js对象)

当DOM要修改的时候，需先修改虚拟dom

用修改之后的虚拟dom跟之前的进行脏检查 （diff算法）

把修改过后的那一部分重新渲染真实dom

可以避免多次dom操作

```html
<div>
    <ul>
        <li>item1</li>
        <li>item2</li>
    </ul>
</div>
```

```javascript
// 根据真实DOM构建一个虚拟DOM（js对象）
// 当DOM要修改的时候，会先修改虚拟DOM
// 用修改之后的虚拟DOM跟修改之前的进行脏检查 （diff算法）
// 把修改过后的那一部分重新渲染真实DOM
// 可以避免多次的DOM操作
const vDom = {
    html: {
        tag: 'html',
        children: [
            {
                tag: 'head'
            },
            {
                tag: 'body',
                style: {
                    width: 1200
                },
                id: 'app'
            }
        ]
    }
}
```

