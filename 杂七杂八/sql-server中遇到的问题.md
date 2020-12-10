# mssql-server中遇到的问题

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

