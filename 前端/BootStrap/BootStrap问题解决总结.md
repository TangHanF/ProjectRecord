# 轮播区域会忽大忽小问题

```
/*解决轮播区域图片大小不一致，导致的轮播区域会忽大忽小地变化。*/
.carousel-inner > .item > img {
    min-width: 100%;
    height: 200px;
}
```

# BootstrapTable重新加载

BootstrapTable需要彻底重新加载时重新init，但是发现仍旧无效，数据不刷新，解决方式：需要调用

```javascript
//先销毁
$("#resource_table").bootstrapTable('destroy');

//再去初始化
$('#bootstrap-table').bootstrapTable({
    url: options.url,                                   // 请求后台的URL（*）
    contentType: "application/x-www-form-urlencoded",   // 编码类型
    method: 'post',                                     // 请求方式（*）
    cache: false,                                       // 是否使用缓存
    // ...
    // ...
});
},
```