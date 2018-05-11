# Homebrew

## 简介

macOS 缺失的软件包管理器。使用 Homebrew 安装 Apple 没有预装但 [你需要的东西](https://github.com/Homebrew/homebrew-core/tree/master/Formula)。[官网](https://brew.sh/)有中文说明。

## 安装与配置

Homebrew 的安装非常简单，将下面这条命令粘贴到终端：

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

等待命令执行完毕。其他配置见[官网中文说明](https://brew.sh/index_zh-cn.html)。

## 常用命令

1. `brew help` 查看帮助
2. `brew install <package name>` 安装软件包
3. `brew uninstall <package name>` 卸载软件包
4. `brew list [--versions]` 列出已安装的软件包(包括版本)
5. `brew search <package name>` 查找软件包
6. `brew info <package name>` 查看软件包信息
7. `brew update` 更新brew
8. `brew outdated` 列出过时的软件包（已安装但不是最新版本）
9. `brew upgrade [<package name>]` 更新过时的软件包（不指定软件包表示更新全部）
10. `brew doctor` 检查brew运行状态

## 常用软件

```
brew install wget
brew install curl
brew install openssl

brew install fish      #安装fish shell
brew install git-flow  #安装git-flow
brew install python    #安装python
```

## Homebrew-Cask

Homebrew-Cask 是 Homebrew 的一个扩展。它能够优雅、简单、快速的安装和管理 macOS 图形界面程序，比如Google Chrome 和Dropbox等等。官网 [https://caskroom.github.io/。](https://caskroom.github.io/%E3%80%82)

### Cask 必装的理由

有图形界面的软件可以直接在 App Stroe 中下载更新，为啥还需要 Cask 呢？因为有的很好用的免费 Mac 软件并没有选择在 App Store 上架，对于没有上架的软件我们只能是通过搜索找到官网然后在下载安装包，这样不够优雅也不方便管理，而使用 Cask 可以通过一行命令就搞定安装了，还可以统一更新升级所有的软件，实现从非 App Store 途径安装的软件的统一管理。
Cask 从软件官方网站下载软件包，然后在后台安装并将 `.app` 移动到 `Applications`。通过 Cask 安装的软件也会在 Lanuchpad 显示，跟从 App Store 安装的软件没啥区别。对于那些收费的软件，用 Cask 安装只是比普通安装方法节省了时间和步骤，没啥其他的区别。

### Cask 常用命令

1. `brew cask -help` 查看帮助
2. `brew cask install <software name>` 安装软件
3. `brew cask uninstall <software name>` 卸载软件
4. `brew cask search <software name>` 搜索软件
5. `brew cask info <software name>` 查看软件相关信息
6. `brew cask list` 列出通过 Homebrew-Cask 安装的包

> 经过测试，虽然 `-help` 是未知命令，但是仍然可查看 Cask 的命令，其他帮助命令（如 `brew cask -h` 和 `brew cask --help`）好像都不行。还有其他的命令就不一一介绍了，其他命令可以通过`brew cask -help`查看。

### Cask 常用软件

```
brew cask install iterm2         #安装iTerm 2
brew cask install launchrocket   #管理软件后台服务
brew cask install google-chrome  #安装Chrome
brew cask install the-unarchiver #解压软件
brew cask install alfred         #效率软件
brew cask install qq             #腾讯QQ
brew cask install evernote       #云笔记软件
brew cask install sublime-text   #文本编辑器
brew cask install skitch         #ervernote配套的截图软件
brew cask install dropbox        #文件同步软件
brew cask install zotero         #网页收藏与文献管理软件
brew cask install anki           #记忆软件
brew cask install virtualbox     #虚拟机，可以装个Windows
brew cask install self-control   #避免分心的软件
brew cask install vlc            #视频软件
brew cask install appcleaner     #应用清理

#Quick Look 系列
brew cask install qlcolorcode    #预览脚本时自动代码配色
brew cask install qlstephen      #预览未知拓展名的纯文本文件
brew cask install qlmarkdown     #预览Markdown文件
brew cask install quicklook-json #预览JSON文件
brew cask install quicklook-csv  #预览CSV文件
```

Homebrew-Cask 是一个开源项目，其详细信息可以看[其开源项目介绍](https://github.com/caskroom/homebrew-cask)，所支持的软件列表在这里：<https://github.com/caskroom/homebrew-cask/tree/master/Casks> 。
如果觉得管理软件在后台运行的服务很麻烦，可以装个[LaunchRocket](https://github.com/jimbojsb/launchrocket)，这也是个开源项目。
关于 Quick Look 的介绍可以看这篇文章[加强你的「一指禅」：Mac QuickLook「快速预览」兼容性扩展教程](https://sspai.com/post/31927)，同时[Quick Look plugins](https://github.com/sindresorhus/quick-look-plugins)这个开源项目列出了所有支持 Homebrew-Cask 的 Quick Look 扩展，据说支持的都是程序员必备。

## 轻松实现一键装机

在使用 Mac 的过程中，总想着有没有方便、简单的办法实现在不同Mac 上同步开发环境的办法，今天在整理 Homebrew 使用笔记的时候突然冒出一个想法，如果我把所有的 Homebrew 安装命令列成一个清单形式，当在另一台新的 Mac 上工作时，那么就可以先装一个 Homebrew 然后将命令清单中的所有命令复制粘贴到终端中，等待命令执行完毕后，新的 Mac 的大部分开发环境就跟常用的 Mac 开发环境一致了。下面列出笔者的常用命令清单：

```
#安装 Homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#安装基础套件
brew install fish      #安装fish shell
brew install git-flow  #安装git-flow
brew install python    #安装python

#Homebrew-Cask
brew tap caskroom/cask

# 安装Cask基础软件
brew cask install iterm2         #安装iTerm 2
brew cask install visual-studio-code#微软出品的文本编辑器，可替代 Sublime Text
brew cask install google-chrome  #安装Chrome
brew cask install the-unarchiver #解压软件
brew cask install alfred         #效率软件
brew cask install qq             #腾讯QQ
brew cask install sourcetree     #Git GUI 客户端
brew cask install cheatsheet     # 显示当前程序的快捷键列表，默认的快捷键是长按⌘
```

这份清单会随着我对 Mac 的不断深入了解而持续更新，欢迎关注 [Sheh 伟伟的个人博客](https://davidsheh.github.io/)。

## 参考资料

[Mac 开发配置手册](https://aaaaaashu.gitbooks.io/mac-dev-setup/content/Homebrew/index.html)

------

**同系列文章**

[Mac开发必备工具（一）—— Homebrew](http://davidsheh.github.io/2017/08/26/mac-homebrew/)

[Mac开发必备工具（二）—— iTerm 2](http://davidsheh.github.io/2017/08/27/mac-iterm2/)

[Mac开发必备工具（三）—— Fish shell](http://davidsheh.github.io/2017/08/28/mac-fishshell/)