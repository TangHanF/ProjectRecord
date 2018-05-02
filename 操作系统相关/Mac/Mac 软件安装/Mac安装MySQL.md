1. 下载mysql for mac: <https://dev.mysql.com/downloads/mysql/>
2. 双击mysql-5.7.17-macos10.12-x86_64.dmg进行解压, 双击mysql-5.7.17-macos10.12-x86_64.pkg进行安装

![img](https://img-blog.csdn.net/20170208092830245?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGFuc2FuZGF5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

3. Continue -> Continue, Agree -> Install -> 输入管理员密码


4. 记录下来弹窗中的密码

![img](https://img-blog.csdn.net/20170208092926818?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGFuc2FuZGF5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

5.  进入系统偏好设置, 找到mysql, 启动服务

![img](https://img-blog.csdn.net/20170208092957553?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGFuc2FuZGF5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

6. 将mysql的命令添加到系统中

   1) 进入/usr/local/mysql/bin,查看此目录下是否有mysql

   2) 执行vim ~/.bash_profile
       在该文件中添加mysql/bin的目录

> PATH=$PATH:/usr/local/mysql/bin

添加完成后，按esc，然后输入wq保存。
(3).最后在命令行输入`source ~/.bash_profile`

7. 通过mysql -uroot -p登录mysql, 输入之前保存的密码
8. 重置mysql初始密码

> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword');  

参考文章:

mac安装mysql的两种方法: <http://www.jianshu.com/p/fd3aae701db9>