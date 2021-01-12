# mssql-server中遇到的问题

## mssql-server登录

```
sqlcmd -S localhost -U SA
```

## 1.如果遇到服务未启动

```
netstat -a | grep 1433
查看端口状态

status mssql-server --no-pages//查看服务启动状态

```

## 2.启动mssql-server服务

```
systemctl start mssql-server 
```

## 3.关闭mssql-server服务

```
systemctl stop mssql-server
```

## 4.重启

```
systemctl restart mssql-server
```

## 5.重新安装以重置密码

```
sudo /opt/mssql/bin/mssql-conf setup
此时按照安装步骤，重新设置SA密码即可
```

## 6.修改密码

```
1、登陆服务器，停用sqlserver服务，（命令：sudo systemctl stop mssql-server）
2、切换到/opt/mssql/bin/目录下面（命令：cd /opt/mssql/bin）
3、使用命令查看（命令./mssql-conf -h)
4、使用命令set-sa-password重置密码（命令./mssql-conf set-sa-password)
5、输入两遍密码，确认。
6、重启sqlserver服务（命令：sudo systemctl start mssql-server）
```

