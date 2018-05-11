- 首先打开站长工具，测试一下最优的DNS

  [打开Dns检测|Dns查询 - 站长工具](http://tool.chinaz.com/dns?type=1&host=github.com&ip=)

  监测结果类似如下：

  ![](https://ws2.sinaimg.cn/large/006tNc79ly1fr4crv9gy3j31a412mk1z.jpg)

  发现这个访问速度很快

- 编辑host文件

  - `sudo vim /etc/hosts` 然后在最后一行加入：

    ![](https://ws3.sinaimg.cn/large/006tNc79ly1fr4cu4nsnaj30o00e6gqp.jpg)