# 服务器安装Ubuntu黑屏

**引言：为了寒假能够使用服务器远程开发，现存的16.04过于老旧，因此采用安装20.10版本，在安装完成提示重启后，重新启动却一直黑屏**

## 解决方法：

开机grub界面按`e`键，`linux`打头的行，`quiet`后添加`nomodeset`。
 F10保存并启动，

进入recovery mode来

## 注意

上述方法是临时起作用。

编辑`/etc/default/grub`中进行修改，则还需要`sudo update-grub`。这样操作后，重启后就一直使用nomodeset参数了。

## 成功开机后，配置ssh远程连接

```bash
sudo apt install openssh-server

sudo apt install ufw
#安装防火墙管理
sudo ufw enable
sudo ufw allow 22
#允许通过22端口连接
sudo systemctl enable ssh
#允许ssh自启动
```

