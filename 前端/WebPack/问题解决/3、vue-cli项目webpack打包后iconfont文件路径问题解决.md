在使用vue-cli创建vue项目时，可以自动生成webpack文件。使用

```
npm run build

* 1

```

即可打包发布生产文件，打包后的文件 
![webpack配置](https://ws3.sinaimg.cn/large/006tNbRwly1fwtkkmyzxcj30w50epwgh.jpg)
可以看到使用url-loader处理后的文件是在static目录下生成fonts目录下的文件。全部样式文件打包在css目录下app.hash.css文件中。 
但我们会发现发布后，会存在字体文件找不到的问题，查看css文件发现是iconfont字体文件的路径引用问题。 
![这里写图片描述](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkkntca0j30wq05eweq.jpg)

解决方法： 
在build/utils文件中的下图所示位置添加../../公共路径 
![这里写图片描述](https://ws2.sinaimg.cn/large/006tNbRwly1fwtkkobf8sj30pd0j0dih.jpg)
这样打包的iconfont字体文件路径时就会加上../../了。引用就没问题了。而不再需要手动更改css文件中的路径。 
![这里写图片描述](https://ws3.sinaimg.cn/large/006tNbRwly1fwtkkot52fj30w904ymxd.jpg)