# 安装 homebrew

- 官网：[https://brew.sh](https://link.zhihu.com/?target=https%3A//brew.sh)
- 打开苹果终端，在终端输入 

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#  重新安装

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

-----

# 替换及重置Homebrew默认源

$brew update 慢？来试试用 Coding 家的 Homebrew 源吧！( 该源每 5 分钟和上游同步一次，依托 Coding 遍布全国的 Git 服务节点（在 [http://Coding.net](https://link.zhihu.com/?target=http%3A//Coding.net)push & pull 仓库代码的速度也是同样的快），让你的 brew update 更快！）

```
cd "$(brew --repo)" && git remote set-url origin https://git.coding.net/homebrew/homebrew.git

$ cd $home && brew update
```

--------

```
替换brew.git:
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git


替换homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

替换Homebrew Bottles源: 参考:[替换Homebrew Bottles源](https://lug.ustc.edu.cn/wiki/mirrors/help/homebrew-bottles)

在中科大源失效或宕机时可以： 1. 使用[清华源设置参考](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)。 2. 切换回官方源：

```
重置brew.git:
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

重置homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```

注释掉bash配置文件里的有关Homebrew Bottles即可恢复官方源。 重启bash或让bash重读配置文件。



------

# 通过

在mac系统中，使用homebrew可以很方便的管理包。按照官网的说明执行以下命令时总是报错： 
`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

应该是这个资源访问有问题，那么我们可以尝试使用国内的镜像。给大家推荐一个中科院的镜像站点，里面有各种资源： 
<https://mirrors.ustc.edu.cn/brew.git> 

言归正传，开始踩坑

### 第一步，获取install文件

把官网给的脚本拿下来 
`curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install`

### 第二步，更改脚本中的资源链接，替换成清华大学的镜像

就是把这两句 
BREW_REPO = “<https://github.com/Homebrew/brew>“.freeze 
CORE_TAP_REPO = “<https://github.com/Homebrew/homebrew-core>“.freeze 
更改为这两句 
BREW_REPO = “<https://mirrors.ustc.edu.cn/brew.git> “.freeze 
CORE_TAP_REPO = “<https://mirrors.ustc.edu.cn/homebrew-core.git>“.freeze 
当然如果这个镜像有问题的话，可以换成别的

### 第三步，执行脚本

`/usr/bin/ruby brew_install`

然后可以看到这几句： 

==> **Tapping homebrew/core**

Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...

fatal: unable to access 'https://github.com/Homebrew/homebrew-core/': LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54

Error: Failure while executing: git clone https://github.com/Homebrew/homebrew-core /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

Error: Failure while executing: /usr/local/bin/brew tap homebrew/core

liyuanbadeMacBook-Pro:~ liyuanba$ git clone https://github.com/Homebrew/homebrew-core /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

出现这个原因是因为源不通，代码来不下来，解决方法就是更换国内镜像源：

执行下面这句命令，更换为中科院的镜像：

 git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

就下载成功了

然后把

homebrew-core

的镜像地址也设为中科院的国内镜像

cd "$(brew --repo)" 

git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

 

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" 

git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

执行更新，成功：

brew update

最后用这个命令检查无错误：

brew doctor

 