# AngularJS是什么?

AngularJS是一个开源Web应用程序框架。它最初是由MISKO Hevery和Adam Abrons于2009年开发。现在是由谷歌维护。它的最新版本是1.3.14。

AngularJS在它的[官方文档](https://docs.angularjs.org/guide/introduction) 中定义如下：

> AngularJS is a structural framework for dynamic web apps. It lets you use HTML as your template language and lets you extend HTML's syntax to express your application's components clearly and succinctly. Angular's data binding and dependency injection eliminate much of the code you currently have to write. And it all happens within the browser, making it an ideal partner with any server technology.

## 特性

- AngularJS是一个功能强大的基于JavaScript开发框架用于创建富互联网应用(RIA)。
- AngulajJS为开发者提供的选项(使用JavaScript)在一个干净的MVC(模型 - 视图 - 控制器)的方式来编写客户端应用程序。
- AngularJS写的应用都是跨浏览器兼容。AngularJS使用JavaScript代码自动处理适应每种浏览器。
- AngularJS是开源的，完全免费的，并且由数千名世界各地的开发者开发维护。它是根据Apache许可证2.0版许可发布。

总体来说，AngularJS是一个用来构建大型应用，高性能的Web应用程序的框架，同时使它们易于维护。

## 核心特征

以下是AngularJS中最重要的核心功能：

- **数据绑定:** 模型和视图组件之间的数据自动同步。
- **适用范围:** 这些对象参考模型。它们充当控制器和视图之间的胶水。
- **控制器:** 这些Javascript函数绑定到特定的范围。
- **服务:** AngularJS配有多个内置服务，例如 $http 可作为一个XMLHttpRequest请求。这些单一对象在应用程序只实例化一次。
- **过滤器:** 从一个数组的条目中选择一个子集，并返回一个新的数组。
- **指令:** 指令是关于DOM元素标记(如元素，属性，CSS等等)。这些可以被用来创建作为新的，自定义部件的自定义HTML标签。AngularJS设有内置指令(如：ngBind，ngModel...)
- **模板:**这些符合从控制器和模型信息的呈现的视图。这些可以是单个文件(如index.html)，或使用“谐音”在一个页面多个视图。
- **路由:** 它是切换视图的概念。
- **模型视图:** MVC是一个设计模式将应用划分为不同的部分(称为模型，视图和控制器)，每个都有不同的职责。 AngularJS并没有传统意义上的实现MVC，而是更接近于MVVM(模型 - 视图 - 视图模型)。 AngularJS团队将它作为模型视图。
- **深层链接:** 深层链接，可以使应用程序状态进行编码在URL中而能够添加到书签。应用程序可从URL恢复到相同的状态。
- **依赖注入:** AngularJS有一个内置的依赖注入子系统，开发人员通过使应用程序从而更易于开发，理解和测试。

## 概念

下图描述了AngularJS，我们将详细的后续章节讨论一些重要的部分。
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH1255S48.jpg)

## AngularJS的优点

- AngularJS提供一个非常干净和维护的方式来创造单页的应用。
- AngularJS提供数据绑定功能在HTML中，从而给用户提供丰富和响应的体验
- AngularJS代码可进行单元测试。
- AngularJS使用依赖注入和利用关注点分离。
- AngularJS提供了可重用的组件。
- 使用AngularJS，开发人员编写更少的代码，并获得更多的功能。
- 在AngularJS中，视图都是纯HTML页面，并用JavaScript编写控制器做业务处理。

AngularJS应用程序可以在所有主要的浏览器和智能手机，包括Android和iOS系统的手机/平板电脑上运行。

## AngulaJS的缺点

虽然AngularJS自带很多优点，但我们应该考虑以下几点(缺点)：

- **不安全：**因为只是JavaScript一种框架，由AngularJS编写的应用程序是不安全的。服务器端身份验证和授权是必须用来保证应用程序的安全。
- **不可降解：**如果应用程序的用户禁用JavaScript，那最后用户看到的只是基本页面，仅此而已。

## AngularJS组件

AngularJS框架可分为以下三个主要部分组成：

- **ng-app :** 指令定义和链接AngularJS应用程序到HTML。
- **ng-model :** 指令绑定AngularJS应用数据的值到HTML输入控件。
- **ng-bind :** 该指令绑定AngularJS应用程序数据到HTML标签。

# AngularJS环境设置

在本章中，我们将讨论如何建立AngularJS库在Web应用程序开发中使用。我们还将简要地学习目录结构和它的内容。

打开链接<https://angularjs.org/>(打不开可能需要翻墙)，会看到有两个下载AngularJS库的选项：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH12H39D.jpg)

- View on GitHub- 单击此按钮跳到GitHub，并获得所有最新的脚本。

- Download- 或者点击此按钮，会看到屏幕如下：
  ![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH12RV28.jpg)

  

  此屏幕给出了使用AngularJS如下多种选择：

  - Downloading and hosting files locally
    - 有两种不同的选择：旧版和最新版。旧版是版本低于1.2.x版本，最新是1.3.x版本。
    - 我们也可以使用缩小，非压缩或压缩版本。
  - CDN access: 也可以使用一个CDN。CDN全世界可访问，它放在谷歌主机区域性数据中心。  这也提供了一个优点，即如果访问者的网页已经从相同的CDN 下载了AngularJS的副本，它不必再重新下载。

> 在本教程中我们使用的是CDN版本库

## 示例

现在让我们使用AngularJS库编写一个简单的例子。让我们创建一个HTML文件 first-angular.html 如下：

```html
<!doctype html>
<html>
   <head>
      <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.3.0-beta.17/angular.min.js"></script>
   <title>第一个AngularJS程序</title>
   </head>
   <body ng-app="myapp">
      <div ng-controller="HelloController" >
         <h2>你好 ！第一个{{helloTo.title}}程序示例</h2>
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

下面的章节详细描述上面的代码：

### 包括AngularJS

我们已经包括了AngularJS的JavaScript文件到HTML页面中，所以我们可以用AngularJS：

```html
<head>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
</head>
```

在其官方网站检查AngularJS的最新版本。

### 指向AngularJS应用程序

接下来我们指示HTML的哪一部分包含了AngularJS应用程序。这可以通过ng-app属性到AngularJS应用程序的根HTML元素。可以把它添加到HTML元素或body元素，如下所示：

```html
<body ng-app="myapp">
</body>
```

### 视图

这是视图的一部分：

```html
<div ng-controller="HelloController" >
   <h2>Welcome {{helloTo.title}} to the world of Yiibai tutorials!</h2>
