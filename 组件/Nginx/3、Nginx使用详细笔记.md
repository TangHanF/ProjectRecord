# Nginx安装配置使用详细笔记前言

选择Nginx的优点：
	Nginx 可以在大多数 Unix like OS 上编译运行，并有 Windows 移植版。 Nginx 的1.4.0稳定版已经于2013年4月24日发布，一般情况下，对于新建站点，建议使用最新稳定版作为生产版本，已有站点的升级急迫性不高。Nginx 的源代码使用 2-clause BSD-like license。
	Nginx 是一个很强大的高性能Web和反向代理服务器，它具有很多非常优越的特性。
	在高连接并发的情况下，Nginx是Apache服务器不错的替代品：Nginx在美国是做虚拟主机生意的老板们经常选择的软件平台之一。能够支持高达 50,000 个并发连接数的响应，感谢Nginx为我们选择了 epoll and kqueue作为开发模型。

CentOS6.2实战部署Nginx+MySQL+PHP [http://www.linuxidc.com/Linux/2013-09/90020.htm](https://www.linuxidc.com/Linux/2013-09/90020.htm)

使用Nginx搭建WEB服务器 [http://www.linuxidc.com/Linux/2013-09/89768.htm](https://www.linuxidc.com/Linux/2013-09/89768.htm)

搭建基于Linux6.3+Nginx1.2+PHP5+MySQL5.5的Web服务器全过程 [http://www.linuxidc.com/Linux/2013-09/89692.htm](https://www.linuxidc.com/Linux/2013-09/89692.htm)

CentOS 6.3下Nginx性能调优 [http://www.linuxidc.com/Linux/2013-09/89656.htm](https://www.linuxidc.com/Linux/2013-09/89656.htm)

CentOS 6.3下配置Nginx加载ngx_pagespeed模块 [http://www.linuxidc.com/Linux/2013-09/89657.htm](https://www.linuxidc.com/Linux/2013-09/89657.htm)

CentOS 6.4安装配置Nginx+Pcre+php-fpm [http://www.linuxidc.com/Linux/2013-08/88984.htm](https://www.linuxidc.com/Linux/2013-08/88984.htm)

Nginx搭建视频点播服务器（仿真专业流媒体软件） [http://www.linuxidc.com/Linux/2012-08/69151.htm](https://www.linuxidc.com/Linux/2012-08/69151.htm)


**查看进程数**

进程数是与top出来的cpu数量是一样的。在/usr/local/nginx/conf/nginx.conf配置文件里面的worker_processes参数。
worker_processes指明了nginx要开启的进程数，据官方说法，一般开一个就够了，多开几个，可以减少机器io带来的影响。据实践表明，nginx的这个参数在一般情况下开4个或8个就可以了，再往上开的话优化不太大。据另一种说法是，nginx开启太多的进程，会影响主进程调度，所以占用的cpu会增高。

1. [root@lb-net-2 ~]# `ps -eaf|grep nginx`
2. root 2221 1382 0 18:06 pts/0 00:00:00 grep nginx
3. root 16260 1 0 Jun18 ? 00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
4. nobody 16261 16260 0 Jun18 ? 00:01:26 nginx: worker process
5. nobody 16262 16260 0 Jun18 ? 00:01:32 nginx: worker process
6. nobody 16263 16260 0 Jun18 ? 00:01:25 nginx: worker process
7. nobody 16264 16260 0 Jun18 ? 00:01:33 nginx: worker process
8. nobody 16265 16260 0 Jun18 ? 00:01:32 nginx: worker process
9. nobody 16266 16260 0 Jun18 ? 00:01:24 nginx: worker process
10. nobody 16267 16260 0 Jun18 ? 00:01:32 nginx: worker process
11. nobody 16268 16260 0 Jun18 ? 00:01:23 nginx: worker process
12. nobody 16269 16260 0 Jun18 ? 00:01:32 nginx: worker process
13. nobody 16270 16260 0 Jun18 ? 00:01:26 nginx: worker process
14. nobody 16271 16260 0 Jun18 ? 00:01:32 nginx: worker process
15. nobody 16272 16260 0 Jun18 ? 00:01:25 nginx: worker process
16. nobody 16273 16260 0 Jun18 ? 00:01:26 nginx: worker process
17. nobody 16274 16260 0 Jun18 ? 00:01:32 nginx: worker process
18. nobody 16275 16260 0 Jun18 ? 00:01:32 nginx: worker process
19. nobody 16276 16260 0 Jun18 ? 00:01:33 nginx: worker process
20. nobody 16277 16260 0 Jun18 ? 00:01:24 nginx: worker process
21. nobody 16278 16260 0 Jun18 ? 00:01:24 nginx: worker process
22. nobody 16279 16260 0 Jun18 ? 00:01:30 nginx: worker process
23. nobody 16280 16260 0 Jun18 ? 00:01:24 nginx: worker process
24. nobody 16281 16260 0 Jun18 ? 00:01:32 nginx: worker process
25. nobody 16282 16260 0 Jun18 ? 00:01:32 nginx: worker process
26. nobody 16283 16260 0 Jun18 ? 00:01:25 nginx: worker process
27. nobody 16284 16260 0 Jun18 ? 00:01:26 nginx: worker process



# 配置文件

## Nginx反向代理实践

> 省过

## Nginx Rewrite重新定向

使用nginx做重新定向。 
nginx参考网址：http://blog.sina.com.cn/s/blog_97688f8e0100zws5.html

> 语法规则： **location [=|~|~*|^~] /uri/ { … }**

- = 开头表示精确匹配
- ^~ 开头表示uri以某个常规字符串开头，理解为匹配 url路径即可。nginx不对url做编码，因此请求为/static/20%/aa，可以被规则^~ /static/ /aa匹配到（注意是空格）。
- ~ 开头表示区分大小写的正则匹配
- ~* 开头表示不区分大小写的正则匹配
- !~和!~*分别为区分大小写不匹配及不区分大小写不匹配 的正则
- / 通用匹配，任何请求都会匹配到。

多个location配置的情况下匹配顺序为:

> 首先匹配 =，其次匹配^~, 其次是按文件中顺序的正则匹配，最后是交给 / 通用匹配。当有匹配成功时候，停止匹配，按当前匹配规则处理请求。

例子，有如下匹配规则：

> location = / {
>
> ​	规则A
>
> }

> location = /login {
>
> ​	规则B
>
> }

> location ^~ /static/ {
>
> ​	规则C
>
> }

> location ~ \.(gif|jpg|png|js|css)$ {
>
> ​	规则D
>
> }

> location ~* \.png$ {
>
> ​	规则E
>
> }

> location !~ \.xhtml$ {
>
> ​	规则F
>
> }

> location !~* \.xhtml$ {
>
> ​	规则G
>
> }

> location / {
>
> ​	规则H
>
> }

那么产生的效果如下：

- 访问根目录/， 比如http://localhost/ 将匹配规则A
- 访问 http://localhost/login 将匹配规则B，http://localhost/register 则匹配规则H
- 访问 http://localhost/static/a.html 将匹配规则C
- 访问 http://localhost/a.gif, http://localhost/b.jpg 将匹配规则D和规则E，但是规则D顺序优先，规则E不起作用，而 http://localhost/static/c.png 则优先匹配到规则C
- 访问 http://localhost/a.PNG 则匹配规则E，而不会匹配规则D，因为规则E不区分大小写。
- 访问 http://localhost/a.xhtml 不会匹配规则F和规则G，http://localhost/a.XHTML不会匹配规则G，因为不区分大小写。规则F，规则G属于排除法，符合匹配规则但是不会匹配到，所以想想看实际应用中哪里会用到。
- 访问 http://localhost/category/id/1111 则最终匹配到规则H，因为以上规则都不匹配，这个时候应该是nginx转发请求给后端应用服务器，比如FastCGI（php），tomcat（jsp），nginx作为方向代理服务器存在。



所以实际使用中，个人觉得至少有三个匹配规则定义，如下：

- 直接匹配网站根，通过域名访问网站首页比较频繁，使用这个会加速处理，官网如是说。

  这里是直接转发给后端应用服务器了，也可以是一个静态首页

- 第一个必选规则

> location = / {
> 	proxy_pass http://tomcat:8080/index
> }

- 第二个必选规则是处理静态文件请求，这是nginx作为http服务器的强项

  有两种配置模式，目录匹配或后缀匹配,任选其一或搭配使用

> location ^~ /static/ {
> 	root /webroot/static/;
> }

> location ~* \.(gif|jpg|jpeg|png|css|js|ico)$ {
> 	root /webroot/res/;
> }

- 第三个规则就是通用规则，用来转发动态请求到后端应用服务器

  非静态文件请求就默认是动态请求，自己根据实际把握

  毕竟目前的一些框架的流行，带.php,.jsp后缀的情况很少了

> location / {
> 	proxy_pass http://tomcat:8080/
> }

