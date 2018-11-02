​	目前，使用vue-cli脚手架写了一个前端项目，之前一直是使用npm run dev 在8080端口上进行本地调试。项目已经进行一半了，今天有时间突然想使用npm run build进行上线打包，试试能否成功看到我的项目效果。一开始是毫无头绪，什么都不懂，直接是就在命令行上敲下：npm run build命令。

![](https://ws1.sinaimg.cn/large/006tNbRwly1fwtkkpa1vhj30sr0fn74r.jpg)

​	好开心啊，竟然没有报错。以为就这么简单的成功了，在浏览器上输入：http://localhost/MGT/learnVuex/dist/index.html，一片空白。果然没有那么顺利。打开控制，看到Console下出现了很多错误。

![](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkkpprwaj30r50cejse.jpg)

错误看不懂，（捂脸）只好百度了。

我们一开始运行npm run build 命令时，有这么一段提示：

![](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkkq5ntoj30ie01tt8h.jpg)

这段话的意思就是说：构建文件务必放在一个`HTTP`服务器。直接打开`index.html`文件将不工作。

看到提示还是要好好看的，这毛病要改呀！

那么问题来了，怎么解决呢？

我们知道打包的命令文件是config/build.js

![](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkkqlfnkj307r0cxgln.jpg)

到项目目录下的`config`文件夹里的`index.js`文件中,将`build`对象下的`assetsPublicPath`中的`“/”`，改为`“./”`即可，就在前面加个点就可以了，

![](https://ws1.sinaimg.cn/large/006tNbRwly1fwtkkr26kwj30oe0ab0tk.jpg)

现在再重新打包一次 `npm run build`，刷新你的页面，就可以看到啦

![](https://ws4.sinaimg.cn/large/006tNbRwly1fwtkkrhjbzj314v0hd75a.jpg)

在这之前有一个前提条件，那就是电脑上要安装服务器。只要你的服务器上有支持http或者https的服务器软件就可以，我知道的有nginx和apache两种，只要安装了两个中的一个，并且配合好访问路径，把你生成的文件放到服务器下或者映射路径下，启动你的服务器软件即可，然后就可以使用你配置的路径访问项目。

我在浏览器上直接是输入localhost，打开文件目录的，http://localhost/MGT/learnVuex/dist/index.html，这么文件到底是在哪个盘下面呢？

我在电脑上上安装了一个XAMPP，并把apache的映射路径设置为：E:/project，而我的项目文件就放在E:/project目录下面 这就是我的：E:\\project\\MGT\\learnVuex\\dist。

所以在浏览器上输入：localhost，就是打开E:/project，就可以看到这目录下的所以项目文件啦。