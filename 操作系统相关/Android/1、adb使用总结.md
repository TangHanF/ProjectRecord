#### 前言

> ADB是android debug bridge的缩写，负责计算机与Android设备的几乎所有通信和协作，可以认为是连接两者的桥梁。

#### ADB源码

用了那么久的adb，你知道adb源码在哪里吗？那你又有看过看过adb源码吗？

没关系，链接如下：
http://androidxref.com/8.0.0_r4/xref/system/core/adb/

#### ADB命令分类

详细使用可查看：
http://adbshell.com/commands/adb-forward

**ADB Debugging**

- adb devices
- adb forward
- adb kill-server

**Package Manger**

- adb install
- adb uninstall
- adb shell pm list packages
- adb shell pm path
- adb shell pm clear

**Wireless**

- adb connect
- adb usb

**File Manager**

- adb pull
- adb push
- adb shell ls
- adb shell cd
- adb shell rm
- adb shell mkdir
- adb shell touch
- adb shell pwd
- adb shell cp
- adb shell mv

**Network**

- adb shell netstat
- adb shell ping
- adb shell netcfg
- adb shell ip

**Logcat**

- adb logcat
- adb shell dumpsys
- adb shell dumpstate

**Screenshot**

- adb shell screencap
- adb shell screenrecord [4.4+]

**System**

- adb root
- adb sideload
- adb shell ps
- adb shell top
- adb shell getprop
- adb shell setprop

#### ADB命令的常见使用场景

##### 01

某日产品经理小李找到你说：“小王，给我来几张我们的APP截图。” ，只听见小王麻溜敲打着键盘，使用`adb shell screencap /sdcard/xiaoli/001.png`和`adb pull /sdcard/xiaoli/001.png`。

在这个场景里小王使用到`adb shell screencap` **截屏**和`adb pull` **文件传输**两个命令。

##### 02

我们的APP要上线了，但是因为项目十分庞大，说不准我们的小王写的代码没有把Log关闭，怎么办呢？来吧，在命令行里看一下

```
adb logcat | grep com.xxx.xxx
```

接下来你就在APP里乱点把，看看有没有一些尚未关闭的Log。

在Android逆向工程中，我们也可以通过这种方式，利用那些大意而留下来的Log信息进行相关的逻辑分析。

##### 03

某日，那个叫做小李的产品经理又找到你说:“小王，你帮我在电脑上下载了一个APP装到手机上”

二话不说，小王下载好app使用`adb install xxx.apk`进行安装。

But,出问题了，需要指定手机。原来，小王的电脑上连接了两个手机。

`adb devices`大显身手，原来小李的手机编号是"Sx1xxx2xxxx"。

接下来，小王使用`adb -s Sx1xxx2xxxx install xxx.apk`

##### 04

短平快的教你通过局域网WIFI连接手机。

- 前提需要USB连接手机。
- adb tcpip 5555
- adb connect #.#.#.#(你手机的IP地址)
- 拔掉USB，你已经成功通过WIFI连接了。(其实背后是通过TCP协议来实现的)

--------

安装APK
`adb install xxx.apk`

清除已经安装的APK并安装新的APK
`adb install -r test.apk`

卸载APK
`adb uninstall package_name`

清除指定APP的缓存
`adb shell pm clear package_name`

输出指定包名APP的安装位置
`adb shell pm path package_name`

输出手机中所有的包名
`adb shell pm list packages`

查看指定包名的内存信息
`adb shell dumpsys meminfo package_name`