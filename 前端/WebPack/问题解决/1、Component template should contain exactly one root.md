Component template should contain exactly one root

组件模板应该只包含一个根

如下代码是错误的，会提示以上错误，需要添加一个根元素：

```html
<template>
    <Button>Default</Button>
    <Button type="primary">{{Primary}}</Button>
    <Button type="dashed">{{Dashed}}</Button>
    <Button type="text">{{Text}}</Button>
    <br><br>
    <Button type="info">{{Info}}</Button>
    <Button type="success">{{Success}}</Button>
    <Button type="warning">{{Warning}}</Button>
    <Button type="error">{{Error}}</Button>
</template>
```

需要修改为：

```html
<template>
  <div >
    <Button>Default</Button>
    <Button type="primary">{{Primary}}</Button>
    <Button type="dashed">{{Dashed}}</Button>
    <Button type="text">{{Text}}</Button>
    <br><br>
    <Button type="info">{{Info}}</Button>
    <Button type="success">{{Success}}</Button>
    <Button type="warning">{{Warning}}</Button>
    <Button type="error">{{Error}}</Button>
  </div>
</template>
```

可参考Vue说明：[单个根元素](https://cn.vuejs.org/v2/guide/components.html#%E5%8D%95%E4%B8%AA%E6%A0%B9%E5%85%83%E7%B4%A0)