</div>
```

ng-controller 告诉AngularJS什么控制器使用在视图中。helloTo.title告诉AngularJS将命名helloTo.title的值写入到HTML的“model”中。

### 控制器

这里是控制器部分：

```html
<script>
   angular.module("myapp", [])
   .controller("HelloController", function($scope) {
      $scope.helloTo = {};
      $scope.helloTo.title = "AngularJS";
    });
</script>
```

此代码注册一个名为HelloController的控制器功能，在myapp模块。 我们将学习更多关于它们在各自的模块和控制器章节。控制器函数注册在Angular中，通过angular.module(...).controller(...) 的函数来调用。

传递给控制器函数的$scope参数是模型。控制器函数增加了helloTo的 JavaScript对象，并在该对象它增加了一个标题字段。

### 执行

将以上代码保存为  first-angular.html ，并在浏览器中打开它。会看到如下的输出：

![](https://ws3.sinaimg.cn/large/006tNc79ly1fsbt3ji8l9j30gx06zaar.jpg) 

当页面在浏览器中加载，输出下面的结果：

- HTML文档加载到浏览器，并且由浏览器进行评估计算。AngularJS JavaScript文件被加载，Angular 全局对象被创建。接下来，JavaScript一个注册控制器的函数被执行。
- 接下来AngularJS通过HTML扫描，以寻找AngularJS应用程序和视图。当视图的定位后，它连接视图到对应的控制器函数。
- 接下来，AngularJS执行控制器函数。然后，它呈现通过控制器模型数据来自填充的视图。此时网页已准备就绪。

# AngularJS MVC 架构

模型视图控制器(Model View Controller)或MVC，因为它是俗称，是一种Web应用程序开发设计模式。模型-视图-控制器模式由以下三部分组成：

- **Model** - 是一个最低水平负责维护数据的模式。
- **View** - 这是负责显示所有或一部分的数据到用户。
- **Controller** - 软件代码控制模型和视图之间的相互作用。

MVC是很流行的，因为它从用户界面层和支持分离关注隔离了应用逻辑。在这里，控制器接收应用程序的所有请求，然后使用Model，以准备视图需要的数据。然后视图使用控制器准备的数据，以产生一个最终的像样响应的数据输出。 MVC的抽象图形可以表示如下。
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH1303O17.jpg)

## 模型

模型负责管理应用程序的数据。它响应从视图请求，同时也从控制器响应指令到自我更新。

## 视图

在一个特定的格式的呈现数据，由控制器决定呈现数据触发。 它们都是基于脚本的模板系统，如JSP，ASP，PHP也很容易使用AJAX技术来集成。

## 控制器

控制器负责响应于用户输入并执行交互数据模型对象。控制器接收输入，并验证输入，然后执行修改数据模型的业务操作的状态。

AngularJS是一个基于MVC的框架。在接下来的章节中，让我们看看AngularJS如何使用MVC方法论。

# AngularJS 表达式

表达式用于应用程序绑定数据到HTML。表达式编写在双括号就如：`{{ expression}}`. **表达式中的行为方式与 ng-bind 指令相同**。AngularJS应用表达式是纯JavaScript表达式和输出正在使用的数据。

## 使用数字

```html
<p>Expense on Books : {{cost * quantity}} Rs</p>
```

## 使用字符串

```html
<p>Hello {{student.firstname + " " + student.lastname}}!</p>
```

## 使用对象

```html
<p>Roll No: {{student.rollno}}</p>
```

## 使用数组

```html
<p>Marks(Math): {{marks[3]}}</p>
```

## 示例

下面的例子将展示上述所有表达式。

sampleAngularJS.html

```html
<html>
<title>AngularJS 表达式</title>
<body>
<h1>Sample Application</h1>
<div ng-app="" ng-init="quantity=1;cost=30; student={firstname:'李',lastname:'刚',rollno:101};marks=[82,91,78,77,64]">
   <p>Hello {{student.firstname + " " + student.lastname}}!</p>   
   <p>Expense on Books : {{cost * quantity}} Rs</p>
   <p>Roll No: {{student.rollno}}</p>
   <p>Marks(Math): {{marks[3]}}</p>
