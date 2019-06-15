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

