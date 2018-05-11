# Mac 系统重装的一些坑

对于 Mac 用户来说，因为有 Time Machine 所以很少有必要全新安装，很多时候只需要从备份恢复就能满血复活，不过 Time Machine 也不是绝对靠谱的，印象中就经历过两次备份损坏导致无法还原的情形。换个角度来看，隔几年全新安装一次对系统是次优化和净化，说不定还能挖出很多使用习惯和文件备份上的坑。

## 第一时间恢复网络环境

准备重新整理系统之前，已经启用了 iCloud Drive，文档、桌面这些都已同步到云端；共享资源和应用软件配置信息保存在 Dropbox；协作的少量文档保存在 Google Drive；公司台式机和 MacBook 之间交换的公司文档保存在 OneDrive。规划主次依旧是 iCloud Drive、Dropbox、Google Drive、OneDrive，所有这些云端数据要下载到新的系统，网络环境必须顺畅和高速才有效率。

还有一个要优先恢复网络的原因是 Mail.app，大量软件的授权都是保存在 Gmail 邮件当中的，如果不能把邮件同步下来软件安装的时候就会卡壳。

iCloud Drive 中包含很多第三方应用的文档，例如：Surge 的配置，恢复科学上网离不开这些配置文件，另外一个经验就是 Surge 程序包最好也在这个文件夹里放一份，这样系统恢复后 iCloud 文档同步到本地后便于快速安装和恢复网络环境。

