# `dpkg`使用详解

普通安装`.deb`

```shell
sudo dpkg -i xxx.deb
```

设置安装位置

```shell
sudo dpkg -i xxx.deb --instdir xxx/xxx/xxx
```

查看软件安装状态

```shell
sudo dpkg -l sofrware_name
```

删除安装残留

```shell
sudo dpkg -r software_name
```

强制清除残留

```
sudo dpkg --remove --force-remove-reinstreq  software_name
```

