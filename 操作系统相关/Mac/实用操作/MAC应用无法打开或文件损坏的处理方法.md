

​	在MAC下安装一些软件时提示"来自身份不明开发者"，其实这是MAC新系统启用了新的安全机制。
默认只信任 **Mac App Store** 下载的软件和拥有开发者 ID 签名的应用程序。
换句话说就是 MAC 系统默认只能安装靠谱渠道（有苹果审核的 **Mac App Store**）下载的软件或被认可的人开发的软件。

​	这当然是为了用户不会稀里糊涂安装流氓软件中招，但没有开发者签名的 “老实软件” 也受影响了，安装就会弹出下图所示警告框：“打不开 xxx，因为它来自身份不明的开发者”。

![来自身份不明的开发者](https://ws2.sinaimg.cn/large/006tNbRwly1fwk9gbuqtpj30nc0b6dgh.jpg)

**出现这个问题的解决方法有2种：**

1. 最简单的方式：按住Control后，再次点击软件图标，即可。
2. 修改系统配置：系统偏好设置... -> 安全性与隐私。

**系统偏好设置**

![系统偏好设置](https://ws2.sinaimg.cn/large/006tNbRwly1fwk9gexh62j30os0m6ae7.jpg)

**安全性与隐私**

![安全性与隐私](https://ws1.sinaimg.cn/large/006tNbRwly1fwk9gcnaiij30oe0jqtbd.jpg)

**认证**

![认证](https://ws4.sinaimg.cn/large/006tNbRwly1fwk9gdzy3yj30om0cwjs4.jpg)

**修改为任何来源**



## 如果没有这个选项的话（macOS Sierra 10.12）,打开`终端`，输入`sudo spctl --master-disable`然后按`回车`。然后会看见个password后面还有个钥匙图标，然后不用管他直接再继续输入你自己电脑解锁密码（输入的时候不显示你输入的密码，感觉就是输入不了东西一样，也不用管，凭感觉输入完按回车键）。然后再回到隐私里，就看见任何来源了。

![修改为任何来源](https://ws4.sinaimg.cn/large/006tNbRwly1fwk9gee0rbj30oe0js77b.jpg)