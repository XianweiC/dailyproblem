# 关于配置python镜像源问题

```
http://quotes.toscrape.com/

# pip从依赖文件中批量安装

pip freeze > <filename>

pip install -r <filename>

镜像文件
pip3 install <name> -i https://pypi.tuna.tsinghua.edu.cn/simple
```



```
torch安装问题

 pip install torch==1.6.0 -f https://download.pytorch.org/whl/torch_stable.html
```



```
Timed Out
pip --default-timeout=100 install 包名

pip的镜像源是国外时，经常遇到‘time out’，我们只需要把源地址改为国内可用的镜像网站就可以避免这个问题。

pip install --index https://pypi.python.org/simple softwarename

如果在国内镜像网站搜索不到该软件或者包，可以换个镜像网站重新下载。

下面为部分国内可用的镜像网站：

Python官方：https://pypi.python.org/simple

v2ex：http://pypi.v2ex.com/simple

阿里云：https://mirrors.aliyun.com/pypi/simple

清华大学：https://pypi.tuna.tsinghua.edu.cn/simple

中国科技大学：https://pypi.mirrors.ustc.edu.cn/simple

中国科学院：http://pypi.mirrors.opencas.cn/simple

douban：http://pypi.douban.com/simple
```





```shell
pip install <package> -i <url>
```

如果我们需要修改pip的配置文件永久地更改pip的镜像源。
 pip的配置文件在linux系统中为：

```shell
~/.pip/pip.conf
```

在windows系统中为：

```shell
C:\Users\{YourNanme}\AppData\Roaming\pip\pip.ini
```

若上述配置文件不存在，则手动创建。
 也可通过下面的命令查看配置文件位置：

```shell
pip -v config list
```

找到pip的配置文件后，以阿里云镜像为例，修改文件内容为：

```shell
[global]
index-url=http://mirrors.aliyun.com/pypi/simple/
trusted-host=mirrors.aliyun.com
```

保存配置文件，则完成了对pip默认镜像源的更换。
