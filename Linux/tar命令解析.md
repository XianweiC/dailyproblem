# tar命令解析

首先在Linux上区分两个概念：打包和压缩。

之所以会有这样的区分，在于Linux上的许多压缩工具只能将一个整体的文件进行压缩，所以我们在进行压缩之前需要将多份文件进行打包，成为一个整体，而`tar`命令则将打包、压缩集成为一体



首先要弄清两个概念：打包和压缩。打包是指将一大堆文件或目录变成一个总的文件；压缩则是将一个大的文件通过一些压缩算法变成一个小文件。

为什么要区分这两个概念呢？这源于Linux中很多压缩程序只能针对一个文件进行压缩，这样当你想要压缩一大堆文件时，你得先将这一大堆文件先打成一个包（tar命令），然后再用压缩程序进行压缩（gzip bzip2命令）

## 常用参数

```bash
tar
	-c,--create #创建一个归档
	-r,--append #追加文件至归档末尾
	-t,--list #列出归档内容
	-x,--extract,--get #从归档中解出文件
	-f # 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名
	
	
	-j,--bzip2 #通过bzip2过滤归档
	-J，--xz #通过xz过滤归档
	-z,--gzip #通过gzip过滤归档
	
	-v,--verbose #详细列出处理文件
	-u,--update #仅追加比归档中副本更新的文件
```

## 举例

```bash
tar -cf my.tar a.txt b.txt
#将a.txt和b.txt进行打包至my.tar

tar -rf my.tar c.txt
#向my.tar中添加文件c.txt

tar -uf my.tar a.txt
#将my.tar中的a.txt进行替换更新

tar -tf my.tar
# 列出my.tar中所有文件

tar -xf my.tar
# 提取my.tar中的文件

-----------------------------------
# 压缩/解压缩

tar -zcvf [压缩包名称].tar.gz [待压缩文件]
#以gzip算法压缩

tar -zxvf [压缩包名称].tar.gz
#以gzip算法解压

tar -jcvf [压缩包名称].tar.bz2 [待压缩文件]
#以bzip2算法进行压缩


```



## make编译示例

```
1.解压tar.gz包
tar -zxvf xxx.tar.gz
cd xxx
2.编译前的配置修改
./configure --prefix=/usr/local
（生成configure配置脚本make configure）
3.编译
make
4.安装
make install
5.清理安装时生成的文件
make clean
```

