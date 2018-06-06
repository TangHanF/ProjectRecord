# Mac下安装NodeJS

下载地址：

[node.js官网](https://nodejs.org/en/download/)

下载完成pkg文件并一步一步安装完成之后输入以下命令检查是否安装成功：

This package will install:
	•	Node.js v8.11.2 to /usr/local/bin/node
	•	npm v5.6.0 to /usr/local/bin/npm

> node -v

> npm -v

然后在Finder中打开用户目录（就是Mac管理员，点开侧栏打开目录，创建一个Js文件，取名helloworld.js就可以，在js文件中输入这些内容）

```javascript
const http = require('http');
const hostname = '127.0.0.1';
const port = 1337;

http.createServer((req, res) => {
	res.writeHead(200, { 'Content-Type': 'text/plain' });
	res.end('Hello World\n');
}).listen(port, hostname, () => {
	console.log(Server running at http://${hostname}:${port}/);
});

```



保存成功之后，打开终端

输入 node helloworld.js得到

![img](https://images2015.cnblogs.com/blog/998610/201611/998610-20161110143209014-2007327076.png)

然后把下面的ip地址复制到浏览器打开

![img](https://images2015.cnblogs.com/blog/998610/201611/998610-20161110143313233-1151696868.png)

 

*这就配置成功了*