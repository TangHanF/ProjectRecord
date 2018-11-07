### 1.添加新的元素 、应用 `clear：both`；

```css
.clear{clear:both; height: 0; line-height: 0; font-size: 0}
<div class="outer">
    <div class="div1">1</div>
    <div class="div2">2</div>
    <div class="div3">3</div>
    <div class="clear"></div>
</div>
```

### 2.父级div定义 `overflow: auto`（注意：是父级div也就是这里的 div.outer）

```html
.over-flow{
    overflow: auto; zoom: 1; //zoom: 1; 是在处理兼容性问题
}
<div class="outer over-flow">
    <div class="div1">1</div>
    <div class="div2">2</div>
    <div class="div3">3</div>
</div>
```

### 3.`:after` 方法：（注意：作用于浮动元素的父亲）

> ​	这种方法清除浮动是现在网上最拉风的一种清除浮动，是利用`:after`和`:before`来在元素内部插入两个元素块，从面达到清除浮动的效果。其实现原理类似于clear:both方法，只是区别在于:clear在html插入一个div.clear标签，而outer利用其伪类clear:after在元素内部增加一个类似于div.clear的效果。下面来看看其具体的使用方法：

```css
#left {
    width: 200px;
    background: red;
    height: 300px;
    float: left;
    box-sizing: border-box;
}

#right {
    width: 800px;
    background: green;
    height: 200px;
    float: left;
    box-sizing: border-box;

}



.clearFix {zoom:1;}    /*==for IE6/7*/
.clearFix :after {
     clear:both;
     content:'.';
     display:block;
     width: 0;
     height: 0;
     visibility:hidden;
}/*==for FF/chrome/opera/IE8==*/
```

```html
<div id="div1">
    <div class="clearFix">
        <div id="left">左侧</div>
        <div id="right">右侧</div>
    </div>
    <div id="footer">我是footer</div>
</div>
```

