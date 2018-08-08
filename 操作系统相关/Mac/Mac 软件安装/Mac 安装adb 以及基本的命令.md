# Mac 安装adb 以及基本的命令

- 安装adb
- adb命令

------

## adb 安装

> - 安装brew
>
> > ruby -e “$(curl –insecure -fsSL <https://raw.githubusercontent.com/Homebrew/install/master/install>)”.
>
> - 安装adb
>
> > brew install Caskroom/cask/android-platform-tools
>
> - 测试adb 是否安装成功: 
>
> > adb devices 
>
> - 通过 WLAN 连接到设备
>
> > 设置端口号： 
> > Adb tcpip 5555 
> > 连接IP/端口号可有可无: 
> > Adb connect 172.168.9.13:5555 
> > 查看设备: 
> > Adb devices 
> > 结束进程,重启服务，重新来一遍: 
> > Adb kill-server/start-server 

IP 为手机端IP地址，在PC端和手机端同时连接同一网络的前提下，获取手机端的IP地址进行连接。网络是一定的可翻墙网络！

### 其他命令

操作手机数据命令：

| 命令                  | 作用                                                         |
| --------------------- | ------------------------------------------------------------ |
| adb pull remote local | 要从模拟器或设备复制文件或目录（及其子目录）                 |
| adb push local remote | 要将文件文件或目录（及其子目录）复制到模拟器或设备           |
| install path_to_apk   | 将 Android 应用（使用 APK 文件的完整路径表示）推送到模拟器/设备 |
| forward local remote  | 将来自指定本地端口的套接字连接转发到模拟器/设备实例上的指定远程端口。 |
| shell                 | 在目标模拟器/设备实例中启动远程 shell。                      |
| shell shell_command   | 在目标模拟器/设备实例中启动远程 shell。                      |

在上述命令中，local 和 remote 指的是开发计算机（本地）和模拟器/设备实例（远程）上目标文件/目录的路径。例如：

> adb push foo.txt /sdcard/foo.txt