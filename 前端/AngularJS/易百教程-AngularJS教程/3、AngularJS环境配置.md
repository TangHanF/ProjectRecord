在本章中，我们将讨论如何设置AngularJS库在Web应用程序开发中使用。我们还将简要地研究了目录结构和它的内容。

当打开链接https://angularjs.org/，会看到有两个选项下载AngularJS库：

![](https://ws4.sinaimg.cn/large/006tNc79ly1fsbt6ys8e4j30er07amxp.jpg)

- GitHub下载 - 单击此按钮去到GitHub，并获得所有最新的脚本。

- 下载 - 或点击此按钮，屏幕下方会看到：

  ![](https://ws3.sinaimg.cn/large/006tNc79ly1fsbt779xq0j30ez09haao.jpg)

  此屏幕给出了使用角JS如下的各种选项：

  - 下载和本地主机文件
    - 有两种不同的选择：旧版和最新。名字本身是自我说明。旧版版本已经低于1.2.x版本和最新为1.3.x版。
    - 我们也可以使用缩小，无压缩或压缩版本。
  - CDN访问：也可以使用CDN。在CDN会给世界各地的访问，在这种情况下，谷歌的主机区域性数据中心。这意味着使用CDN的移动主机的文件从自己的服务器到一系列外部因素的责任。这也提供了一个优点，即如果访问者你的网页已经下载来自相同的CDN AngularJS副本，它不必被重新下载。

> 在本教程中使用CDN版本库。

## 例子

现在让我们使用AngularJS库编写一个简单的例子。创建一个HTML文件 myfirstexample.html 如下：

```html
<!doctype html>
<html>
   <head>
      <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.0-beta.17/angular.min.js"></script>
   </head>
   <body ng-app="myapp">
      <div ng-controller="HelloController" >
         <h2>Welcome {{helloTo.title}} to the world of Yiibai!</h2>
      </div>
      <script>
         angular.module("myapp", [])
         .controller("HelloController", function($scope) {
            $scope.helloTo = {};
            $scope.helloTo.title = "AngularJS";
         });
      </script>
   </body>
</html>
```

下面的章节详细描述了上面的代码：

### 包括AngularJS

我们已经包含了AngularJS的JavaScript文件中的HTML页面，所以我们可以使用AngularJS：

```html
<head>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.2.15/angular.min.js"></script>
</head>
```

检查AngularJS的最新版本在其官方网站。

### 指向AngularJS应用

接下来，我们告诉一下HTML的一部分包含AngularJS应用。这可以通过将ng-app属性到AngularJS应用程序的根目录下的HTML元素。可以将它添加到HTML元素或body元素，如下所示：

```html
<body ng-app="myapp">
</body>
```

### 视图

这部分的视图：

```html
<div ng-controller="HelloController" >
   <h2>Welcome {{helloTo.title}} to the world of Yiibai!</h2>
</div>
```

ng-controller 告诉AngularJS什么是控制器和视图。 helloTo.title告诉AngularJS编写名为helloTo.title的HTML在这个位置的“model”的值。

### 控制器

控制器的部分是：

```html
<script>
   angular.module("myapp", [])
   .controller("HelloController", function($scope) {
      $scope.helloTo = {};
      $scope.helloTo.title = "AngularJS";
    });
</script> 
```

此代码先注册名为HelloController中的名为MyApp角模块控制器的功能。我们将学习更多有关在各自的章节[模块](http://www.yiibai.com/angularjs/angularjs_modules.html)和[控制器](http://www.yiibai.com/angularjs/angularjs_controllers.html)。控制器功能被登记在经由angular.module（...）的角。controller（...）函数调用。 

传递给控制器函数的$scope参数模型。控制器功能增加了helloTo的JavaScript对象，该对象中加上一个标题字段。

### 执行

将以上代码保存为myfirstexample.htmll在任何浏览器中打开它。会看到如下的输出：

 ![](https://ws3.sinaimg.cn/large/006tNc79ly1fsbt8555plj30fg01adfu.jpg)

 

当页面在浏览器中加载时，下面的事件发生：

- HTML文档被加载到浏览器中，并且由浏览器进行计算。 AngularJS JavaScript文件被加载，角全局对象被创建。接下来，JavaScript的一个注册控制器功能被执行。
- AngularJS通过HTML扫描，以寻找AngularJS应用程序和视图。一旦视图的找到，它连接了视图到对应的控制器函数。
- 接下来AngularJS执行控制函数。然后，它呈现与填充控制器模型数据视图。页面现在已准备就绪。

 