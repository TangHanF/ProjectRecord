## AngularJS 是什么?

AngularJS是一个非常强大的JavaScript库，用于在单页应用程序（SPA）项目。它扩展了HTML DOM的附加属性，使之更适应用户操作。 AngularJS是开源的，完全免费的，并且由数千名世界各地的开发。它是根据Apache许可证2.0版许可。

AngularJS是一个开源Web应用程序框架。它最初是由Misko Hevery和Adam Abrons开发于2009年。现在是由谷歌维护。

AngularJS的定义，它的[官方文档](http://docs.angularjs.org/guide/introduction)介绍如下：

> AngularJS是动态的Web应用程序结构框架。它可以让你使用HTML作为模板语言，扩展HTML的语法清晰，简洁地表达应用程序的组件。Angular分明的数据绑定和依赖注入必须编写代码。而这一切都在浏览器内发生，这使得它与任何服务器技术的理想合作伙伴。

## 特点

- AngularJS是一个功能强大的基于JavaScript开发框架来创建富互联网应用（RIA）。
- AngulajJS为开发者提供选项来编写客户端应用程序（使用JavaScript）在一个干净的MVC（模型 - 视图 - 控制器）的方式。
- AngularJS应用是跨浏览器兼容的。自动AngularJS处理适用于每个浏览器的javascript代码。
- AngularJS是开源的，完全免费的，并且由数千名世界各地的开发。它是根据Apache许可证2.0版许可。

总体而言，AngularJS是一个框架可以用来构建大规模，高性能的网络应用，同时也易于维护。

## 核心功能

以下是AngularJS的最重要的核心的功能：

- **数据绑定：**它是模型和视图组件之间的数据的自动同步。
- **适用范围：**这些是指模型对象。充当控制器和视图之间的胶水。
- **控制器：**这些是绑定到特定范围的Javascript函数。
- **服务：**AngularJS配有多个内置的服务，例如$http提供XMLHttpRequest。这些是在应用程序实例化一次的单一对象。
- **过滤器：**这些从数组项目中选择一个子集，并返回一个新的数组。
- **指令：**指令是关于DOM元素标记（如元素，属性，CSS等等）。这些可以被用来创建作为新的自定义窗口小部件自定义的HTML标签。 AngularJS有内置的指令（ngBind，ngModel...）
- **模板：**这些都与控制器和模型信息呈现的视图。这些可以使用“谐音”的单个文件（如index.html），或在一个页面上的多个视图。
- **路由：**它是切换视图的概念。
- **模型 - 视图 ：**MVC是一个设计模式将应用划分为不同的部分（称为模型，视图和控制器），每一个具有不同的责任。 AngularJS没有传统意义上的MVC实现，而是更接近于MVVM（模型 - 视图 - 视图模型）。AngularJS团队让它作为模型视图而不管。
- **深层链接：**深层链接能够使其可书签应用程序的状态进行编码的URL。应用程序可以从该URL为相同的状态恢复。
- **依赖注入：** AngularJS有一个内置的依赖注入子系统，通过使应用程序帮助开发人员更易于开发，理解和测试。

## 概念

下图描绘了AngularJS，我们将详细在随后的章节讨论的一些重要部分。

## AngularJS的优点

- AngularJS提供在一个非常干净和维护方式来创建单页的应用。
- AngularJS提供了数据绑定功能为HTML从而给用户提供丰富而敏感的体验
- AngularJS代码可单元测试。
- AngularJS使用依赖注入和运用关注点分离。
- AngularJS提供了可重用的组件。
- AngularJS能为开发人员编写更少的代码，并获得更多的功能。
- 在AngularJS，视图都是纯HTML页面，并用JavaScript编写控制器完成业务处理。

AngularJS应用程序可以在所有主要浏览器和智能手机，包括Android和iOS系统的手机/平板电脑上运行。

## AngulaJS的缺点

虽然AngularJS带有许多加分，但是我们应该考虑以下几点：

- 不安全：JavaScript只有框架编写的应用程序在AngularJS是不安全的。服务器端的认证和授权是必须的，以保持应用程序的安全。
- 不可降解：如果应用程序的用户禁用JavaScript的话用户将只能看到基本的页面，仅此而已。

## AngularJS组件

AngularJS框架可分为以下三个主要部分组成：

- ng-app : 该指令规定，并链接一个AngularJS应用程序的HTML。
- ng-model : 该指令结合AngularJS应用数据的值到HTML的输入控件。
- ng-bind : 该指令子带AngularJS应用数据的HTML标签。