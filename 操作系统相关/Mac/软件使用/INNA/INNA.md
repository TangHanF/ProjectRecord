 

 

 

 

 

【写在开头】

> 我在一开始安装IINA的时候也是出现题主的问题，但是通过加群（142730636）请教了群主大大（也就是本软件的开发作者）后，他耐心细心的指导让我一步一步成功实现了用IINA在线观看视频！！！再次表白感谢作者大大 [@大型强子对撞机](http://www.zhihu.com/people/7a259628c35c76c8347053f57c504655)！！！

涉及：MAC电脑，homebrew, youtube-dl, IINA

关于IINA：

- 官网下载链接：

https://lhc70000.github.io/iina/zh-cn/lhc70000.github.io

- 作者知乎专栏：

大型强子对撞机：IINA 向「现代 macOS 播放器」的目标又进了一步zhuanlan.zhihu.com![图标](https://pic4.zhimg.com/v2-081ca186ad3be64879435c6dad192db7_180x120.jpg)

【正文】

一、安装 homebrew

- 官网：[https://brew.sh](https://link.zhihu.com/?target=https%3A//brew.sh)
- 打开苹果终端，在终端输入 

```
- /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- 回车
- 等待程序处理（这个安装过程较长，请耐心等待），直至显示

```
rollerdeMacBook—Pro : roller$  
```

(roller是我的电脑名称）

二、安装 youtube-dl

- 在终端输入 

```
brew install youtube-dl
```

- 回车
- 等待程序处理，直至显示

```
rollerdeMacBook—Pro : roller$ 
```

(roller是我的电脑名称）

三、设置IINA

- IINA的偏好设置----网络----youtube-dl----启用youtube-dl----自定义youtube----dl路径：/usr/local/bin ----回车

&lt;img src="https://pic3.zhimg.com/50/v2-21b4f955e09c9a6848c17b83d73c2505_hd.jpg" data-caption="" data-size="normal" data-rawwidth="988" data-rawheight="1046" class="origin_image zh-lightbox-thumb" width="988" data-original="https://pic3.zhimg.com/v2-21b4f955e09c9a6848c17b83d73c2505_r.jpg"&gt;![img](https://pic3.zhimg.com/80/v2-21b4f955e09c9a6848c17b83d73c2505_hd.jpg)

- 重启
- 下载youtube-dl插件（safari/chrome)

&lt;img src="https://pic4.zhimg.com/50/v2-1af28594bca41fa8ccfec1b3f9ac46f6_hd.jpg" data-caption="" data-size="normal" data-rawwidth="1172" data-rawheight="634" class="origin_image zh-lightbox-thumb" width="1172" data-original="https://pic4.zhimg.com/v2-1af28594bca41fa8ccfec1b3f9ac46f6_r.jpg"&gt;![img](https://pic4.zhimg.com/80/v2-1af28594bca41fa8ccfec1b3f9ac46f6_hd.jpg)

- 下载后打开安装到扩展中（记得点系统偏好设置-安全性与隐私-锁的图标）

&lt;img src="https://pic3.zhimg.com/50/v2-e9e9858cd55e0cb2b2d19a10bbfde8b1_hd.jpg" data-caption="" data-size="normal" data-rawwidth="1336" data-rawheight="1086" class="origin_image zh-lightbox-thumb" width="1336" data-original="https://pic3.zhimg.com/v2-e9e9858cd55e0cb2b2d19a10bbfde8b1_r.jpg"&gt;![img](https://pic3.zhimg.com/80/v2-e9e9858cd55e0cb2b2d19a10bbfde8b1_hd.jpg)

- 打开一个视频网站，会发现页面地址栏有一个小图标

&lt;img src="https://pic3.zhimg.com/50/v2-959a0c336cb0ba66e0ab499fcec13837_hd.jpg" data-caption="" data-size="normal" data-rawwidth="120" data-rawheight="74" class="content_image" width="120"&gt;![img](https://pic3.zhimg.com/80/v2-959a0c336cb0ba66e0ab499fcec13837_hd.jpg)

点击它，并允许打开IINA，等待加载后就可以在IINA里观看无广告的视频啦~~！！

PS：目前可用的视频网站有：Youtube, 优酷，Blibli (爱奇艺、腾讯、Acfun不可以）