# Mac磁盘格式类型



# 分区推荐

![](https://ws1.sinaimg.cn/large/006tNc79ly1fr8okvop9mj319e0p2gpg.jpg)

FAT32可以同时使用，但是单个文件不能超过4G；

**推荐**

- ExFAT 格式用在Win上
- MacOS用在Mac上

> 因为Mac的TimeMachine需要使用`Mac OS 扩展（日志式）`所以不能把整个硬盘都分成FAT32。

基于以上需求，我把硬盘分了3个区：Mac（MacOS）、Win（ExFAT）、Time Machine（MacOS 日志式备份专用）

Mac上都可以读取，Win上可以读取Win的区