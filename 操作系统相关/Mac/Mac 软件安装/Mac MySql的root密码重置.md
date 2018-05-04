停止MySQL的服务，打开系统的偏好设置，找到MySQL 进去后，点击Stop MySQL Server即可。

 ![](https://ws4.sinaimg.cn/large/006tKfTcly1fqymm8r4cfj30jg0ammy5.jpg)

开启两个终端，在第一个终端输入`sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables`，输入当前用户的密码，如下图所示

![](https://ws3.sinaimg.cn/large/006tKfTcly1fqymmwvqsnj30hy05cwf5.jpg)

然后在第二个终端输入`sudo /usr/local/mysql/bin/mysql -u root`，然后输入当前用户的密码后，出现以下的界面

![](https://ws3.sinaimg.cn/large/006tKfTcly1fqymouhx3pj30hz09o0u3.jpg)

然后输入命令`UPDATE mysql.user SET authentication_string=PASSWORD('新密码') WHERE User='root';`回车，出现以下的界面，说明修改成功。

![](https://ws3.sinaimg.cn/large/006tKfTcly1fqympcy4zqj30ia03ydg3.jpg)

接下来输入`FLUSH PRIVILEGES;`回车，出现下面的界面

![](https://ws2.sinaimg.cn/large/006tKfTcly1fqympuu2n2j30ag02hjrd.jpg)

最后，输入`\q`，退出。关闭第一个终端，回到系统的偏好设置，重新开启MySQL即可。

![](https://ws3.sinaimg.cn/large/006tKfTcly1fqymqcepc3j3051026jr7.jpg) 



 

 

 

 