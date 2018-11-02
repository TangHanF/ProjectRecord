可以参考：[Vue开发细节总结](quiver:///notes/0A250BFB-4ADF-4F2E-A133-AB39EC9918C7)

示例项目创建
======

要使用此模板，请使用[vue-cli构建](https://github.com/vuejs/vue-cli)项目。建议使用npm 3+以获得更高效的依赖树。

```
$ npm install -g vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm install
$ npm run dev
```

项目结构
====

```
.
├── build/                      \# webpack配置文件
│   └── ...
├── config/
│   ├── index.js                \# 主项目配置文件
│   └── ...
├── src/
│   ├── main.js                 \# 【重要】应用入口文件
│   ├── App.vue                 \# 主应用组件
│   ├── components/             \# UI组件
│   │   └── ...
│   └── assets/                 \# 模块资源存放处 (由WebPack处理)
│       └── ...
├── static/                     \# 纯静态资源 (直接复制即可)
├── test/
│   └── unit/                   \# 单元测试
│   │   ├── specs/              \# 测试规范文件
│   │   ├── eslintrc            \# eslint的配置文件，仅用于单元测试的额外设置
│   │   ├── index.js            \# 测试构建条目文件
│   │   ├── jest.conf.js        \# 使用Jest进行单元测试时的配置文件
│   │   └── karma.conf.js       \# 使用Karma进行单元测试时测试运行器配置文件
│   │   ├── setup.js            \# 在Jest运行单元测试之前运行的文件
│   └── e2e/                    \# e2e tests
│   │   ├── specs/              \# 测试规范文件
│   │   ├── custom-assertions/  \# e2e测试的自定义断言
│   │   ├── runner.js           \# test runner script
│   │   └── nightwatch.conf.js  \# test runner config file
├── .babelrc                    \# babel转码器配置文件（babel作用就是将ES6转为ES5，提高兼容性，参考：[babel配置文件](http://es6.ruanyifeng.com/#docs/intro#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6-babelrc)）
├── .editorconfig               \# indentation, spaces/tabs and similar settings for your editor
├── .eslintrc.js                \# eslint config
├── .eslintignore               \# eslint ignore rules
├── .gitignore                  \# sensible defaults for gitignore
├── .postcssrc.js               \# postcss config
├── index.html                  \# index.html template
├── package.json                \# 构建脚本和依赖项
└── README.md                   \# Default README file
```

### `build/`

此目录包含开发服务器和生产webpack构建的实际配置。通常，您不需要修改这些文件，除非您想要自定义Webpack加载器，在这种情况下您应该查看`build/webpack.base.conf.js`。

### `config/index.js`

这是主要配置文件，它公开了构建设置的一些最常见的配置选项。有关详细信息，请参阅[开发期间的API代理](http://vuejs-templates.github.io/webpack/proxy.html)和[与后端框架集成](http://vuejs-templates.github.io/webpack/backend.html)。

### `src/`

这是您的大多数应用程序代码所在的位置。如何构建此目录中的所有内容在很大程度上取决于您; 如果您使用的是Vuex，则可以参考[Vuex应用程序](http://vuex.vuejs.org/en/structure.html)的[建议](http://vuex.vuejs.org/en/structure.html)。

### `static/`

此目录是您不希望使用Webpack处理的静态资产的转义窗口。它们将直接复制到生成webpack构建资产的同一目录中。

有关详细信息，请参阅[处理静态资产](http://vuejs-templates.github.io/webpack/static.html)。

### `test/unit`

包含单元测试相关文件。有关详细信息，请参阅[单元测试](http://vuejs-templates.github.io/webpack/unit.html)

### `test/e2e`

包含e2e测试相关文件。有关更多详细信息，请参阅[端到端测试](http://vuejs-templates.github.io/webpack/e2e.html)。

### `index.html`

这是我们单页面应用程序的模板 `index.html`。在开发和构建期间，Webpack将生成资源文件，这些生成的资源文件的URL将自动注入此模板以呈现最终的HTML。

### `package.json`

包含所有构建依赖项和[构建命令](http://vuejs-templates.github.io/webpack/commands.html)的NPM包元文件。

组件的注册使用
=======

创建一个组件，并在路由加入组件，然后访问单页面应用。

**结构：**

![](https://ws3.sinaimg.cn/large/006tNbRwly1fwtkc70w6fj30kc0xsdj1.jpg)

1. 首先在“components”里面创建一个组件，例如“IView.vue”
2. 然后在“router”的index.js（默认index.js，可以是其它名称，不过import的时候就需要适当调整）路由配置里面配置组件的路由信息

App.vue
-------

```html
<!--主应用-->

<template>
  <div id="app">
    <img src="./assets/logo.png">


    <router-view/>

    <!--<div style="margin-top: 20px">-->
      <!--<router-view></router-view>-->
    <!--</div>-->
  </div>
</template>


<script>
  export default {
    name: 'App'
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
```

main.js
-------

```js
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router/myrouter.js'//可以不加js后缀
//如果router目录下有一个index.js的路由配置文件，可以直接写为： import router from './router'

import iView from 'iview';
import 'iview/dist/styles/iview.css';



Vue.config.productionTip = false;
Vue.use(iView);

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router:router,//路由
  components: {App},//在模块系统中局部注册,参考：https://cn.vuejs.org/v2/guide/components-registration.html#在模块系统中局部注册
  template: '<App/>'//模板
});

```

myrouter.js
-----------

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

import HelloWorld from '@/components/HelloWorld'
import IView from '@/components/IView.vue'//可以不加vue后缀

Vue.use(VueRouter)

export default new VueRouter({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    },
    {
      path:'/iv',
      name:'IView',
      component:IView
    }
  ]
})
```

WebPack打包部署到GitHub Page
=======================

如今我们创建一个前端项目的时候, 已经很少手动创建 index.html, main.js , main.css 这文件了, 通常我们都会选择一个前端框架, 并使用相应的 command line tool 来初始化项目.

这里笔者用 Vue 的 webpack 项目 做介绍, rect 和 angular 进行类似的配置即可.

#### 创建项目

首先我们用 vue-cli 创建一个 webpack 管理的 vue 项目 ([点我安装 vue-cli](https://github.com/vuejs-templates/webpack)),

```
vue init webpack github-page-vue-demo
```

然后我们进入项目, 看看目录结构:

![simplest demo](resources/54E093DD5DDA66B7655E956FE64D924D.png "simplest demo")

可以看到 config 目录中有三个文件:

```
config                     // 配置目录
├── dev.env.js             // 用于development模式的环境变量
├── index.js               // 用于配置 `dev` 模式和 `prod` 模式的 webpack config 文件
└── prod.env.js            // 用于product模式的环境变量
```

这里我们需要配置的就是 index.js 文件, 先看看该文件内容 (这里将不相关的代码用...略过), 其中我们需要关注的是 module.exports 的 build 属性, 我们将在这里配置 webpack build 时生成文件的路径

```
module.exports = {
  dev: {
      ...
  },

  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    ...
  }
}
```

可以看到图中主要配置了 index 文件和 assets 文件的路径. 默认执行 `yarn run build` 后 webpack 会将项目打包到项目根目录的 ./dist 文件夹, 如图:

![image-20181102113836926](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkenpuccj30sx0lcjza.jpg)

#### 修改编译配置

但是 github pages 默认只能识别项目根目录的 index 文件, 如果我们想要让 github pages 识别到我们 build 出来的文件应该怎么办呢?

你可能会想到直接将 dist 文件夹中 build 生成的文件直接复制到项目的根目录, 这确实是个办法. 但是这样的话, 我们每次 build 完, 都需要手动复制一边文件, 这无疑增加了很多重复性的工作.

我们可以通过修改默认的配置来达到项目 build 的文件直接生成到项目根目录的目的, 像这样:

```
module.exports = {
  dev: {
      ...
  },

  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../index.html'),  //之前是 '../dist/index.html'

    // Paths
    assetsRoot: path.resolve(__dirname, '../'),  // 之前是 '../dist'
    assetsSubDirectory: 'static',
    assetsPublicPath: './',    // 之前是 '/'
    ...
  }
}
```

所做的改动就是去掉了默认的 dist 目录, 并且将 assets 的引用路径从 绝对路径 改为了 \_相对路径\_.

去掉 dist 目录是为了将 build 的 target 路径改为项目根目录. 改为相对路径是因为在部署到 github pages 的时候, 我们的域名是 `https://username.github.io/repositoryName`, 也就是说我们的项目是部署在子域名上的, 如果用绝对路径会导致 assets 文件 404.

这样修改完后我们又发现一个问题: 在这样的配置下, build 结束生成的 index.html 文件会覆盖原有的 template index.html 文件, 并且根目录多了一个 static 文件夹, 很容易让人对这个文件夹的作用产生疑惑. 有没有更好的解决办法呢 ?

让我们回到 github page 的 setting 页面:
![image-20181102113928389](https://ws3.sinaimg.cn/large/006tNbRwly1fwtkfiiaqvj31030kc40t.jpg)

可以看到这里有一个选项是 `master branch /docs folder` . 当前状态是不可选的, 原因是我们的项目代码里面没有 `/docs` 目录.

这个选项的意思是 github page 可以识别我们项目中的 docs 文件夹, 并在这个文件夹中寻找 index 文件进行部署. 选中这个选项后, 我们只需要将之前 webpack 默认的 dist 文件夹改为 docs 文件夹即可, 修改后配置如下:

```
module.exports = {
  dev: {
      ...
  },

  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../docs/index.html'),  //之前是'../dist/index.html'

    // Paths
    assetsRoot: path.resolve(__dirname, '../docs'),  // 之前是 '../dist'
    assetsSubDirectory: 'static',
    assetsPublicPath: './',    // 之前是 '/'
    ...
  }
}
```

完成以上的修改后, 我们再次运行 `yarn run build`, 你会发现根目录下多了一个 docs 文件夹, 里面承载了 index 文件和 static 文件夹. 我们讲 docs 目录以及其下的文件全部加入 git 版本管理, 并 push 到 github.

再次来到 该项目的 github page setting 页面, 这时 master branch /docs folder 就变成可选中的了. 我们选中这个选项, 并保存设置.

过两分钟左右, 我们再次访问我们项目的 \_github page url\_, 就会发现项目已经部署成功了