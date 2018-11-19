**1、下载maven包：**

　　下载链接：🔗<http://maven.apache.org/download.cgi>

　　maven下载文件释义：

　　　　1⃣️ Binary tar.gz archive：是装在Linux、MacOsX上的。

　　　　2⃣️ Binary zip archive：是装在windows上的。

 　  　　3⃣️ binary表示编译后的二进制文件，一般比较小，适合直接在项目中使用，

　　　　4⃣️ source表示可以查看源代码的，比binary大一些，如果你想看一下maven的源码可以下载这一类的 .

 

**2、配置maven环境变量（首先要确保java环境变量已经配置好）：**

　　　　1⃣️ 先双击Binary tar.gz archive文件，解压到文件目录下；

　　　　2⃣️ 查看文件路径：1）首先，打开终端；

　　　　　　　　　　　　 2）再将apache-maven-3.5.0 文件夹拖入到终端内，文件夹路径就会显示出来；

　　　　3⃣️ 在终端打开配置环境变量到文件：

　　　　　　　               1）在终端输入  vim ~/.bash_profile，进入到环境变量配置文件里面；

　　　　　　　　　　　 2）进入后，是read模式，按下 i (编辑)键，进入insert模式；

　　　　　　　　　　    3）将环境变量加入其实，环境变量如下：

　　　　　　　　　　　　　　export MAVEN_HOME=/Users/robbie/apache-maven-3.3.3

　　　　　　　　　　　　　　export PATH=$PATH:$MAVEN_HOME/bin

　　　　　　　　　　　 4）按下 ESC，退出insert模式；

　　　　　　　　　　　 5）输入 :wq (保存修改)退出当前文件；

　　　　　　　　　　　 6）使修改的环境变量bash_profile文件生效，输入 source .bash_profile，按下Enter键即可.

 

 