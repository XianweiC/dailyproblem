# Ubuntu安装软件位置修改

安装包：xxx.deb



```shell
dpkg -i --instdir=/media/xianwei/D:/usr/bin xxx.deb
#安装位置在/media/D:/usr/bin

cd /media/D:/usr/bin

#创建软连接
sudo ln -s  /media/xianwei/D:/usr/bin/xxx /usr/local/bin/xxx
#删除软链接 sudo unlink /usr/local/bin/xxx

#图表等
sudo ln -s /media/xianwei/D:/usr/share/applications/xxx.desktop /usr/local/share/applications/xxx.desktop
```

