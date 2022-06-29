# Ubuntu  NVIDIA驱动安装总结             

学校服务器显卡型号：tesla k40c,在使用第二种方法安装后，成功开机

在Ubuntu 上安装NVIDIA有三种方法：

- 使用标准Ubuntu仓库进行自动化安装
- 使用PPA仓库进行自动化安装
- 使用官方的NVIDIA驱动进行手动安装

上述三种方法均可用，我个人更习惯于使用手动安装。

注意：

在安装之前首先就是要禁用Nouveau的驱动，禁用该驱动的方法参照[这篇博客](https://blog.csdn.net/tjuyanming/article/details/79267984)。

上一步的改动只是在安装的时候临时禁用。如果没有永久禁用该驱动，可能会出现安装完毕NIVIDA显卡后无法进入Ubuntu的情况(在登录界面，输入密码也无法登录)。

所以，在安装后Ubuntu成功后需要在grub的配置文件里面更改：

```shell
$ sudo gedit /boot/grub/grub.cfg 
1
```

在文本中搜索`quiet splash` 然后添加`acpi_osi=linux nomodeset`，保存文本即可。

#### 1. 使用标准Ubuntu 仓库进行自动化安装

这种方法几乎是所有的示例中最简单的方法，也是该教程最为推荐的方法。首先，检测你的NVIDIA显卡型号和推荐的驱动程序的模型。在命令行中输入如下命令：

```shell
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001180sv00001458sd0000353Cbc03sc00i00
vendor   : NVIDIA Corporation
model    : GK104 [GeForce GTX 680]
driver   : nvidia-304 - distro non-free
driver   : nvidia-340 - distro non-free
driver   : nvidia-384 - distro non-free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin
 
== cpu-microcode.py ==
driver   : intel-microcode - distro free
123456789101112
```

从输出结果可以看到，目前系统已连接Nvidia GeFrand GTX 680显卡，建议安装驱动程序是 nvidia-384版本的驱动。如果您同意该建议，请再次使用Ubuntu驱动程序命令来安装所有推荐的驱动程序。

输入以下命令：

```shell
$ sudo ubuntu-drivers autoinstall
1
```

一旦安装结束，重新启动系统，你就完成了。

#### 2. 使用PPA仓库进行自动安装

使用图形驱动程序PPA存储库允许我们安装NVIDIA beta驱动程序，但是这种方法存在不稳定的风险。
 首先，将`ppa:graphics-drivers/ppa`存储库添加到系统中：

```shell
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
12
```

接下来，识别显卡模型和推荐的驱动程序：

```shell
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001180sv00001458sd0000353Cbc03sc00i00
vendor   : NVIDIA Corporation
model    : GK104 [GeForce GTX 680]
driver   : nvidia-340 - third-party free
driver   : nvidia-390 - third-party free recommended
driver   : nvidia-387 - third-party free
driver   : nvidia-304 - distro non-free
driver   : nvidia-384 - third-party free
driver   : xserver-xorg-video-nouveau - distro free builtin

== cpu-microcode.py ==
driver   : intel-microcode - distro free
1234567891011121314
```

输入以下命令：

```shell
$ sudo apt install nvidia-390
1
```

一旦完成，即可重新启动系统。

\####3.使用官方的NVIDIA驱动进行手动安装

这种方式也是我最常用的方式，安装方式如下。

首先识别NVIDIA显卡型号，输入一下命令：

```
$  lshw -numeric -C display
1
```

或者

```
$ lspci -vnn | grep VGA
1
```

下载[NVIDIA官方](https://www.nvidia.com/Download/index.aspx)显卡驱动，然后存储到相应路径。

停止可视化桌面：

```shell
$ sudo telinit 3		
1
```

之后会进入一个新的命令行会话，使用当前的用户名密码登录

在相应路径下安装NVIDIA驱动(安装文件也可为.sh后缀，如果提示没有权限使用`sudo`)：

```
$ bash NVIDIA-Linux-x86_64-384.111.bin
1
```

按照以下步骤：

> Accept License
>  The distribution-provided pre-install script failed! Are you sure you want to continue? -> CONTINUE INSTALLATION
>  Would you like to run the nvidia-xconfig utility? -> YES

在安装结束后，在命令行输入一下命令重启，NVIDIA驱动即可安装成功：

```shell
$ sudo reboot
```