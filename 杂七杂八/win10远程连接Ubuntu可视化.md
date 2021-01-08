# win10远程连接Ubuntu可视化

Xrdp 是一个微软远程桌面协议（RDP）的开源实现，它允许你通过图形界面控制远程系统。通过 RDP，你可以登录远程机器，并且创建一个真实的桌面会话，就像你登录本地机器一样。

这篇指南讲解如何在 Ubuntu 20.04 上安装和配置 Xrdp 服务器。

## 一、安装桌面环境

Ubuntu 服务器通常使用命令行进行管理，并且默认没有安装桌面环境。如果你正在运行 Ubuntu 桌面版，忽略这一步。

在 Ubuntu 源仓库有很多桌面环境供你选择。一个选择是安装 Gnome，它是 Ubuntu 20.04 的默认桌面环境。另外一个选项就是安装 xfce。它是快速，稳定，并且轻量的桌面环境，使得它成为远程服务器的理想桌面。

运行下面任何一个命令去安装你选择的桌面环境：

- 安装 Gnome

```
sudo apt update


sudo apt install ubuntu-desktop
```

取决于你的系统，下载和安装 GUI 软件包，将会花费一些时间。

## 二、安装 Xrdp

Xrdp 被包含在默认的 Ubuntu 软件源中。想要安装它，运行：

```
sudo apt install xrdp 
```

一旦安装完成，Xrdp 服务将会自动启动。你可以输入下面的命令，验证它：

```
sudo systemctl status xrdp
```

输出将会像下面这样：

```
● xrdp.service - xrdp daemon



     Loaded: loaded (/lib/systemd/system/xrdp.service; enabled; vendor preset: enabled)



     Active: active (running) since Fri 2020-05-22 17:36:16 UTC; 4min 41s ago



  ...
```

默认情况下，Xrdp 使用`/etc/ssl/private/ssl-cert-snakeoil.key`,它仅仅对“ssl-cert” 用户组成语可读。运行下面的命令，将`xrdp`用户添加到这个用户组：

```
sudo adduser xrdp ssl-cert  
```

重启 Xrdp 服务，使得修改生效：

```
sudo systemctl restart xrdp
```

就这样。Xrdp 已经在你的 Ubuntu 服务器上安装好了，你可以开始使用它了。

## 三、Xrdp 配置

Xrdp 配置文件定位在`/etc/xrdp`目录。对于基本的 Xrdp 链接，你不需要对配置文件做任何改动。

Xrdp 使用默认的 X Window 桌面环境（）Gnome or XFCE）。

主要的配置文件被命名为 [xrdp.ini](https://linux.die.net/man/5/xrdp.ini)。这个文件被分成不同的段，允许你设置全局配置，例如安全，监听地址，创建不同的 xrdp 登录会话等。

不管什么时候你对配置文件做出修改，你需要重启 Xrdp 服务。

Xrdp 使用`startwm.sh`文件启动 X 会话。如果你想使用另外一个 X Window 桌面，编辑这个文件。

## 四、配置防火墙

Xrdp 守护程序在所有的网络接口上监听端口`3389`。如果你在你的 Ubuntu 服务器上运行一个防火墙，你需要打开 Xrdp 端口。

想要允许从某一个指定的 IP 地址或者 IP 范围访问 Xrdp 服务器，例如`192.168.33.0/24`,你需要运行下面的命令：

```
sudo ufw allow from 192.168.33.0/24 to any port 3389
```

如果你想允许从任何地方访问（由于安全原因，这种方式不鼓励），运行：

```
sudo ufw allow 3389
```

想要增加安全，你可以考虑 Xrdp 仅仅监听 localhost，并且创建一个 SSH 隧道，将本地机器的`3389`端口到远程服务器的同样端口之间的流量加密。

## 五、连接 Xrdp 服务器

现在你已经设置好你的 Xrdp 服务器，是时候打开你的 Xrdp 客户端并且连接到服务器。

如果你有一台 Windows 电脑，你可以使用默认的 RDP 客户端。在 Windows  搜索栏输入“remote”，并且点击“Remote Desktop Connection”。这将会打开一个 RDP  客户端。在“Computer”区域输入远程服务器 IP地址，并且点击“Connect”。

[![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly93d3cuaXRjb2Rlci50ZWNoL2ltZy9saW51eGl6ZS91YnVudHUvcmRwLWNsaWVudC0xLmpwZw?x-oss-process=image/format,png)](https://www.aliyun.com/minisite/goods?userCode=dbgo15cy)

在登录屏幕，输入你的用户名和密码，点击“OK”。

[![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly93d3cuaXRjb2Rlci50ZWNoL2ltZy9saW51eGl6ZS91YnVudHUvcmRwLWxvZ2luLmpwZw?x-oss-process=image/format,png)](https://www.aliyun.com/minisite/goods?userCode=dbgo15cy)

一旦登录，你将看到默认的 Gnome 或者 Xfce 桌面，它应该像下面这样：

[![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly93d3cuaXRjb2Rlci50ZWNoL2ltZy9saW51eGl6ZS91YnVudHUveHJkcC1nbm9tZS1kZXNrdG9wLmpwZw?x-oss-process=image/format,png)](https://www.aliyun.com/minisite/goods?userCode=dbgo15cy)

现在你可以从你的本地机器上使用你的键盘和鼠标和远程桌面进行交互了。

如果你正在运行 macOS,你可以从Mac App Store安装 Microsoft Remote Desktop应用。 Linux 用户可以使用一个 RDP 客户端，例如 Remmina 或者 Vinagre。

## 六、总结

配置一个远程桌面，允许你从你的本地机器通过一个简单易用的图形界面来管理你的 Ubuntu 20.04 服务器。