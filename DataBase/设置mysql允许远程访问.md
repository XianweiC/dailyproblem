# 设置mysql允许远程访问

## 引言：

在通过DataGrip访问服务器数据库时，在账号密码都正确的情况下，被拒绝连接，原来是未在数据库设置访问权限。

-----

## 方法：

设置mysql允许远程访问
1.登陆mysql数据库，修改表。
use mysql;
update user set host='%' where user='root';
select host,user from user;
flush privileges; 

注意：最后一句很重要，目的是使修改生效，如果没有写，则还是不能进行远程连接。

2.授权用户，允许从任何主机连接到mysql数据库。
grant all privileges on \*.* to 'root'@'%' identified by 'pwd' with grant option;
flush privileges;

如果只是允许用户从ip为192.168.1.104的主机连接到mysql服务器。
grant all privileges on *.* to 'root'@'%192.168.1.104' identified by 'ip'@''#' with grant option;
flush privileges;