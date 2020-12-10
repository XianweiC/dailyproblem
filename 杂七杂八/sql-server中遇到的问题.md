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

