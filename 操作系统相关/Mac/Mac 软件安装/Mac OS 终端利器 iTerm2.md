# 一部分

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228130441550-1699845986.jpg)



之前一直使用 Mac OS 自带的终端，用起来虽然有些不太方便，但总体来说还是可以接受的，是有想换个终端的想法，然后今天偶然看到一个终端利器 iTerm2，发现真的很强大，也非常的好用，按照网上配置了主题什么的，还是有些坑的，这边再记录下，以便后面查阅。

## 1. 安装 iTerm2

下载地址：<https://www.iterm2.com/downloads.html>

下载的是压缩文件，解压后是执行程序文件，你可以直接双击，或者直接将它拖到 Applications 目录下。

或者你可以直接使用 Homebrew 进行安装：

```
$ brew cask install iterm2
```

## 2. 配置 iTerm2 主题

iTerm2 最常用的主题是 Solarized Dark theme，下载地址：<http://ethanschoonover.com/solarized>

下载的是压缩文件，你先解压一下，然后打开 iTerm2，按`Command + ,`键，打开 Preferences 配置界面，然后`Profiles -> Colors -> Color Presets -> Import`，选择刚才解压的`solarized->iterm2-colors-solarized->Solarized Dark.itermcolors`文件，导入成功，最后选择 Solarized Dark 主题，就可以了。

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124549144-520902143.png)

## 3. 配置 Oh My Zsh

Oh My Zsh 是对主题的进一步扩展，地址：<https://github.com/robbyrussell/oh-my-zsh>

一键安装：

```
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

安装好之后，需要把 Zsh 设置为当前用户的默认 Shell（这样新建标签的时候才会使用 Zsh）：

```
$ chsh -s /bin/zsh
```

然后，我们编辑`vim ~/.zshrc`文件，将主题配置修改为`ZSH_THEME="agnoster"`。

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124617863-587540558.png)

`agnoster`是比较常用的 zsh 主题之一，你可以挑选你喜欢的主题，zsh 主题列表：<https://github.com/robbyrussell/oh-my-zsh/wiki/themes>

效果如下（配置了声明高亮）：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124626363-735900072.png)

## 4. 配置 Meslo 字体

使用上面的主题，需要 Meslo 字体支持，要不然会出现乱码的情况，字体下载地址：[Meslo LG M Regular for Powerline.ttf](https://github.com/powerline/fonts/blob/master/Meslo%20Slashed/Meslo%20LG%20M%20Regular%20for%20Powerline.ttf)

下载好之后，直接在 Mac OS 中安装即可。

然后打开 iTerm2，按`Command + ,`键，打开 Preferences 配置界面，然后`Profiles -> Text -> Font -> Chanage Font`，选择 Meslo LG M Regular for Powerline 字体。

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124638503-196536251.png)

当然，如果你觉得默认的`12px`字体大小不合适，可以自己进行修改。

另外，VS Code 的终端字体，也需要进行配置，打开 VS Code，按`Command + ,`键，打开用户配置，搜索`fontFamily`，然后将右边的配置增加`"terminal.integrated.fontFamily": "Meslo LG M for Powerline"`，示例：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124651285-113264887.png)

## 5. 声明高亮

效果就是上面截图的那样，特殊命令和错误命令，会有高亮显示。

使用 Homebrew 安装：

```
$ brew install zsh-syntax-highlighting
```

安装成功之后，编辑`vim ~/.zshrc`文件，在最后一行增加下面配置：

```
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124702378-701306768.png)

**注意：修改完成配置文件之后注意执行**`source ~/.zshrc`使之生效！！

## 6. 自动建议填充

这个功能是非常实用的，可以方便我们快速的敲命令。

配置步骤，先克隆`zsh-autosuggestions`项目，到指定目录：

```
$ git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
```

然后编辑`vim ~/.zshrc`文件，找到`plugins`配置，增加`zsh-autosuggestions`插件。

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124716003-211091713.png)

注：上面声明高亮，如果配置不生效的话，在`plugins`配置，再增加`zsh-syntax-highlighting`插件试试。

有时候因为自动填充的颜色和背景颜色很相似，以至于自动填充没有效果，我们可以手动更改下自动填充的颜色配置，我修改的颜色值为：`586e75`，示例：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124726566-1303342612.png)

效果：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124741660-319157353.png)

## 7. 左右键跳转

主要是按住`option + → or ←`键，在命令的开始和结尾跳转切换，原本是不生效的，需要手动开启下。

打开 iTerm2，按`Command + ,`键，打开 Preferences 配置界面，然后`Profiles → Keys → Load Preset... → Natural Text Editing`，就可以了。

## 8. iTerm2 快速隐藏和显示

这个功能也非常使用，就是通过快捷键，可以快速的隐藏和打开 iTerm2，示例配置（`Commond + .`）：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124752394-498404916.png)

## 9. iTerm2 隐藏用户名和主机名

有时候我们的用户名和主机名太长，比如我的`xishuai@xishuaideMacBook-Pro`，终端显示的时候会很不好看（上面图片中可以看到），我们可以手动去除。

编辑`vim ~/.zshrc`文件，增加`DEFAULT_USER="xishuai"`配置，示例：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124824566-107795143.png)

我们可以通过`whoami`命令，查看当前用户，效果（另外分屏的效果）：

