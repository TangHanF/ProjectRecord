###### Mac移动硬盘分区无法装载



1、首先输入命令： `diskutil list`

查看你的硬盘装载的名字（如下）

> /dev/disk0
>
>    TYPE NAME                    SIZE       IDENTIFIER
>
>    0:      GUID_partition_scheme                        *250.1 GB   disk0
>
>    1:                        EFI EFI                     209.7 MB   disk0s1
>
>    2:                  Apple_HFS ssd                     249.1 GB   disk0s2
>
>    3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
>
> /dev/disk1
>
> ​                     TYPE NAME                    SIZE       IDENTIFIER
>
>    0:      GUID_partition_scheme                        *320.1 GB   disk1
>
>    1:                        EFI EFI                     209.7 MB   disk1s1
>
>    2:                  Apple_HFS Macintosh HD            319.2 GB   disk1s2
>
>    3:                 Apple_Boot Recovery HD             650.0 MB   disk1s3
>
> /dev/disk2
>
> ​                       TYPE NAME                    SIZE       IDENTIFIER
>
>    0:     FDisk_partition_scheme                        *2.0 TB     disk2
>
>    1:                  Apple_HFS MAC                     666.9 GB   disk2s1
>
>    2:               Windows_NTFS MAC-WINDOWS             666.9 GB   disk2s2
>
>    3:               Windows_NTFS WINDOWS                 666.5 GB   disk2s3
>
>  

2、通过命令装载分区

1. `sudo diskutil mount /dev/disk3s1`

或者：

mkdir /Volume/partition1

sudo mount /dev/disk3s1 exfat /Volume/partition1

（假设你的分区是exfat格式）

----------

 

实在不不行，参考一下方法：

1. `fsck -fy`

经过一番搜索，在链接“<http://osxdaily.com/2013/08/07/how-to-repair-a-mac-disk-with-fsck-from-single-user-mode/>”帮助下，我可以用Cmd+S单用户登录系统，并且使用“fsck -fy”检查硬盘分区。但怎么检查我移动硬盘的分区呢？并且分区格式怎么判断？

2. `fsck_hfs -fy /dev/disk2s2`

在链接“<http://hints.macworld.com/article.php?story=20030714194313542>”和“<http://superuser.com/questions/503759/how-to-run-fsck-on-an-external-drive-with-os-x>”帮助下，我进入单用户模式（其实是命令行模式），知道我的移动硬盘是挂载到/dev下的disk2，每个分区是以s1，s2，s3来区分。我分区是hfs，我用mount -t hfs来加载没成功，但直接用fsck_hfs成功了。所以最后一个链接挺有用，知道命令，知道分区格式，知道分区，那么就能顺利进行修复了。修复完毕后，系统提示说A分区没啥问题，我基本放心了。

重启到正常模式下，插上移动硬盘，可以进行Time Machine备份，彻底搞定。

 