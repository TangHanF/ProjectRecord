## Nginx 安装

系统平台：`CentOS release 6.6 (Final)` 64位。

### 一、安装编译工具及库文件

```
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
```

### 二、首先要安装 PCRE

PCRE 作用是让 Nginx 支持 Rewrite 功能。

1、下载 PCRE 安装包，下载地址： <http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz>

```
[root@bogon src]# wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
```

2、解压安装包:

```
[root@bogon src]# tar zxvf pcre-8.35.tar.gz
```

3、进入安装包目录

```
[root@bogon src]# cd pcre-8.35
```

4、编译安装 

```
[root@bogon pcre-8.35]# ./configure
[root@bogon pcre-8.35]# make && make install
```

5、查看pcre版本

```
[root@bogon pcre-8.35]# pcre-config --version
```

### 安装 Nginx

1、下载 Nginx，下载地址：<http://nginx.org/download/nginx-1.6.2.tar.gz>

```
[root@bogon src]# wget http://nginx.org/download/nginx-1.6.2.tar.gz
```

![img](https://ws3.sinaimg.cn/large/006tNbRwly1fwphcb11lsj30li025glk.jpg)2、解压安装包

```
[root@bogon src]# tar zxvf nginx-1.6.2.tar.gz
```

3、进入安装包目录

```
[root@bogon src]# cd nginx-1.6.2
```

4、编译安装

```
[root@bogon nginx-1.6.2]# ./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
[root@bogon nginx-1.6.2]# make
[root@bogon nginx-1.6.2]# make install
```

5、查看nginx版本

```
[root@bogon nginx-1.6.2]# /usr/local/webserver/nginx/sbin/nginx -v
```

到此，nginx安装完成。

------

## Nginx 配置

创建 Nginx 运行使用的用户 www：

```
[root@bogon conf]# /usr/sbin/groupadd www 
[root@bogon conf]# /usr/sbin/useradd -g www www
```

配置nginx.conf ，将/usr/local/webserver/nginx/conf/nginx.conf替换为以下内容

```properties
[root@bogon conf]#  cat /usr/local/webserver/nginx/conf/nginx.conf

user www www;
worker_processes 2; #设置值和CPU核心数一致
error_log /usr/local/webserver/nginx/logs/nginx_error.log crit; #日志位置和日志级别
pid /usr/local/webserver/nginx/nginx.pid;
#Specifies the value for maximum file descriptors that can be opened by this process.
worker_rlimit_nofile 65535;
events
{
  use epoll;
  worker_connections 65535;
}
http
{
  include mime.types;
  default_type application/octet-stream;
  log_format main  '$remote_addr - $remote_user [$time_local] "$request" '
               '$status $body_bytes_sent "$http_referer" '
               '"$http_user_agent" $http_x_forwarded_for';
  
#charset gb2312;
     
  server_names_hash_bucket_size 128;
  client_header_buffer_size 32k;
  large_client_header_buffers 4 32k;
  client_max_body_size 8m;
     
  sendfile on;
  tcp_nopush on;
  keepalive_timeout 60;
  tcp_nodelay on;
  fastcgi_connect_timeout 300;
  fastcgi_send_timeout 300;
  fastcgi_read_timeout 300;
  fastcgi_buffer_size 64k;
  fastcgi_buffers 4 64k;
  fastcgi_busy_buffers_size 128k;
  fastcgi_temp_file_write_size 128k;
  gzip on; 
  gzip_min_length 1k;
  gzip_buffers 4 16k;
  gzip_http_version 1.0;
  gzip_comp_level 2;
  gzip_types text/plain application/x-javascript text/css application/xml;
  gzip_vary on;
 
  #limit_zone crawler $binary_remote_addr 10m;
 #下面是server虚拟主机的配置
 server
  {
    listen 80;#监听端口
    server_name localhost;#域名
    index index.html index.htm index.php;
    root /usr/local/webserver/nginx/html;#站点目录
      location ~ .*\.(php|php5)?$
    {
      #fastcgi_pass unix:/tmp/php-cgi.sock;
      fastcgi_pass 127.0.0.1:9000;
      fastcgi_index index.php;
      include fastcgi.conf;
    }
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|ico)$
    {
      expires 30d;
  # access_log off;
    }
    location ~ .*\.(js|css)?$
    {
      expires 15d;
   # access_log off;
    }
    access_log off;
  }

}
```

检查配置文件ngnix.conf的正确性命令：

```
[root@bogon conf]# /usr/local/webserver/nginx/sbin/nginx -t
```

------

## 启动 Nginx

Nginx 启动命令如下：

```
[root@bogon conf]# /usr/local/webserver/nginx/sbin/nginx
```

------

## 访问站点

从浏览器访问我们配置的站点ip：

------

## Nginx 其他命令

以下包含了 Nginx 常用的几个命令：

```
/usr/local/webserver/nginx/sbin/nginx -s reload            # 重新载入配置文件
/usr/local/webserver/nginx/sbin/nginx -s reopen            # 重启 Nginx
/usr/local/webserver/nginx/sbin/nginx -s stop              # 停止 Nginx
```







参考：


https://www.jianshu.com/p/d5114a2a2052

https://blog.csdn.net/mulangren1988/article/details/59104415

http://www.runoob.com/linux/nginx-install-setup.html

https://www.zhihu.com/question/20092756

https://blog.csdn.net/finded/article/details/51889588

- [CentOS 7 下安装 Nginx](https://www.linuxidc.com/Linux/2016-09/134907.htm)












-------

zlib：

wget http://www.zlib.net/zlib-1.2.11.tar.gz

首先安装必要的库（nginx 中gzip模块需要 zlib 库，rewrite模块需要 pcre 库，ssl 功能需要openssl库）。选定**/usr/local**为安装目录，以下具体版本号根据实际改变。

1.安装PCRE库

```
$ cd /usr/local/
$ sudo wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.36.tar.gz
$ sudo tar -zxvf pcre-8.36.tar.gz
$ cd pcre-8.36
$ sudo ./configure
$ sudo make
$ sudo make install
```

2.安装zlib库

```
$ cd /usr/local/ 
$ sudo wget http://zlib.net/zlib-1.2.8.tar.gz
$ sudo tar -zxvf zlib-1.2.8.tar.gz
$ cd zlib-1.2.8
$ sudo ./configure
$ sudo make
$ sudo make install
```

3.安装ssl

```
$ cd /usr/local/
$ sudo wget http://www.openssl.org/source/openssl-1.0.1j.tar.gz
$ sudo tar -zxvf openssl-1.0.1j.tar.gz
$ sudo ./config
$ sudo make
$ sudo make install
```

4.安装nginx

```
$ cd /usr/local/
$ sudo wget http://nginx.org/download/nginx-1.8.0.tar.gz
$ sudo tar -zxvf nginx-1.8.0.tar.gz
$ cd nginx-1.8.0  
$ sudo ./configure --prefix=/usr/local/nginx  #这一步需要按需要添加编译参数，如下
$ sudo make
$ sudo make install
```

如果是使用安装包编译的上面几个依赖，需要在在--prefix后面接以下命令:

```
--with-pcre=/usr/local/pcre-8.36 指的是pcre-8.36 的源码路径。
--with-zlib=/usr/local/zlib-1.2.8 指的是zlib-1.2.8 的源码路径。
```