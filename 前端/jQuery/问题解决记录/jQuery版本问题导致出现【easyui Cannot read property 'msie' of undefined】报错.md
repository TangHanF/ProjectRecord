## 报错信息
> easyui Cannot read property 'msie' of undefined

## 错误分析
> `$.browser`的api从jQuery1.9开始就正式废除，js代码里只要用到`$.browser`就会报这个错

## 解决方案

### 方案一：使用`jQuery Migrate`插件
该插件能够自动恢复那些在最新版本之后被废弃的API，从而让已有的js应用层代码无须改动就能和最新的jQuery库一起正常运行

[点击此处下载jQuery Migrate插件（右击另存即可）](http://code.jquery.com/jquery-migrate-1.2.1.js)

**下载完成之后在引用jQuery js的地方之后加上一行对jQuery Migrate js文件的引用即可**，例如：
``` html
<script src="http://code.jquery.com/jquery-1.10.2.js"></script>
<script src="http://code.jquery.com/jquery-migrate-1.2.1.js"></script>
```

### 方案二：加入代码

> 注意，以下代码的加载顺序在jQuery文件之后，$.browser的代码之前

``` javascript
jQuery.browser = {};
(function() {
    jQuery.browser.msie = false;
    jQuery.browser.version = 0;
    if (navigator.userAgent.match(/MSIE ([0-9]+)./)) {
        jQuery.browser.msie = true;
        jQuery.browser.version = RegExp.$1;
    }
})();

```