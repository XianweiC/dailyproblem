# Linux强制用户下线

起因在于使用小组服务器时，经常忘记正常`exit`退出，导致出现重复用户

```bash
who # 查看当前登陆用户
---
a@a-MS-7C06:~$ who
a        pts/0        2022-07-09 00:35 (10.193.180.253)
a        pts/1        2022-07-11 12:36 (10.175.103.219)
a        pts/3        2022-07-11 16:26 (10.175.226.219)
```

使用命令

```shell
pkill [-SIGNAL] [-u 用户名] [-t 虚拟终端名] 
```

例如：

```
pkill -kill -t pts/3
```