![img](https://images2017.cnblogs.com/blog/435188/201712/435188-20171228124832113-143056841.png)

## 10. iTerm2 配置代理

编辑`~ vim ~/.zshrc`，增加下面配置（使用的 shadowsocks）：

```
# proxy list
alias proxy='export all_proxy=socks5://127.0.0.1:1086'
alias unproxy='unset all_proxy'
```

iTerm2 需要新建标签页，才有效果：

```
$ proxy
$ curl ip.cn
当前 IP：185.225.14.5 来自：美国

$ unproxy
$ curl ip.cn
当前 IP：115.236.186.130 来自：浙江省杭州市 电信
```

我们可以测试下：

```
$ curl https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64

<html>
  <head>
    <title>Directory listing for /yum/repos/kubernetes-el7-x86_64/</title>
  </head>
  <body>
    <h2>Index of /yum/repos/kubernetes-el7-x86_64/</h2>
    <p></p>
    <a href="/yum/repos/kubernetes-el7-x86_64/repodata">repodata</a><br />
  </body>
</html>
```

## 11. iTerm2 快捷命令

快捷命令说明：

| 命令                                                 | 说明           |
| ---------------------------------------------------- | -------------- |
| command + t                                          | 新建标签       |
| command + w                                          | 关闭标签       |
| command + 数字 command + 左右方向键                  | 切换标签       |
| command + enter                                      | 切换全屏       |
| command + f                                          | 查找           |
| command + d                                          | 垂直分屏       |
| command + shift + d                                  | 水平分屏       |
| command + option + 方向键 command + [ 或 command + ] | 切换屏幕       |
| command + ;                                          | 查看历史命令   |
| command + shift + h                                  | 查看剪贴板历史 |
| ctrl + u                                             | 清除当前行     |
| ctrl + l                                             | 清屏           |
| ctrl + a                                             | 到行首         |
| ctrl + e                                             | 到行尾         |
| ctrl + f/b                                           | 前进后退       |
| ctrl + p                                             | 上一条命令     |
| ctrl + r                                             | 搜索命令历史   |

参考资料：

- [iTerm2 + Oh My Zsh + Solarized color scheme + Meslo powerline font + [Powerlevel9k\] - (macOS)](https://gist.github.com/kevin-smets/8568070)（**推荐**）
- [iTerm2 + oh my zsh + solarized + Meslo powerline font (OS X / macOS)](https://www.jianshu.com/p/0ff3269bc261)
- [Mac 下终端配置（item2 + oh-my-zsh + solarized 配色方案）](http://zhuxin.tech/2017/09/21/zsh%E9%85%8D%E7%BD%AE/)
- [MAC 下 iTerm 主题配置](https://www.zybuluo.com/Sweetfish/note/636550)
- [iTerm2 快捷键大全](https://cnbin.github.io/blog/2015/06/20/iterm2-kuai-jie-jian-da-quan/)

-------

# 二部分

（1）现在假设大家都安装了iTerm2，我们先把bash切换成zsh，使用命令行如下：

> chsh -s /bin/zsh

执行命令后，会让你输入电脑的密码，输入即可。完成后，需要完全退出iTerm2,再次进入时，就已经从bash切换到zsh了。当然，如果你哪一天又想用bash了，也可以使用下列命令：

> chsh -s /bin/bash

切换成功后，退出，再次进入的时候就切换bash成功了，相互切换是不是很方便呢？

如果你想看看自己的机子上装了哪些shell，可以使用如下命令：

> cat /etc/shells

我的显示如下：

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh

（2）安装 oh my zsh

Zsh和bash一样，是一种Unix shell，但大多数Linux发行版都默认使用bash shell。但Zsh有强大的自动补全参数和自定义配置功能等等，Github地址：<https://github.com/robbyrussell/oh-my-zsh>，可以让我们非常快速的上手zsh。不得不说，这个oh my zsh真的是牛逼哄哄，去看看上面的star就知道了。个人推荐使用curl自动安装，执行命令行如下：

> curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

（3）至此，iTerm2安装完毕、zsh已经切换成功、oh my zsh也已经安装OK。大家命令行的效果就应该如我上图所示了。是不是我们这篇博客就应该结束了呢？这样的话我们这篇博客的意义就不大了。下面我们来详细的讲讲如何高逼格的使用iTerm2,让我们的工作效率高起来。

【1.选中即复制】

在iTerm2中，直接用鼠标选中某个单词或者一行命令，那么就已经被复制了。不需要在去按command+C命令了。

【2.屏幕分隔】

这个是我最喜欢的iTerm2的功能，分隔成多个屏幕，只要你电脑的屏幕足够大，想分多少个屏幕都可以。可以同时进行命令行操作，而不会像只有在一个屏幕时，因为一个命令或者网络下载阻塞了，而不能执行其他命令了。如果你同时想去执行很多命令，那么，do it.

> command+d:垂直分割；

> command+shift+d:水平分割

![img](https://img-blog.csdn.net/20160110170738241?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)。

【3.快速唤出】

这个同样是我很喜欢的功能，炫酷到无法阻挡。设置好系统热键之后，只要按快捷键，iTerm2就会从顶部以半透明的形式快速唤出，相当炫酷高效。个人因为经常使用iTerm2，所以设置了热键为：option+空格键。大家也可以根据自己的喜好设置快捷键。

![img](https://img-blog.csdn.net/20160110171614291?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)。

使用快捷键快速唤出的效果。。。貌似是直接浮动在窗口上的，我截不了屏。。。大家尝试去感受下。

【4.显示复制历史】

使用快捷键shift+command+h,快速显示出我复制过的历史记录，你可以快速选择使用。

![img](https://img-blog.csdn.net/20160110173508688?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)。

【5.全屏切换】

command+enter,可以快速实现全屏与正常窗口大小的切换，非常方便。