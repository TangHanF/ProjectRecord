# 移动设备优先

移动设备优先是 Bootstrap 3 的最显著的变化。

Bootstrap 3 的设计目标是移动设备优先，然后才是桌面设备。

为了让 Bootstrap 开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 **viewport meta** 标签，如下所示：

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

*`width`* 属性控制设备的宽度。假设网站将被带有不同屏幕分辨率的设备浏览，那么将它设置为 *device-width* 可以确保它能正确呈现在不同设备上。

*`initial-scale=1.0`* 确保网页加载时，以 1:1 的比例呈现，不会有任何的缩放。

在移动设备浏览器上，通过为 **viewport meta** 标签添加 *`user-scalable=no`* 可以禁用其缩放（zooming）功能。

通常情况下，*`maximum-scale=1.0`* 与 `user-scalable=no` 一起使用。这样禁用缩放功能后，用户只能滚动屏幕，就能让您的网站看上去更像原生应用的感觉。

注意，这种方式我们并不推荐所有网站使用，还是要看您自己的情况而定！

```html
<meta name="viewport" content="width=device-width, 
                                     initial-scale=1.0, 
                                     maximum-scale=1.0, 
                                     user-scalable=no">
```

