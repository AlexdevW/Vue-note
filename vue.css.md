## router-link-exact-active

当<router-link>被激活时Vue自动为我们创建的class类名

```css
.router-link-exact-active {
  color: #e00;
}
```

## scoped

[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)让你可以在同一个文件里完全控制 CSS，将其作为组件代码的一部分。

样式只在当前组件内生效

```css
<style scoped>
  @media (min-width: 250px) {
    .list-container:hover {
      background: orange;
    }
  }
</style>
```

