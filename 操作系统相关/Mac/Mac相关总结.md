# Mac Office破解

https://blog.csdn.net/qq_34621169/article/details/79365247

# Mac剪切操作

1. `⌘+C` 复制选择项
2. `⌥+⌘+V` 然后粘贴 

# Finder标题栏显示路径

## 在Finder标题栏显示路径

> defaults write com.apple.finder _FXShowPosixPathInTitle -bool TRUE;killall Finder

## 关闭显示路径

> defaults delete com.apple.finder _FXShowPosixPathInTitle;killall Finder

以上命令执行完毕需要在执行 `killall Finder`

# quickplay自动播放

> defaults write com.apple.QuickTimePlayerX MGPlayMovieOnOpen 1

Quickplay插件，播放各种视频格式

http://www.mac52ipod.cn/post/Perian-QuickTime-AVI-Flv-MkV.php



# **Mac**常用快捷键符号

`⌘`（command）

`⌥`（option）

`⇧`（shift）

`⇪`（caps lock）

`⌃`（control）

`↩`（return）

`⌅`（enter）



# Mac 终端自定义命令

> vim ~/.bash_profile

输入一下内容

> alias ll='ls -alF'
>
> alias la='ls -A'
>
> alias l='ls -CF

保存完成之后重新加载，使之生效：

> source ~/.bash_profile

# Command+T打开、新建标签

- 浏览器
- 终端
- 办公软件等等

-----

# Git SSL错误解决

错误信息：

> error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 60

解决方案：

> **env GIT_SSL_NO_VERIFY=true** git clone https://<host_name/git/project.git
>
> git config --global http.sslVerify false

# Launchpad图标大小调整

**终端输入**

**改变行数：**`defaults write com.apple.dock springboard-rows -int X`

**改变列数：**`defaults write com.apple.dock springboard-columns -int X`

**改变生效：**`killall Dock`

其中X是大于0的整数。根据自己喜好调整即可。

**恢复默认**

```bash
defaults write com.apple.dock springboard-rows Default
defaults write com.apple.dock springboard-columns Default
killall Dock
```

![](https://ws4.sinaimg.cn/large/006tNc79ly1fqxedjuce9j30jg0c675w.jpg)



# HomeBrew-OS X 不可或缺的套件管理器

## 1.安装

 中间会按RETURN键，输入密码

![](https://ws3.sinaimg.cn/large/006tNc79ly1fqxe8tugyjj31bm13uqia.jpg)

## 2.卸载

$ cd `brew --prefix`

$ rm -rf Cellar

$ brew prune

$ rm `git ls-files`

$ rm -rf .git

$ rm -rf ~/Library/Caches/Homebrew



HomwView简介、安装、使用

## 一、Homebrew是什么

Homebrew是一款Mac OS平台下的软件包管理工具，拥有安装、卸载、更新、查看、搜索等很多实用的功能。简单的一条指令，就可以实现包管理，而不用你关心各种依赖和文件路径的情况，十分方便快捷。

援引[官方](http://brew.sh/)的一句话：又提示缺少套件啦？别担心，Homebrew 随时守候。Homebrew – OS X 不可或缺的套件管理器。

## 二、Homebrew安装

### 1. 要求

- Intel CPU [1](https://blog.csdn.net/andanlan/article/details/51589800#fn:cpu)

- OS X 10.9 or higher [2](https://blog.csdn.net/andanlan/article/details/51589800#fn:os-x)

- Xcode命令行工具 [3](https://blog.csdn.net/andanlan/article/details/51589800#fn:xcode)

  ```
  $ xcode-select --install
  12
  ```

  ​

- 支持shell (sh或者bash) [4](https://blog.csdn.net/andanlan/article/details/51589800#fn:shell)

### 2. 安装和卸载

- 安装

  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  12
  ```

- 卸载

  ```
  $ cd `brew --prefix`
  $ rm -rf Cellar
  $ brew prune
  $ rm `git ls-files`
  $ rm -r Library/Homebrew Library/Aliases Library/Formula Library/Contributions
  $ rm -rf .git
  $ rm -rf ~/Library/Caches/Homebrew1234567
  ```

## 三、Homebrew基本使用

### 安装任意包

```
$ brew install <packageName>
12
```

示例：安装wget

```
$ brew install wget
12
```

### 卸载任意包

```
$ brew uninstall <packageName>
12
```

示例：卸载git

```
$ brew uninstall git
12
```

### 查询可用包

```
$ brew search <packageName>
12
```

### 查看已安装包列表

```
$ brew list
12
```

### 查看任意包信息

```
$ brew info <packageName>
12
```

### 更新Homebrew

```
$ brew update
12
```

### 查看Homebrew版本

```
$ brew -v
12
```

### Homebrew帮助信息

```
$ brew -h
12
```

输出示例:

```
Example usage:
  brew search [TEXT|/REGEX/]
  brew (info|home|options) [FORMULA...]
  brew install FORMULA...
  brew update
  brew upgrade [FORMULA...]
  brew uninstall FORMULA...
  brew list [FORMULA...]

Troubleshooting:
  brew config
  brew doctor
  brew install -vd FORMULA

Brewing:
  brew create [URL [--no-fetch]]
  brew edit [FORMULA...]
  https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Formula-Cookbook.md

Further help:
  man brew
  brew help [COMMAND]
  brew home1234567891011121314151617181920212223
```

## 四、注意

在Mac OS X 10.11系统以后，/usr/local/等系统目录下的文件读写是需要系统root权限的，以往的Homebrew安装如果没有指定安装路径，会默认安装在这些需要系统root用户读写权限的目录下，导致有些指令需要添加sudo前缀来执行，比如升级Homebrew需要：

```
$ sudo brew update
12
```

如果你不想每次都使用sudo指令，你有两种方法可以选择:

1. 对/usr/local 目录下的文件读写进行root用户授权

   ```
   $ sudo chown -R $USER /usr/local
   12
   ```

   示例：

   ```
   $ sudo chown -R wentianen /usr/local
   12
   ```

2. （推荐）安装Homebrew时对安装路径进行指定，直接安装在不需要系统root用户授权就可以自由读写的目录下

   ```
   <install path> -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   12
   ```

## 参考

- [Homebrew官方推荐使用教程](http://brew.sh/index_zh-cn.html)
- [安装卸载homebrew](http://www.cnblogs.com/chenjunbiao/archive/2011/07/11/2102899.html)
- [官方源码库](https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Installation.md)

# 更改app图标

- 先复制你喜欢的app图标。操作：按 `⌘+i` 打开app的简介，点击左上角的app图标，⌘+c 复制

- 在目标app简介中的图标上粘贴即可
- 点击app简介中的图标按下`⌘+⌫`即可还原图标

