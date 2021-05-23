# Ubuntu 设置 snap代理



修改文件 `/etc/environment`,该文件实际上是一个shell脚本，snapd商店通过读取该文件来获取代理信息

在文件中添加：

```shell
http_proxy=http://[服务器地址]:[端口号]
https_proxy=http://[服务器地址]:[端口号]
```

然后重启snap

```bash
sudo systemctl restart snapd
```

