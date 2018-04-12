# NodeJS总结

> 作者：TangHanF
>
> 创建日期：2018年4月11日



# 目录导航

[TOC]



# 基础总结

- Node.js 就是运行在服务端的 JavaScript

- Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

- Node.js 异步编程的直接体现就是回调。异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。**Node 所有 API 都支持回调函数。**

- Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

- Node.js 是单进程单线程应用程序，但是通过事件和回调支持并发，所以性能非常高。

- > - 单进程单线程：一盘炒苦瓜，里面只有苦瓜。
  > - 单进程多线程：一盘宫保鸡丁，里面有黄瓜、胡萝卜、鸡肉、花生米

- Node.js 的每一个 API 都是异步的，并作为一个独立线程运行，使用异步函数调用，并处理并发。

- Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。

- Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.

![](http://www.runoob.com/wp-content/uploads/2015/09/event_loop.jpg "在事件驱动模型中，会生成一个主循环来监听事件，当检测到事件时触发回调函数。")

 

-----

# Node 应用程序是如何工作的？

在 Node 应用程序中，执行异步操作的函数**将回调函数作为最后一个参数**， 回调函数**接收错误对象作为第一个参数**。

例如：

```javascript
var fs = require("fs");

fs.readFile('input.txt', function (err, data) {
   if (err){
      console.log(err.stack);
      return;
   }
   console.log(data.toString());
});
console.log("程序执行完毕");
```

以上程序中 fs.readFile() 是异步函数用于读取文件。 如果在读取文件过程中发生错误，错误 err 对象就会输出错误信息。

如果没发生错误，readFile 跳过 err 对象的输出，文件内容就通过回调函数输出。

# NodeJS重点模块[^ 1]

## fs模块
### 模块说明
> eee
### 代码示例
``` javascript 

```
-----


## http模块
### 模块说明
> eee
### 代码示例
``` javascript 

```
-----

## events模块
### 模块说明
> events 模块只提供了一个对象： events.EventEmitter
### 代码示例

``` JavaScript
    // 引入events模块
    var events = require("events");

    // 创建事件处理程序
    var eventEmitter = new events.EventEmitter();

    var connectHandler = function () {
        console.log("连接成功");

        // 触发 data_received 事件 
        eventEmitter.emit("data_recive")
    }
    // 绑定 connection 事件处理程序
    eventEmitter.on("connection", connectHandler);

    // 使用匿名函数绑定 data_received 事件
    eventEmitter.on("data_recive", function () {
        console.log("数据接收成功！")
    });

    // 触发 connection 事件 
    eventEmitter.emit("connection");

    console.log("程序执行完毕。");
```
**小结**
> EventEmitter的 `on` 进行事件的绑定
>
> EventEmitter的 `emit` 触发绑定的事件

-----



# NodeJS重点类[^ 2]

## EventEmitter 类

### 类说明

>events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。

你可以通过**require("events");**来访问该模块。

### 代码示例

```javascript
// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();
```

- EventEmitter的 `on` 进行事件的绑定
- EventEmitter的 `emit` 触发绑定的事件

EventEmitter 的每个事件由一个事件名和若干个参数组成，**事件名是一个字符串**，通常表达一定的语义。对于每个事件，EventEmitter 支持 若干个事件监听器。

当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。

**多参数、同一事件：**

```javascript
var event = require("events");

var eventEmitter = new event.EventEmitter();

eventEmitter.on("someEvent", function (arg1, arg2) {
    console.log("someEvent1 事件触发", arg1, arg2);
});

eventEmitter.on("someEvent", function (arg1, arg2) {
    console.log("someEvent2 事件触发", arg1, arg2);
});


eventEmitter.emit("someEvent", "参数1", "参数2");
```

运行结果：

> someEvent1 事件触发 参数1 参数2
> someEvent2 事件触发 参数1 参数2

以上例子中，emitter 为事件 someEvent 注册了两个事件监听器，然后触发了 someEvent 事件。

运行结果中可以看到两个事件监听器回调函数被先后调用。 这就是EventEmitter最简单的用法。



### 方法

[参考此处](http://www.runoob.com/nodejs/nodejs-event.html)

## Buffer类



## Stream类



## 333







[^ 1]: 总结整理相关重点模块
[^ 2]: 总结整理相关重点类