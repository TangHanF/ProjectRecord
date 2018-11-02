在一个html页面中加入bootstrap是很方便，就是一般的将css和js文件通过Link和Script标签就行。那么在一个用vue-vli生成的前端项目中如何加入？因为框架不一样了，略微要适应一下

第一步：**脚手架生成项目**

执行命令用webpack模板生成一个名为vuestrap的项目（名字任意）

    vue init webpack vuestrap

在出现的各提示选项中（这些选项都随意）。

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

    ? Project name vuestrap
    ? Project description A Vue.js project
    ? Author SmileHong0121 <fengqingyuhou@gmail.com>
    ? Vue build standalone
    ? Install vue-router? Yes
    ? Use ESLint to lint your code? Yes
    ? Pick an ESLint preset Standard
    ? Setup unit tests with Karma + Mocha? No
    ? Setup e2e tests with Nightwatch? No

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

选项选完，项目也就生成了，执行命令，安装脚手架创建的组件

    npm install

第二步：**安装jquery**

bootstrap是依赖jquery的，所以就先装上jquery，这里用的版本是1.11.3。

稍后在配置的时候，是以webpack插件的方式进行打包，所以这里直接用npm进行安装，因为插件方式打包的组件都是require进来的。

执行命令，并保存到package.json中

    npm install jquery@1.11.3 --save-dev

注：如果想查看npm上jquery有哪些版本，可以执行命令：

    npm view jquery versions

第三步：安装Bootstrap

这里用的版本是3.3.0。执行命令，即可安装完成

    npm install bootstrap@3.3.0 --save-dev

第四步：**配置jquery**

将jquery以插件打包，需要为webpack的plugins进行插件设置。

在build/webpack.base.conf.js文件中，在整个配置对象的末尾增加plugins配置。

在webpack.base.conf.js中的配置项，可以在dev和build出来的pro版本中都有效。

下面的配置其实就是变量名的真正指向设置，这样，在页面中对jquery的各种名字的调用就会有效，否则bootstrap跑不起来。

在这个文件顶部先引入webpack

    var webpack=require('webpack');

![](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkc4pnydj310605z74z.jpg)

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

    plugins: [ new webpack.ProvidePlugin({ $: "jquery", jQuery: "jquery", "windows.jQuery": "jquery" }) ],

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

![](https://ws3.sinaimg.cn/large/006tNbRwly1fwtkc58qk5j31060cbaaw.jpg)

 第五步：**引用bootstrap**

在src/main.js文件的顶部加入如下对bootstrap主要文件的引用，注意这里的路径，不在是从src/assets加载，而是换成了从node_modules加载。

    import 'bootstrap/dist/css/bootstrap.min.css' import 'bootstrap/dist/js/bootstrap.min.js'

![](https://ws1.sinaimg.cn/large/006tNbRwly1fwtkc61xzcj310d084t9l.jpg)

第六步：**配置bootstrap**

因为bootstrap除了js和css文件外，还有字体文件需要一并打包，默认生成的webpack.base.conf.js中的moudle->rules设定中都已经包含对字体文件的打包设置，所以无需修改，很人性啊。

第七步：**验证页面**

就在App.vue中写一个页面，放一个panel，button，modal。

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

```html
<template>
  <div id="app">
    <div class='container'>
      <div class='row'>
        <div class='col-lg-4'>
          <h1>demo</h1>
        </div>

        <div class='col-lg-8'>
          <div class='panel panel-default' style='min-width:500px;box-shadow:4px 4px 10px #888888;'>
            <div class="panel-heading">
              <button id='btnCreate'>
                <span class="glyphicon glyphicon-plus"></span>
              </button>
              <span>&nbsp;&nbsp;&nbsp;</span>
            </div>
            <div class="panel-body">
              <div style='float: left;width:100%'>

                <button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal"> Launch demo modal </button>

                <!-- Modal -->
                <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
                  <div class="modal-dialog" role="document">
                    <div class="modal-content">
                      <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                        <h4 class="modal-title" id="myModalLabel">Modal title</h4>
                      </div>
                      <div class="modal-body"> ... </div>
                      <div class="modal-footer">
                        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save changes</button>
                      </div>
                    </div>
                  </div>
                </div>

              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script> export default { name: 'app' } </script>

<style> #app { margin-top: 60px;
  }
</style>
```

[![复制代码](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkc3qsdag300k00k07b.gif)]( "复制代码")

写完后，执行命令，运行效果。

    npm run dev

![](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkc6iggvj31fj0cpgmj.jpg)