

# NodeJS总结

> 作者：TangHanF
>
> 创建日期：2018年4月11日



参考来源：

- 菜鸟教程  [连接地址](http://www.runoob.com/nodejs/nodejs-tutorial.html)
- 廖雪峰Nodejs  [连接地址](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434501245426ad4b91f2b880464ba876a8e3043fc8ef000)

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
> 文件系统模块，负责读写文件。`fs`模块同时提供了异步和同步的方法。


### 异步读取文件

**代码示例**

``` javascript 
var fs = require('fs');

fs.readFile('sample.txt', 'utf-8', function (err, data) {
    if (err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```
> 异步读取时，传入的回调函数接收两个参数，当正常读取时，`err`参数为`null`，`data`参数为读取到的String。当读取发生错误时，`err`参数代表一个错误对象，`data`为`undefined`。这也是Node.js标准的回调函数：第一个参数代表错误信息，第二个参数代表结果。后面我们还会经常编写这种回调函数。



**当读取二进制文件时，不传入文件编码时，回调函数的`data`参数将返回一个`Buffer`对象,例如**

```javascript
var fs = require('fs');

fs.readFile('sample.png', function (err, data) {
    // 此时 data 就是一个Buffer对象，
    if (err) {
        console.log(err);
    } else {
        console.log(data);
        console.log(data.length + ' bytes');
    }
});
```

`Buffer`对象可以和String作转换:`data.toString()`



### 同步读取文件

除了标准的异步读取模式外，`fs`也提供相应的同步读取函数。同步读取的函数和异步函数相比，多了一个`Sync`后缀，并且不接收回调函数，函数直接返回结果。

用`fs`模块同步读取一个文本文件的代码如下：

```javascript
'use strict';

var fs = require('fs');

var data = fs.readFileSync('sample.txt', 'utf-8');
console.log(data);
```

可见，原异步调用的回调函数的`data`被函数直接返回，函数名需要改为`readFileSync`，其它参数不变。

如果同步读取文件发生错误，则需要用`try...catch`捕获该错误：

```javascript
try {
    var data = fs.readFileSync('sample.txt', 'utf-8');
    console.log(data);
} catch (err) {
    // 出错了
}
```

### 写文件

将数据写入文件是通过`fs.writeFile()`实现的：

```javascript
'use strict';

var fs = require('fs');

var data = 'Hello, Node.js';
fs.writeFile('output.txt', data, function (err) {
    if (err) {
        console.log(err);
    } else {
        console.log('ok.');
    }
});
```

`writeFile()`的参数依次为**文件名**、**数据**和**回调函数**。如果传入的数据是String，默认按UTF-8编码写入文本文件，如果传入的参数是`Buffer`，则写入的是二进制文件。回调函数由于只关心成功与否，因此只需要一个`err`参数。

和`readFile()`类似，`writeFile()`也有一个同步方法，叫`writeFileSync()`：

```javascript
'use strict';

var fs = require('fs');

var data = 'Hello, Node.js';
fs.writeFileSync('output.txt', data);
```

### stat-获取文件相关信息

如果我们要获取文件大小，创建时间等信息，可以使用`fs.stat()`，它返回一个`Stat`对象，能告诉我们文件或目录的详细信息：

```javascript
'use strict';

var fs = require('fs');

fs.stat('sample.txt', function (err, stat) {
    if (err) {
        console.log(err);
    } else {
        // 是否是文件:
        console.log('isFile: ' + stat.isFile());
        // 是否是目录:
        console.log('isDirectory: ' + stat.isDirectory());
        if (stat.isFile()) {
            // 文件大小:
            console.log('size: ' + stat.size);
            // 创建时间, Date对象:
            console.log('birth time: ' + stat.birthtime);
            // 修改时间, Date对象:
            console.log('modified time: ' + stat.mtime);
        }
    }
});
```

运行结果如下：

```
isFile: true
isDirectory: false
size: 181
birth time: Fri Dec 11 2015 09:43:41 GMT+0800 (CST)
modified time: Fri Dec 11 2015 12:09:00 GMT+0800 (CST)
```

`stat()`也有一个对应的同步函数`statSync()`，请试着改写上述异步代码为同步代码。

### 异步还是同步

在`fs`模块中，提供同步方法是为了方便使用。那我们到底是应该用异步方法还是同步方法呢？

由于Node环境执行的JavaScript代码是服务器端代码，所以，绝大部分需要在服务器运行期反复执行业务逻辑的代码，*必须使用异步代码*，否则，同步代码在执行时期，服务器将停止响应，因为JavaScript只有一个执行线程。

服务器启动时如果需要读取配置文件，或者结束时需要写入到状态文件时，可以使用同步代码，因为这些代码只在启动和结束时执行一次，不影响服务器正常运行时的异步执行。



------




## http模块
### 模块说明
> eee
### 代码示例
``` javascript 

```
-----

## url模块

### 模块说明

> 通过`parse()`将一个字符串解析为一个`Url`对象

### 代码示例

```javascript 
var url = require('url');

console.log(url.parse('http://user:pass@host.com:8080/path/to/file?query=string#hash'));
```

结果如下：

```
Url {
  protocol: 'http:',
  slashes: true,
  auth: 'user:pass',
  host: 'host.com:8080',
  port: '8080',
  hostname: 'host.com',
  hash: '#hash',
  search: '?query=string',
  query: 'query=string',
  pathname: '/path/to/file',
  path: '/path/to/file?query=string',
  href: 'http://user:pass@host.com:8080/path/to/file?query=string#hash' }
```

------

## path模块

### 模块说明

> eee

### 代码示例

```javascript 

```

------







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



## crypto模块

### 模块说明

> crypto模块的目的是为了提供通用的加密和哈希算法

#### MD5

> MD5是一种常用的哈希算法，用于给任意数据一个“签名”。这个签名通常用一个十六进制的字符串表示











--------





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

## Stream类

### 类说明

> `stream`是Node.js提供的又一个仅在服务区端可用的模块，目的是支持“流”这种数据结构。
>
> 流是一种抽象的数据结构。想象水流，当在水管中流动时，就可以从某个地方（例如自来水厂）源源不断地到达另一个地方（比如你家的洗手池）。我们也可以把数据看成是数据流，比如你敲键盘的时候，就可以把每个字符依次连起来，看成字符流。这个流是从键盘输入到应用程序，实际上它还对应着一个名字：标准输入流（stdin）。
>
> 如果应用程序把字符一个一个输出到显示器上，这也可以看成是一个流，这个流也有名字：标准输出流（stdout）。流的特点是数据是有序的，而且必须依次读取，或者依次写入，不能像Array那样随机定位。



在Node.js中，流也是一个对象，我们只需要响应流的事件就可以了：`data`事件表示流的数据已经可以读取了，`end`事件表示这个流已经到末尾了，没有数据可以读取了，`error`事件表示出错了。

### 代码示例

```javascript
var fs = require('fs');

// 打开一个流:
var rs = fs.createReadStream('sample.txt', 'utf-8');

rs.on('data', function (chunk) {
    console.log('DATA:')
    console.log(chunk);
});

rs.on('end', function () {
    console.log('END');
});

rs.on('error', function (err) {
    console.log('ERROR: ' + err);
});
```

要注意，`data`事件可能会有多次，每次传递的`chunk`是流的一部分数据。

要以流的形式写入文件，只需要不断调用`write()`方法，最后以`end()`结束：

```javascript
'use strict';

var fs = require('fs');

var ws1 = fs.createWriteStream('output1.txt', 'utf-8');
ws1.write('使用Stream写入文本数据...\n');
ws1.write('END.');
ws1.end();

var ws2 = fs.createWriteStream('output2.txt');
ws2.write(new Buffer('使用Stream写入二进制数据...\n', 'utf-8'));
ws2.write(new Buffer('END.', 'utf-8'));
ws2.end();
```

所有可以读取数据的流都继承自`stream.Readable`，所有可以写入的流都继承自`stream.Writable`。



## Pip类

### 类说明

就像可以把两个水管串成一个更长的水管一样，两个流也可以串起来。一个`Readable`流和一个`Writable`流串起来后，所有的数据自动从`Readable`流进入`Writable`流，这种操作叫`pipe`。

在Node.js中，`Readable`流有一个`pipe()`方法，就是用来干这件事的。

让我们用`pipe()`把一个文件流和另一个文件流串起来，这样源文件的所有数据就自动写入到目标文件里了，所以，这实际上是一个复制文件的程序：

###代码示例

```javascript
'use strict';

var fs = require('fs');

var rs = fs.createReadStream('sample.txt');
var ws = fs.createWriteStream('copied.txt');

rs.pipe(ws);
```

默认情况下，当`Readable`流的数据读取完毕，`end`事件触发后，将自动关闭`Writable`流。如果我们不希望自动关闭`Writable`流，需要传入参数：

```javascript
readable.pipe(writable, { end: false });
```







[^ 1]: 总结整理相关重点模块
[^ 2]: 总结整理相关重点类



# 其它点

1. *注意*，任何时候都可以直接删除整个`node_modules`目录，因为用`npm install`命令可以完整地重新下载所有依赖。并且，这个目录不应该被放入版本控制中。
2. 由`async`标记的函数称为异步函数，在异步函数中，可以用`await`调用另一个异步函数，这两个关键字将在ES7中引入。**每个`async`函数称为middleware**，这些middleware可以组合起来，完成很多有用的功能。如果一个middleware没有调用`await next()`后续的middleware将不再执行，例如可以应用在用户权限检测方面。

