之前通过webpack把bootstrap css 样式引入到模板中，但是注意到的是把全部bootstrap css样式加载进来，但是当前的template中只有简单的些button/div/img/h1/等，而且这些元素只用到了一小部分样式，没有必要把全部的样式都加载进模板，所以需要改进，怎么办呢，PurifyCSS Plugin可以做到只加载当前页面所需要的样式。 
先安装：

```
npm i -D purifycss-webpack purify-css
```

安装完成后当前版本是：

```
"purify-css": "^1.2.5",
"purifycss-webpack": "^0.7.0"
```

接下来去webpack.config.js中去配置：

```javascript
const glob = require('glob');
const PurifyCSSPlugin = require('purifycss-webpack');
```

再把purifyCSSPlugin添加到plugins对象中：

```javascript
new PurifyCSSPlugin({
    // Give paths to parse for rules. These should be absolute! 
    paths: glob.sync(path.join(__dirname, './src/*.html')),
}) //src目录下的所有html模板都会被影响
```

之前没有优化前的bootstrap.css的大小是121KB：

![](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkc2kf77j31d00ug43x.jpg)

优化完之后是11KB：

![](https://ws1.sinaimg.cn/large/006tNbRwly1fwtkc3a6c0j31d00ugn2k.jpg)

打开之后也可以看到它里面也只包含了当前页面元素的css样式。假如现在在模板中加入一个dropdwon:

```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Dropdown button
  </button>
  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
    <a class="dropdown-item" href="#">Action</a>
    <a class="dropdown-item" href="#">Another action</a>
    <a class="dropdown-item" href="#">Something else here</a>
  </div>
</div>

```

从编译后bootstrap.css中可以看到关于dropdown的样式也被加载进来，也就是它会根据页面中实际的元素来加载相对应的css样式。