![img](https://cdn.sspai.com/2017/06/14/4ba019146b629880cf6e7f33eacb0b3b.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

最保险的方式是在移动硬盘中也保存一份常用软件和配置，例如：Surge 和其配置文件、Dropbox 离线安装包、1Password、Telegram Desktop、Keka。

> 如果启用了两步验证，手头还要准备好网络畅通的手机。Dropbox、Google、OneDrive 这些支持两步验证的应用安装时需要输入验证码，需要在手机上打开管理 OTP（One-Time Password）的应用，例如：1Password、Google Authenticator。

## 排除在备份之外的文件

虚拟机的文件过大，从来 Time Machine 的设置里都是将其排除在外的，另外我的设置中还排除了「下载」文件夹，下载文件夹还兼做临时文件夹使用。Telegram 的本地存储默认也是下载文件夹，重整系统前需要检查确认。

启用 iCloud Drive 的文稿和桌面同步后，DEVONthink 的库文件也和 Parallels Desktop 虚拟机文件一样被自己迁移到了用户目录的根目录下，如果是单独备份的也需要核实一次。

![img](https://cdn.sspai.com/2017/06/14/9b23b5a67c0b877e0d27add5552a8769.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

主动备份环节最头疼的是文件的复制速度。虚拟机的文件很大，下载的高清电影也很大，如果不复制到移动硬盘上，等恢复系统后它们就都没有了，手动备份又需要漫长的拷贝传输过程，所以 WiFi 传输就不要考虑了，至少用 USB 3.0 以上速率的移动硬盘或者直接用网线连接进行备份。

## 由 Time Machine 备份里单独提取文件

双击 Time Machine 备份（ .sparsebundle 后缀的文件）可以将备份作为一个磁盘镜像加载上，加载成功后可在 Finder 边栏的设备项下找到。

和访问其他磁盘镜像一样，我们可以在 TM 磁盘备份中查找所有已经备份的文件。如果系统不是从备份恢复安装的，很多时候我们还需要到其中查找文件。个人就经历过，全新安装发现音乐和有声读物全都没有了，只能打开对应的目录从「用户-音乐」里复制。

另外，平时我们主要关注的都是文档备份，很多应用的配置文件很容易被忽视，例如：Hazel 的规则、Alfred 的配置和扩展、Safari 的扩展（~/Library/Safari/Extensions）、aText 的短语配置、Snagit 的截图历史记录、PopClip 的扩展、鼠须管输入法的配置、Scrivener 模板、OmniGraffle 自定义型板等等。有些文件的位置很好找，有些就需要在新系统中导出后基于后缀来搜索判断文件位置，最后再到 TM 中定位复制出来。

![img](https://cdn.sspai.com/2017/06/14/7f442c6d39c67429326c7c48b25bff32.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

经历痛苦的翻找后，很有必要关照一下这么以前忽视的部分：能启用 iCloud 同步的都开启、能导出的导出一份到 Dropbox 文件夹。

## iCloud 照片图库

全新安装后「照片」应用中 iCloud 照片图库默认是关闭的，按照 iCloud 照片图库的同步策略，勾选打开「iCloud 照片图库」后，照片应用会先上传本地的照片然后再下载新的照片，所以在同步完成前，最好不要单独导入照片，避免产生重复。

重做系统前我手动备份了整个照片图库文件（保存到移动硬盘），同时手动备份的还有 Pixave 的图库和 Snagit 的截图自动存储文件夹。系统安装好后，直接将图库复制到图片文件夹下，然后再打开「照片」应用启用 iCloud 照片同步。「照片」应用的底部能看到上传照片的进度提示，这个过程会持续一段时间，直到云端完成比对后才会提示更新完成。

iCloud 照片图库会遵序任务队列的方式来完成上传、下载等动作，所以在同步完成期间最好不要手动导入手机中的照片， iPhone、Mac 上启用「iCloud 照片图库」后，照片会逐步完成同步，只需要等待就好（网络环境很重要）。

其实一直比较好奇 iCloud 照片库的运作方式，每次因为各种原因关闭 iCloud 后再打开都会看到照片应用各种「忙碌」，例如，提示正在上传 30GB 的照片，缓慢的进度让人很担心，不过转天再看就发现已经都完成了。猜想 iCloud 只是上传数据进行比对发现一致就完成了，所以别被同步进度吓着，数据处理上 iCloud 还是很智能的。

## MAS 之外的安装包

MAS 里的应用安装和恢复是最简单的，在「已购」里点击安装就可以。比较费事的是 Mac App Store 之外的很多软件的安装。

了解 Homebrew 的可能会鄙视一下小白，直接 `brew cask install google-chrome`（安装 Google 浏览器的范例）多简单，命令行后面跟上软件名称一次就能搞定。常用的软件 Homebrew-Cask 几乎都支持（[支持应用搜索页](https://caskroom.github.io/search)），而且都是从官方源下载，安全性同样有保障。

使用 [Homebrew-Cask](https://caskroom.github.io/) 前提是已经安装 Xcode开发工具、[Homebrew](https://brew.sh/index_zh-cn.html)，感兴趣的可以 Google 搜索学习一下这种高效率的极客方式。

安装前推荐 Things 这样的任务管理软件罗列梳理一下所需要安装的软件，思考一下是否有必要让某些软件回归，请神容易送神难，安装前想好了总比安装后卸载好。

![img](https://cdn.sspai.com/2017/06/14/34eb8e07796c465b4166c9674eeb2763.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

图示中列出了自己这次安装下载的一堆软件，其实除了软件之外还有字体、Safari 扩展、词典文件以及鼠须管的配置等等。有些是之前备份没有考虑到的，字体就是从原来的 Time Machine 备份（~/资源库/Fonts）里临时挖出来的，移动硬盘上先前备份的字体太凌乱，而旧系统中是经过一段时间打磨留存下来的，所以最后还是从 Time Machine 里翻找了一次。

------

其实这次安装还有不少插曲：例如，为了充分发挥 iCloud 的功用，开启了Pixave 的 iCloud 同步，2000+ 的截图上传那个慢啊，痛苦的是此时 iCloud 照片库也在同步。

还有更糗的是降级前（macOS High Sierra）把移动硬盘格式化成了 APFS （加密），拷贝了 DEVONthink 、图库、Pixave 图库、Snagit 图库、Parallels Desktop 虚拟机等一堆大块头的文件，结果安装好 macOS Sierra 后发现根本没法访问这个磁盘，只能暗骂自己犯二。

鼠须管的安装也不太顺利，原想着只安装 Xcode 命令行工具就能编译，结果不行，最后依旧是等下载带宽空出来安装 Xcode 后才搞定。

 