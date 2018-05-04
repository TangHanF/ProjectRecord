# 查看某个端口运行的程序

> lsof -i :端口号

`-i`参数表示网络链接,该命令会同时列出PID，然后配合`kill -9 PID`值结束程序即可

![](https://ws4.sinaimg.cn/large/006tNc79ly1fqy97w43lij310g0363z9.jpg)

