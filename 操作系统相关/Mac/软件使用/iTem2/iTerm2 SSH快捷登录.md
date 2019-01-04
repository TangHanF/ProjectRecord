# iTerm2 ssh快捷登录

ssh连接命令：`ssh -p端口号 用户名@服务地址`，例如：ssh -p22 root@172.16.1.21，然后输入密码即可。但是每次这么输入感觉太麻烦，我们可以把相关信息保存，然后自动选择连接。

编辑以下脚本并保存：

```
#!/usr/bin/expect -f 
set host 服务器地址 
set port 端口 
set user 用户名 
set password 用户密码 
set timeout -1 

spawn ssh -p$port $user@$host 
expect "assword:" 
send "$password\r" 
interact 
expect eof 
```



**语法说明**：

  上面的set 是定义变量

  下方的 spawn是调用命令，在命令中使用上述定义好的变量

## iTerm设置部分

iTerm -- preferences 打开设置界面

![image-20181225094300042](https://ws4.sinaimg.cn/large/006tNbRwly1fyiqwrasz1j31cz0u0k67.jpg)

![image-20181225094339937](https://ws4.sinaimg.cn/large/006tNbRwly1fyiqxbusu5j314c0bi14f.jpg)

然后直接连接即可