</div>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
</body>
</html>
```

##  输出结果

在浏览器中打开：sampleAngularJS.html， 看到结果如下：

![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH131111P.png)

#  AngularJS 控制器

- AngularJS应用主要依赖于控制器来控制数据流在应用程序中

- 控制器使用 `ng-controller` 指令定义。控制器是一个包含属性/属性和函数的JavaScript对象。
- **每个控制器接受$scope作为参数引用到应用程序/模块**，由控制器来控制。

```html
<div ng-app="" ng-controller="studentController">
...
</div>
```

在这里，我们采用 ng-controller 指令声明控制器studentController。作为下一个步骤，我们将定义 studentController 如下：

```html
<script>
function studentController($scope) {
   $scope.student = {
      firstName: "李",
      lastName: "四",
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
}
</script>
```

- studentController定义一个以 $scope 作为参数的JavaScript对象。
- $scope表示应用程序，它使用studentController对象。
- $ scope.student是studentController对象的属性。
- firstName 和 lastName 是 $scope.student 对象的两个属性。我们已经为它们设置了缺省值。
- fullName是 $scope.student 对象的函数，其任务是返回合并后的名字。
- 在fullName函数中我们得到了 student 对象，然后返回合并后的名字。
- 我们还可以定义控制器对象在单独的JS文件，并参考(引入)该文件在HTML页面。

现在，我们可以在studentController使用ng-model或表达式来获取学生的属性。

```html
Enter first name: <input type="text" ng-model="student.firstName"><br>
Enter last name: <input type="text" ng-model="student.lastName"><br>
<br>
You are entering: {{student.fullName()}}
```

- 绑定 student.firstName 和 student.lastname 两个输入框。
- 绑定student.fileName()到HTML。
- 现在，只要输入名字和姓氏在输入框中，可以看到全名(fullname)自动更新。

## 示例

下面的例子将展示控制器的使用。

testAngularJS.html

```html
<html>
<head>
<title>Angular JS Controller</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
</head>
<body>
<h2>AngularJS应用示例</h2>
<div ng-app="mainApp" ng-controller="studentController">

Enter first name: <input type="text" ng-model="student.firstName"><br><br>
Enter last name: <input type="text" ng-model="student.lastName"><br>
<br>
您输入的名字是: {{student.fullName()}}
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope) {
   $scope.student = {
      firstName: "李",
      lastName: "刚",
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
</script>
</body>
</html>
```

## 输出

在浏览器中打开：textAngularJS.html ，将看以下的结果：

![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH13200964.png)

# AngularJS 过滤器

过滤器用来改变修改的数据，并可以在表达式或使用管道字符指令来过滤。以下是常用的过滤器的列表。

| S.No. | 名称      | 描述                               |
| ----- | --------- | ---------------------------------- |
| 1     | uppercase | 转换文本为大写文字。               |
| 2     | lowercase | 转换文本为小写文字。               |
| 3     | currency  | 以货币格式格式化文本。             |
| 4     | filter    | 过滤数组到根据提供标准的一个子集。 |
| 5     | orderby   | 排序基于提供标准的数组。           |

## 大写过滤器

添加大写字母过滤器使用管道符表达式。在这里，我们添加大写过滤器中的所有字母为大写，并打印学生的名字。

```html
Enter first name:<input type="text" ng-model="student.firstName">
Enter last name: <input type="text" ng-model="student.lastName">
Name in Upper Case: {{student.fullName() | uppercase}}
```

## 小写过滤器

添加小写过滤器使用管道符表达式。在这里，我们添加小写过滤器全部以小写字母打印学生的名字。

```html
Enter first name:<input type="text" ng-model="student.firstName">
Enter last name: <input type="text" ng-model="student.lastName">
Name in Upper Case: {{student.fullName() | lowercase}}
```

## 货币过滤器

添加货币过滤器使用管道符返回数的表达式。在这里，我们添加货币过滤器使用货币格式的打印费用。

```html
Enter fees: <input type="text" ng-model="student.fees">
fees: {{student.fees | currency}}
```

## 过滤过滤器

若要仅显示必修科目，我们使用subjectName作为过滤器。

```html
Enter subject: <input type="text" ng-model="subjectName">
Subject:
<ul>
  <li ng-repeat="subject in student.subjects | filter: subjectName">
    {{ subject.name + ', marks:' + subject.marks }}
  </li>
</ul>
```

## 排序过滤器

由标记来排序科目，我们使用的OrderBy标记。

```html
Subject:
<ul>
  <li ng-repeat="subject in student.subjects | orderBy:'marks'">
    {{ subject.name + ', marks:' + subject.marks }}
  </li>
</ul>
```

## 示例

下面的例子将展示上述所有过滤器。

testAngularJS.html

```html
<html>
<head>
<title>Angular JS Filters</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
</head>
<body>
<h2>AngularJS过滤器应用示例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<table border="0">
<tr><td>Enter first name:</td><td><input type="text" ng-model="student.firstName"></td></tr>
<tr><td>Enter last name: </td><td><input type="text" ng-model="student.lastName"></td></tr>
<tr><td>Enter fees: </td><td><input type="text" ng-model="student.fees"></td></tr>
<tr><td>Enter subject: </td><td><input type="text" ng-model="subjectName"></td></tr>
</table>
<br/>
<table border="0">
<tr><td>Name in Upper Case: </td><td>{{student.fullName() | uppercase}}</td></tr>
<tr><td>Name in Lower Case: </td><td>{{student.fullName() | lowercase}}</td></tr>
<tr><td>fees: </td><td>{{student.fees | currency}}</td></tr>
<tr><td>Subject:</td><td>
<ul>
   <li ng-repeat="subject in student.subjects | filter: subjectName |orderBy:'marks'">
      {{ subject.name + ', marks:' + subject.marks }}
   </li>
</ul>
</td></tr>
</table>
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope) {
   $scope.student = {
      firstName: "李",
      lastName: "Gang",
      fees:500,
      subjects:[
         {name:'物理',marks:70},
         {name:'化学',marks:80},
         {name:'数学',marks:65},
         {name:'外语', marks:87}
      ],
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
</script>
</body>
</html>
```

## 输出结果

在浏览器中打开：textAngularJS.html，看到结果如下： 

![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH13251335.png)

#  AngularJS 表格

表中的数据本质上是通常可重复。 ng-repeat 指令可轻松用于绘制表格。下面的例子是使用 ng-repeat 指令来绘制表格。

```html
<table>
   <tr>
      <th>Name</th>
      <th>Marks</th>
   </tr>
   <tr ng-repeat="subject in student.subjects">
      <td>{{ subject.name }}</td>
      <td>{{ subject.marks }}</td>
   </tr>
</table>
```

表可以使用CSS样式设置样式。

```html
<style>
table, th , td {
   border: 1px solid grey;
   border-collapse: collapse;
   padding: 5px;
}
table tr:nth-child(odd) {
   background-color: #f2f2f2;
}
table tr:nth-child(even) {
   background-color: #ffffff;
}
</style>
```

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html 

文件内容：

```html
<html>
<head>
<title>AngularJS表格示例</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
<style>
table, th , td {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f2f2f2;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
</head>
<body>
<h2>AngularJS 表格应用示例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<table border="0">
<tr><td>姓:</td><td><input type="text" ng-model="student.firstName"></td></tr>
<tr><td>名: </td><td><input type="text" ng-model="student.lastName"></td></tr>
<tr><td>名字: </td><td>{{student.fullName()}}</td></tr>
<tr><td>科目:</td><td>
<table>
   <tr>
      <th>名字</th>
      <th>标记</th>
   </tr>
   <tr ng-repeat="subject in student.subjects">
      <td>{{ subject.name }}</td>
      <td>{{ subject.marks }}</td>
   </tr>
</table>
</td></tr>
</table>
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope) {
   $scope.student = {
      firstName: "周",
      lastName: "杰伦",
      fees:500,
      subjects:[
         {name:'物理',marks:73},
         {name:'化学',marks:90},
         {name:'数学',marks:68},
		 {name:'英文',marks:85},
		 {name:'生物',marks:77}
      ],
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
</script>
</body>
</html>
```

## 输出结果

在浏览器中打开：textAngularJS.html ，看到结果如下：

 

#  AngularJS HTML DOM

下面的指令可用于绑定应用程序数据到HTML DOM元素的属性。

| S.No. | 名称        | 描述                        |
| ----- | ----------- | --------------------------- |
| 1     | ng-disabled | 禁用给定的控制              |
| 2     | ng-show     | 显示了一个给定的控制        |
| 3     | ng-hide     | 隐藏一个给定的控制          |
| 4     | ng-click    | 表示一个AngularJS click事件 |

## ng-disabled 指令

添加ng-disabled属性到一个HTML按钮，并把它传递模型。绑定模型到复选框，来看看变化。

```html
<input type="checkbox" ng-model="enableDisableButton">Disable Button
<button ng-disabled="enableDisableButton">Click Me!</button>
```

## ng-show 指令

添加 ng-show 属性到HTML按钮，并把它传递到模型。该模型绑定复选框。

```html
<input type="checkbox" ng-model="showHide1">Show Button
<button ng-show="showHide1">Click Me!</button>
```

## ng-hide 指令

添加 ng-hide 属性到HTML按钮，并把它传递模型。该模型绑定复选框。

```html
<input type="checkbox" ng-model="showHide2">Hide Button
<button ng-hide="showHide2">Click Me!</button>
```

## ng-click 指令

添加ng-click属性到一个HTML按钮，更新模型。绑定模型到HTML如下所示。

```html
<p>Total click: {{ clickCounter }}</p></td>
<button ng-click="clickCounter = clickCounter + 1">Click Me!</button>
```

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html

```html
<html>
<head>
<title>AngularJS HTML DOM 示例</title>
</head>
<body>
<h2>AngularJS HTML DOM 应用示例</h2>
<div ng-app="">
<table border="0">
<tr>
   <td><input type="checkbox" ng-model="enableDisableButton">Disable Button</td>
   <td><button ng-disabled="enableDisableButton">点击我!</button></td>
</tr>
<tr>
   <td><input type="checkbox" ng-model="showHide1">显示按钮</td>
   <td><button ng-show="showHide1">Click Me!</button></td>
</tr>
<tr>
   <td><input type="checkbox" ng-model="showHide2">隐藏按钮</td>
   <td><button ng-hide="showHide2">Click Me!</button></td>
</tr>
<tr>
   <td><p>Total click: {{ clickCounter }}</p></td>
   <td><button ng-click="clickCounter = clickCounter + 1">点击我!</button></td>
</tr>
</table>
</div>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
</body>
</html>
```

## 输出结果

在浏览器中打开：textAngularJS.html ，看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH1342U93.png)

 

#  AngularJS 模块

AngularJS支持模块化方法。模块用于单独的逻辑表示服务，控制器，应用程序等。为保持代码简洁，我们在单独的 js 文件中定义模块，并将其命名为 module.js文件。 在这个例子中，我们要创建两个模块。

- **应用模块** - 控制器用于初始化应用程序。
- **控制器模块** - 用于定义控制器。

## 应用模块

mainApp.js

```html
var mainApp = angular.module("mainApp", []);
```

在这里，我们声明了使用 angular.module 函数的应用程序mainApp模块。我们已经传递一个空数组给它。这个数组通常包含依赖模块。

## 控制器模块

studentController.js

```html
mainApp.controller("studentController", function($scope) {
   $scope.student = {
      firstName: "Mahesh",
      lastName: "Parashar",
      fees:500,
      subjects:[
         {name:'Physics',marks:70},
         {name:'Chemistry',marks:80},
         {name:'Math',marks:65},
         {name:'English',marks:75},
         {name:'Hindi',marks:67}
      ],
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
```

在这里，我们声明了使用 mainApp.controller 函数的一个控制器 studentController 模块。

## 使用模块

```html
<div ng-app="mainApp" ng-controller="studentController">
..
<script src="mainApp.js"></script>
<script src="studentController.js"></script>
```

这里我们使用 ng-app 指令和控制器使用 ng-controller 指令的应用模块。我们已经在主HTML页面导入 mainApp.js 和 studentController.js。

## 实例

下面的例子将展示上述所有模块。

testAngularJS.html

```html
<html>
<head>
<title>Angular JS 模块实例</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
<script src="mainApp.js"></script>
<script src="studentController.js"></script>
<style>
table, th , td {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f2f2f2;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
</head>
<body>
<h2>AngularJS 模块应用实例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<table border="0">
<tr><td>姓:</td><td><input type="text" ng-model="student.firstName"></td></tr>
<tr><td>名: </td><td><input type="text" ng-model="student.lastName"></td></tr>
<tr><td>姓名: </td><td>{{student.fullName()}}</td></tr>
<tr><td>科目:</td><td>
<table>
   <tr>
      <th>名字</th>
      <th>标记</th>
   </tr>
   <tr ng-repeat="subject in student.subjects">
      <td>{{ subject.name }}</td>
      <td>{{ subject.marks }}</td>
   </tr>
</table>
</td></tr>
</table>
</div>
</body>
</html>
```

mainApp.js

```javascript
var mainApp = angular.module("mainApp", []);
```

studentController.js

```javascript
mainApp.controller("studentController", function($scope) {
   $scope.student = {
      firstName: "周",
      lastName: "杰伦",
      fees:500,
      subjects:[
         {name:'物理',marks:78},
         {name:'化学',marks:82},
         {name:'语文',marks:68},
         {name:'外语',marks:79},
         {name:'Java',marks:87}
      ],
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
```

## 输出结果

在浏览器中打开 textAngularJS.html; 看到的结果如下所示：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH13600602.png)

 

# AngularJS表单

AngularJS丰富表格填写和验证。 我们可以用ng-click来处理AngularJS点击按钮，使用$dirty和$invalid 来做验证。使用 novalidate 以及表单来声明禁止浏览器做特定的验证。表单控件大量使用Angular事件。让我们首先快速浏览一下事件。

## 事件

AngularJS提供可与HTML控件相关联的多个事件。例如ng-click通常与按钮相关联。下面是支持Angular JS事件。

- ng-click
- ng-dbl-click
- ng-mousedown
- ng-mouseup
- ng-mouseenter
- ng-mouseleave
- ng-mousemove
- ng-mouseover
- ng-keydown
- ng-keyup
- ng-keypress
- ng-change

## ng-click

表格的复位数据上使用 on-click 指令。

```html
<input name="firstname" type="text" ng-model="firstName" required>
<input name="lastname" type="text" ng-model="lastName" required>
<input name="email" type="email" ng-model="email" required>
<button ng-click="reset()">Reset</button>
<script>
   function studentController($scope) { 
      $scope.reset = function(){
         $scope.firstName = "Mahesh";
         $scope.lastName = "Parashar";
         $scope.email = "MaheshParashar@yiibai.com";
  }   
   $scope.reset();
}
</script>
```

## 验证数据

以下可用于跟踪错误。

- **$dirty** - 状态指示值已被改变
- **$invalid**- 指示值的状态是无效的
- **$error**- 指出确切的错误

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html

```html
<html>
<head>
<title>AngularJS 表单</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
<style>
table, th , td {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f2f2f2;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
</head>
<body>
<h2>AngularJS 表单应用示例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<form name="studentForm" novalidate>
<table border="0">
<tr><td>姓氏:</td><td><input name="firstname" type="text" ng-model="firstName" required>
   <span style="color:red" ng-show="studentForm.firstname.$dirty && studentForm.firstname.$invalid">
      <span ng-show="studentForm.firstname.$error.required">姓氏不可为空.</span>
   </span>
</td></tr>
<tr><td>名字: </td><td><input name="lastname"  type="text" ng-model="lastName" required>
   <span style="color:red" ng-show="studentForm.lastname.$dirty && studentForm.lastname.$invalid">
      <span ng-show="studentForm.lastname.$error.required">名字必填.</span>
   </span>
</td></tr>
<tr><td>Email: </td><td><input name="email" type="email" ng-model="email" length="100" required>
<span style="color:red" ng-show="studentForm.email.$dirty && studentForm.email.$invalid">
      <span ng-show="studentForm.email.$error.required">Email 必填.</span>
	  <span ng-show="studentForm.email.$error.email">无效的Email地址.</span>
   </span>
</td></tr>
<tr><td><button ng-click="reset()">重置</button></td><td><button 
	ng-disabled="studentForm.firstname.$dirty && studentForm.firstname.$invalid ||
			  studentForm.lastname.$dirty && studentForm.lastname.$invalid ||
			  studentForm.email.$dirty && studentForm.email.$invalid"
	ng-click="submit()">提交</button></td></tr>
</table>
</form>
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope) {
   $scope.reset = function(){
		$scope.firstName = "Zhuo";
		$scope.lastName = "Jar";
		$scope.email = "yiibai.com@gmail.com";
   }   
   $scope.reset();
});
</script>
</body>
</html>
```

## 输出结果

在浏览器中打开 textAngularJS.html。看到结果结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH13AN22.png)

 

#  AngularJS Includes

HTML不支持HTML页面嵌入到HTML页面。为了实现这一函数通过以下方式被使用：

- **使用Ajax** - 使服务器调用来获取相应的HTML页面，并将其设置在HTML控制的innerHTML。
- **使用服务器端包含** - JSP，PHP和其他Web端服务器技术可以包括HTML页面在动态页面内。

使用AngularJS，我们可以用ng-include 指令使嵌入一个HTML页面在HTML页面中。

```html
<div ng-app="" ng-controller="studentController">
   <div ng-include="'main.htm'"></div>
   <div ng-include="'subjects.htm'"></div>
</div>
```

## 实例

tryAngularJS.html

```html
<html>
<head>
<title>Angular JS Includes 示例</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
<style>
table, th , td {
   border: 1px solid grey;
   border-collapse: collapse;
   padding: 5px;
}
table tr:nth-child(odd) {
   background-color: #f2f2f2;
}
table tr:nth-child(even) {
   background-color: #ffffff;
}
</style>
</head>
<body>
<h2>AngularJS Include示例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<div ng-include="'main.html'"></div>
<div ng-include="'subjects.html'"></div>
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope) {
   $scope.student = {
      firstName: "周",
      lastName: "杰伦",
      fees:500,
      subjects:[
         {name:'物理',marks:78},
         {name:'化学',marks:82},
         {name:'语文',marks:68},
         {name:'外语',marks:79},
          {name:'Java',marks:87}
      ],
      fullName: function() {
         var studentObject;
         studentObject = $scope.student;
         return studentObject.firstName + " " + studentObject.lastName;
      }
   };
});
</script>
</body>
</html>
```

main.html

```php+HTML
<table border="0">
   <tr><td>姓氏:</td><td><input type="text" ng-model="student.firstName"></td></tr>
   <tr><td>名字: </td><td><input type="text" ng-model="student.lastName"></td></tr>
   <tr><td>全名: </td><td>{{student.fullName()}}</td></tr>
</table>
```

subjects.html

```html
<p>科目:</p>
<table>
   <tr>
      <th>名字</th>
      <th>标记</th>
   </tr>
   <tr ng-repeat="subject in student.subjects">
      <td>{{ subject.name }}</td>
      <td>{{ subject.marks }}</td>
   </tr>
</table>
```

## 输出结果

要运行这个例子，需要部署textAngularJS.html，main.html 和 subjects.html 到Web服务器。使用 URL 访问服务器并在 Web 浏览器中打开 textAngularJS.html。看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH143225L.png)

 

# AngularJS Ajax

AngularJS提供 $http 控制，可以作为一种服务从服务器读取数据。服务器可以建立数据库调用来获取记录。AngularJS需要JSON格式的数据。一旦数据准备好，$http可以用以下面的方式从服务器得到数据。

```
function studentController($scope,$http) {
var url="data.txt";
   $http.get(url).success( function(response) {
                           $scope.students = response; 
                        });
}
```

在这里，data.txt中包含了学生记录。$http服务使 Ajax 调用并设置响应到学生的属性。 "students" 模型可以用于绘制 HTML 表格。

## 示例

data.txt

```
[
{
"Name" : "周杰伦",
"RollNo" : 104,
"Percentage" : "80%"
},
{
"Name" : "陈小春",
"RollNo" : 231,
"Percentage" : "71%"
},
{
"Name" : "张学友",
"RollNo" : 391,
"Percentage" : "75%"
},
{
"Name" : "邓紫祺",
"RollNo" : 451,
"Percentage" : "77%"
}
]
```

testAngularJS.html

```
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Angular JS Includes示例</title>
<script src="http://www.yiibai.com/js/angular.min.js"></script>
<style>
table, th , td {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f2f2f2;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
</head>
<body>
<h2>AngularJS 应用示例</h2>
<div ng-app="mainApp" ng-controller="studentController">
<table>
   <tr>
      <th>名字</th>
      <th>号码</th>
	  <th>百分比</th>
   </tr>
   <tr ng-repeat="student in students">
      <td>{{ student.Name }}</td>
      <td>{{ student.RollNo }}</td>
	  <td>{{ student.Percentage }}</td>
   </tr>
</table>
</div>
<script>
var mainApp = angular.module("mainApp", []);

mainApp.controller('studentController', function($scope, $http) {
   var url="data.txt";
   $http.get(url).success( function(response) {
      $scope.students = response;
   });
});
</script>
</body>
</html>
```

## 输出结果

要运行这个例子，需要部署 textAngularJS.html，data.txt 到 Web 服务器。在服务器使用 URL 在Web浏览器中打开textAngularJS.html。看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH14410549.png)

 

# AngularJS 视图

AngularJS支持通过单个页面上的多个视图单页应用。要做到这一点AngularJS提供了ng-view 、 ng-template 指令和 $routeProvider 服务。

## ng-view

NG-view标记简单地创建一个占位符，其中一个相应的视图(HTML或ng-template视图)，可以根据配置来放置。

## 使用

定义主模块使用一个 div 及ng-view。

```
<div ng-app="mainApp">
...
   <div ng-view></div>

</div>    
```

## ng-template

ng-template指令用于创建使用脚本标记的HTML视图。它包含一个“id”属性用于由 $routeProvider 映射带有控制器的视图。

## 使用

定义脚本块类型为 ng-template 的主模块 。

```
<div ng-app="mainApp">
...
   <script type="text/ng-template" id="addStudent.htm">
      <h2> Add Student </h2>
         {{message}}
   </script>

</div>    
```

## $routeProvider

$routeProvider是用来设置URL配置的关键服务，映射与对应的HTML页面或ng-template，并附加相同的控制器。

## 使用

定义脚本块类型为 ng-template 的主模块 。

```
<div ng-app="mainApp">
...
   <script type="text/ng-template" id="addStudent.htm">
      <h2> Add Student </h2>
         {{message}}
   </script>

</div>    
```

## 使用

定义脚本块及主模块，并设置路由配置。

```
 var mainApp = angular.module("mainApp", ['ngRoute']);
      
      mainApp.config(['$routeProvider',
         function($routeProvider) {
            $routeProvider.
               when('/addStudent', {
                  templateUrl: 'addStudent.htm',
                  controller: 'AddStudentController'
               }).
               when('/viewStudents', {
                  templateUrl: 'viewStudents.htm',
                  controller: 'ViewStudentsController'
               }).
               otherwise({
                  redirectTo: '/addStudent'
               });
         }]);
    
```

以下是在上面的例子中要考虑的重点。

- $ routeProvider定义作为一个函数在mainApp模块的配置下，使用键 '$routeProvider'.
- $routeProvider定义URL “/addStudent”，然后映射到“addStudent.htm”。addStudent.htm 存在于相同的路径的主html页面。如果HTM网页没有定义，那么NG-模板使用id="addStudent.htm"。我们使用ng-template。
- "otherwise" 用于设置的默认视图。
- "controller" 用于为视图设置相应的控制器。

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html

```
<html>
<head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 视图</title>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular-route.min.js"></script>
</head>
<body>
   <h2>AngularJS 视图应用示例</h2>
   <div ng-app="mainApp">
      <p><a href="#addStudent">添加学生</a></p>
      <p><a href="#viewStudents">查看学生</a></p>
      <div ng-view></div>
      <script type="text/ng-template" id="addStudent.html">
         <h2> 添加学生 </h2>
         {{message}}
      </script>
      <script type="text/ng-template" id="viewStudents.html">
         <h2> 查看学生 </h2>	    
         {{message}}
      </script>	
   </div>

   <script>
      var mainApp = angular.module("mainApp", ['ngRoute']);
      
      mainApp.config(['$routeProvider',
         function($routeProvider) {
            $routeProvider.
               when('/addStudent', {
                  templateUrl: 'addStudent.html',
                  controller: 'AddStudentController'
               }).
               when('/viewStudents', {
                  templateUrl: 'viewStudents.html',
                  controller: 'ViewStudentsController'
               }).
               otherwise({
                  redirectTo: '/addStudent'
               });
         }]);

         mainApp.controller('AddStudentController', function($scope) {
            $scope.message = "这个页面是用于显示学生信息的输入表单";
         });

         mainApp.controller('ViewStudentsController', function($scope) {
            $scope.message = "这个页面是用于显示所有学生信息";
         });
   </script>
</body>
</html>
```

## 结果

在浏览器中打开 textAngularJS.html 看到结果如下：

 

 

 

# AngularJS 作用域

作用域是视图连接控制器起特殊作用的JavaScript对象。作用域包含模型数据。在控制器，模型数据通过$ scope对象访问。

```
<script>
      var mainApp = angular.module("mainApp", []);

      mainApp.controller("shapeController", function($scope) {
         $scope.message = "In shape controller";
         $scope.type = "Shape";
      });
</script>
```

以下是在上面的例子中要考虑的重点。

- $scope被作为第一个参数在其构造器确定指示控制器。
- $scope.message 和 $scope.type 在HTML页面中使用模型。
- 我们已经设置了模型的值，这将反映在应用模块，其控制器shapeController中。
- 也可以在 $scope 内定义函数。

## 继承作用域

作用域由控制器指定。如果我们定义嵌套控制器，那么子控制器将继承其父控制器的作用域范围。

```
<script>
      var mainApp = angular.module("mainApp", []);

      mainApp.controller("shapeController", function($scope) {
         $scope.message = "In shape controller";
         $scope.type = "Shape";
      });
	  
      mainApp.controller("circleController", function($scope) {
         $scope.message = "In circle controller";   
      });
</script>
```

以下是在上面的例子中要考虑的重点。

- 我们在shapeController设定模型的值。
- 我们重载子控制器 circleController 的消息。当模块的控制器 circleController 中的  “message” 一起使用，将重写消息。

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html

```
<html>
<head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 表单</title>
</head>
<body>
   <h2>AngularJS 表单应用示例</h2>
   <div ng-app="mainApp" ng-controller="shapeController">
      <p>{{message}} <br/> {{type}} </p>
      <div ng-controller="circleController">
         <p>{{message}} <br/> {{type}} </p>
      </div>
      <div ng-controller="squareController">
         <p>{{message}} <br/> {{type}} </p>
      </div>
   </div>
   <script src="http://www.yiibai.com/js/angular.min.js"></script>
   <script>
      var mainApp = angular.module("mainApp", []);

      mainApp.controller("shapeController", function($scope) {
         $scope.message = "In shape controller";
         $scope.type = "Shape";
      });

      mainApp.controller("circleController", function($scope) {
         $scope.message = "In circle controller";   
      });

      mainApp.controller("squareController", function($scope) {
         $scope.message = "In square controller";
         $scope.type = "Square";
      });

   </script>
</body>
</html>
```

## 输出结果

在浏览器中打开 textAngularJS.html 看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH14A9D2.png)

 

# AngularJS Services

AngularJS使用服务架构支持“分离 - 关注”的概念。服务(Services)是JavaScript函数，并负责只做一个特定的任务。这使得它们维护和测试单个的实体。控制器，过滤器可以基于请求调用它们。服务注入正常使用AngularJS的依赖注入机制。

AngularJS提供例如，$http, $route, $window, $location等许多内置服务，每个服务负责例如一个特定的任务，$http是用来做AJAX调用来从服务器获取数据。 $route用来定义路由信息等。内置的服务总是以$符号为前缀。

有两种方法来创建服务。

- factory
- service

## 使用工厂方法

使用工厂方法，我们首先定义一个工厂，然后分配方法给它。

```
      var mainApp = angular.module("mainApp", []);
      mainApp.factory('MathService', function() {     
         var factory = {};  
         factory.multiply = function(a, b) {
            return a * b 
         }
         return factory;
      }); 
```

## 使用服务方法

使用服务的方法，我们定义了一个服务，然后分配方法给它。 也可以注入已可用的服务给它。

```
mainApp.service('CalcService', function(MathService){
    this.square = function(a) { 
		return MathService.multiply(a,a); 
	}
});
```

## 示例

下面的例子将展示上述所有指令。

testAngularJS.html

```
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 服务示例</title>
   <script src="http://www.yiibai.com/js/angular.min.js"></script>
</head>
<body>
   <h2>AngularJS 服务应用示例</h2>
   <div ng-app="mainApp" ng-controller="CalcController">
      <p>输入一个数字: <input type="number" ng-model="number" />
      <button ng-click="square()">X<sup>2</sup></button>
      <p>结果: {{result}}</p>
   </div>
   <script>
      var mainApp = angular.module("mainApp", []);
      mainApp.factory('MathService', function() {     
         var factory = {};  
         factory.multiply = function(a, b) {
            return a * b 
         }
         return factory;
      }); 

      mainApp.service('CalcService', function(MathService){
            this.square = function(a) { 
            return MathService.multiply(a,a); 
         }
      });

      mainApp.controller('CalcController', function($scope, CalcService) {
            $scope.square = function() {
            $scope.result = CalcService.square($scope.number);
         }
      });
   </script>
</body>
</html>
```

## 结果

在浏览器中打开 textAngularJS.html 看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH14J1300.png)

 

# AngularJS依赖注入

依赖注入是部件赋予的，不是硬组件内的编码的依赖设计模式。这从定位减轻组件的依赖，使依赖可配置。这有助于使组件可重复使用，维护和测试。

AngularJS提供了一个至高无上的依赖注入机制。它提供了一种可被注入彼此作为依赖以下核心组件。

- 值 - value
- 工厂 - factory
- 服务 - service
- 提供者 - provider
- 常量 - constant

## 值

值是简单的JavaScript对象，并用它在配置阶段传递值到控制器。

```
//define a module
var mainApp = angular.module("mainApp", []);
//create a value object as "defaultInput" and pass it a data.
mainApp.value("defaultInput", 5);
...
//inject the value in the controller using its name "defaultInput"
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
      $scope.number = defaultInput;
      $scope.result = CalcService.square($scope.number);

      $scope.square = function() {
      $scope.result = CalcService.square($scope.number);
   }
});
```

## 工厂

工厂是一个函数用于返回结果值。它根据需要创建一个值，当一个服务或控制器需要时。它通常使用一个工厂函数来计算和返回结果值

```
//define a module
var mainApp = angular.module("mainApp", []);
//create a factory "MathService" which provides a method multiply to return multiplication of two numbers
mainApp.factory('MathService', function() {     
   var factory = {};  
   factory.multiply = function(a, b) {
      return a * b 
   }
   return factory;
}); 

//inject the factory "MathService" in a service to utilize the multiply method of factory.
mainApp.service('CalcService', function(MathService){
      this.square = function(a) { 
      return MathService.multiply(a,a); 
   }
});
...
```

## 服务

服务是一个单独的JavaScript包含了一组函数对象来执行某些任务。服务正在使用 service()  函数，然后注射到控制器中。

```
//define a module
var mainApp = angular.module("mainApp", []);
...
//create a service which defines a method square to return square of a number.
mainApp.service('CalcService', function(MathService){
      this.square = function(a) { 
      return MathService.multiply(a,a); 
   }
});
//inject the service "CalcService" into the controller
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
      $scope.number = defaultInput;
      $scope.result = CalcService.square($scope.number);

      $scope.square = function() {
      $scope.result = CalcService.square($scope.number);
   }
});
```

## 提供者

提供者使用AngularJS内部创建的服务，工厂等。在配置阶段(第一阶段AngularJS引导自身期间)。下面提及的脚本可以被用来创建，我们已经在前面创建了MathService。提供者是一个特殊的工厂方法使用get()方法来返回值/服务/工厂。

```
//define a module
var mainApp = angular.module("mainApp", []);
...
//create a service using provider which defines a method square to return square of a number.
mainApp.config(function($provide) {
   $provide.provider('MathService', function() {
      this.$get = function() {
         var factory = {};  
         factory.multiply = function(a, b) {
            return a * b; 
         }
         return factory;
      };
   });
});
```

## 常量

常量用于通过配置的相应值，考虑到值不能在配置阶段传递使用。

```
mainApp.constant("configParam", "constant value");
```

## 示例

下面的例子将展示上述所有指令的使用。

testAngularJS.html

```
<html>
<head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>AngularJS 依赖注入</title>
</head>
<body>
   <h2>AngularJS 依赖注入应用示例</h2>
   <div ng-app="mainApp" ng-controller="CalcController">
      <p>输入一个整数: <input type="number" ng-model="number" />
      <button ng-click="square()">X<sup>2</sup></button>
      <p>结果值: {{result}}</p>
   </div>
   <script src="http://www.yiibai.com/js/angular.min.js"></script>
   <script>
      var mainApp = angular.module("mainApp", []);
	  
      mainApp.config(function($provide) {
         $provide.provider('MathService', function() {
            this.$get = function() {
               var factory = {};  
               factory.multiply = function(a, b) {
                  return a * b; 
               }
               return factory;
            };
         });
      });

      mainApp.value("defaultInput", 5);

      mainApp.factory('MathService', function() {     
         var factory = {};  
         factory.multiply = function(a, b) {
            return a * b; 
         }
         return factory;
      }); 

      mainApp.service('CalcService', function(MathService){
            this.square = function(a) { 
            return MathService.multiply(a,a); 
         }
      });

      mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
            $scope.number = defaultInput;
            $scope.result = CalcService.square($scope.number);

            $scope.square = function() {
            $scope.result = CalcService.square($scope.number);
         }
      });
   </script>
</body>
</html>
```

## 结果

在浏览器中打开 textAngularJS.html 看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH14Ua20.png)

 

# AngularJS自定义指令

自定义指令用于在AngularJS中来扩展HTML的功能。自定义指令使用“指令”函数定义。自定义指令只是替换了被激活的元素。AngularJS应用程序引导过程中找到匹配的元素，并使用自定义指令compile() 方法，一次使用基于指令的范围自定义指令link() 方法处理元素。AngularJS 为下面的元素类型创建自定义的指令提供支持。

- 元素指令 - 当遇到指令激活匹配的元素。
- 属性 - - 当遇到指令激活属性时匹配。
- CSS - - 当遇到指令激活匹配CSS样式。
- 注释 - - 当遇到指令激活匹配的注释。

## 理解自定义指令

定义自定义HTML标签。

```
<student name="Mahesh"></student><br/>
<student name="Piyush"></student>
```

定义自定义指令来处理上面的自定义HTML标签。

```
var mainApp = angular.module("mainApp", []);

//Create a directive, first parameter is the html element to be attached.	  
//We are attaching student html tag. 
//This directive will be activated as soon as any student element is encountered in html
mainApp.directive('student', function() {
   //define the directive object
   var directive = {};
   //restrict = E, signifies that directive is Element directive
   directive.restrict = 'E';
   //template replaces the complete element with its text. 
   directive.template = "Student: <b>{{student.name}}</b> , Roll No: <b>{{student.rollno}}</b>";
   //scope is used to distinguish each student element based on criteria.
   directive.scope = {
       student : "=name"
   }
   //compile is called during application initialization. AngularJS calls it once when html page is loaded.
   directive.compile = function(element, attributes) {
      element.css("border", "1px solid #cccccc");
	  //linkFunction is linked with each element with scope to get the element specific data.
      var linkFunction = function($scope, element, attributes) {
          element.html("Student: <b>"+$scope.student.name +"</b> , Roll No: <b>"+$scope.student.rollno+"</b><br/>");
          element.css("background-color", "#ff00ff");
      }
      return linkFunction;
   }
   return directive;
});
```

定义控制器以更新指令的作用域。这里我们使用名称属性的值作为子的作用域。

```
mainApp.controller('StudentController', function($scope) {
      $scope.Mahesh = {};
      $scope.Mahesh.name = "Mahesh Parashar";
      $scope.Mahesh.rollno  = 1;

      $scope.Piyush = {};
      $scope.Piyush.name = "Piyush Parashar";
      $scope.Piyush.rollno  = 2;
});
```

## 示例

```
<html>
<head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 自定义指令</title>
</head>
<body>
   <h2>AngularJS 自定义指令示例</h2>
   <div ng-app="mainApp" ng-controller="StudentController">
		<student name="Mahesh"></student><br/>
		<student name="Piyush"></student>
   </div>
   <script src="http://www.yiibai.com/js/angular.min.js"></script>
   <script>
      var mainApp = angular.module("mainApp", []);
	  
      mainApp.directive('student', function() {
         var directive = {};
         directive.restrict = 'E';
         directive.template = "Student: <b>{{student.name}}</b> , 编号: <b>{{student.rollno}}</b>";
         
         directive.scope = {
            student : "=name"
         }
		 
         directive.compile = function(element, attributes) {
            element.css("border", "1px solid #cccccc");

            var linkFunction = function($scope, element, attributes) {
               element.html("Student: <b>"+$scope.student.name +"</b> , 编号: <b>"+$scope.student.rollno+"</b><br/>");
               element.css("background-color", "#eee");
            }

            return linkFunction;
         }

         return directive;
      });
	  
      mainApp.controller('StudentController', function($scope) {
            $scope.Mahesh = {};
            $scope.Mahesh.name = "张学友";
            $scope.Mahesh.rollno  = 100;

            $scope.Piyush = {};
            $scope.Piyush.name = "陈奕迅";
            $scope.Piyush.rollno  = 102;
      });
      
   </script>
</body>
</html>
```

## 结果

在Web浏览器中打开textAngularJS.htm。看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH1495U17.png)

 

#  AngularJS国际化

AngularJS支持内置国际化三种类型的过滤器：货币，日期和数字。我们只需要根据国家的区域合并相应的JS。默认情况下它处理浏览器的语言环境。例如，使用丹麦语区域设置，使用下面的脚本：

```
<script src="https://code.angularjs.org/1.2.5/i18n/angular-locale_da-dk.js"></script> 
```

## 使用中文区域设置示例

testAngularJS.html

```
<html>
<head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 国际化</title>
</head>
<body>
   <h2>AngularJS 国际化应用示例</h2>
   <div ng-app="mainApp" ng-controller="StudentController">
      {{fees | currency }}  <br/><br/>
      {{admissiondate | date }}   <br/><br/>
      {{rollno | number }}  
   </div>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
   <script src="http://cdnjscn.b0.upaiyun.com/libs/angular-i18n/1.2.0/angular-locale_zh-cn.js"></script> 
   <script>
      var mainApp = angular.module("mainApp", []);
	    
      mainApp.controller('StudentController', function($scope) {
            $scope.fees = 100;
			$scope.admissiondate  = new Date();
            $scope.rollno = 123.45;
      });
      
   </script>
</body>
</html>
```

## 结果

在Web浏览器中打开textAngularJS.htm。看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH1503c64.png)

 

## 使用浏览器的语言环境示例

testAngularJS.html

```
<html>
<head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
   <title>Angular JS 浏览器语言设置示例</title>
</head>
<body>
   <h2>AngularJS 区域语言设置(浏览器设置)</h2>
   <div ng-app="mainApp" ng-controller="StudentController">
      {{fees | currency }}  <br/><br/>
      {{admissiondate | date }}   <br/><br/>
      {{rollno | number }}  
   </div>
   <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
   <!-- <script src="http://cdnjscn.b0.upaiyun.com/libs/angular-i18n/1.2.0/angular-locale_zh-hk.js"></script> -->
   <script>
      var mainApp = angular.module("mainApp", []);
	    
      mainApp.controller('StudentController', function($scope) {
            $scope.fees = 100;
			$scope.admissiondate  = new Date();
            $scope.rollno = 123.45;
      });
      
   </script>
</body>
</html>
```

## 结果

在Web浏览器中打开textAngularJS.html。看到结果如下：
![img](https://www.yiibai.com/uploads/allimg/201508/1-150QH15113C5.png)

 

 