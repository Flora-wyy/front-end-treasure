### 什么是css隔离？
css样式dom文档是全局生效的，非常容易出现：样式重名，被覆盖, css隔离就是解决该问题

### css隔离有哪些常用方法？
#### 使用命名空间
通过不同的命名或前缀来区分相应的css样式, 这类方法有一定的繁琐工作量
```css

  .a_container {}
  .b_conainer {}
```

### shadow Dom
element.attachShadow({open: true})

#### css module
通过给选择器加上特殊的属性来实现
如vue sfc中style加上scoped属性，在dom上添加data-v-XXX属性作为唯一标识
```html

<template>
  <div>
  </div>
</template>
<style scoped>
  .main {}
  /* 该类会被转为.main[data-v-XXX] */
</style>
```