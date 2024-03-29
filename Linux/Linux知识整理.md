# Linux知识整理

## 文件系统

目录

```
# 安装位置
/usr/bin
/usr/loacl/bin

# 图标
/usr/local/applications/xxx.desktop
```

## 命令

### df 命令

显示磁盘空间使用情况。获取硬盘被占用了多少空间，目前还剩下多少空间等信息，如果没有文件名被指定，则所有当前被挂载的文件系统的可用空间将被显示。默认情况下，磁盘空间将以 1KB 为单位进行显示，除非环境变量 POSIXLY_CORRECT 被指定，那样将以512字节为单位进行显示：

```shell
-a 全部文件系统列表
-h 以方便阅读的方式显示信息
-i 显示inode信息
-k 区块为1024字节
-l 只显示本地磁盘
-T 列出文件系统类型
```

### ps 命令

ps(process status)，用来查看当前运行的进程状态



## `ln`链接

建立软链接（相当于快捷方式）

```shell
ln -s 'target_file' 'tagert_location'
```



## `unzip`解压

```shell
unzip -O 编码格式(CP936/GBK/GB18030) xxx.zip -d /xxx/xxx
```
