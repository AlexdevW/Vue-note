复选框美化

```html
<label class="hw-cart-item-check">
    <input type="checkbox" :checked="isCheck">
    <span></span>
</label>
```

```css
&-check {
    display: inline-block;
    width: 20px;
    margin: 10px 10px 0 0;
    input {
        display: none; 
        &:checked {
            + span {
                background-color: $mainColor;
                border-color: $mainColor;
                position: relative;

                &::after {
                    content: "";
                    position: absolute;
                    width: 13px;
                    height: 7px;
                    border: 2px solid #ffffff;
                    border-width: 0 0px 2px 2px;
                    left: 0;
                    top: 0;
                    transform: rotate(-45deg)
                }
            }
        }
    }
    span {
        display: inline-block;
        width: 20px;
        height: 20px;
        box-sizing: border-box;
        border: 2px solid $deepGrey;
    }
}
```

```css
width: auto;
border-width: 0 1px;
```

### 去掉input type=number时输入框内的上下箭头

```
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
input[type="number"]{
  -moz-appearance: textfield;
}
```

### 限制 `input` 输入框只能输入纯数字

```js
只能输入纯数字的输入框:<input type="text" name="" oninput="value=value.replace(/[^\d]/g,'')">
```

#### input不能为空，不能以0开头，只能是纯数字

```js
let val = this.$refs.input.value  // <input> type属性为Number
if (val < 1 || val.startsWith(0)) this.$refs.input.value = this.count
```



