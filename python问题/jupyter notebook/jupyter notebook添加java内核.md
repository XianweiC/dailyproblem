# jupyter notebook添加java内核



# 1. 配置Java9以上版本的Java环境

# 2. 下载 java 内核压缩包ijava

下载地址:https://github.com/SpencerPark/IJava/releases![下载 java 内核压缩包ijavaijava](https://img-blog.csdnimg.cn/20200621163140573.png)

# 3. 解压下载的压缩包到自己的文件夹

解压后得到一个 install.py 的文件，和一个 java 文件夹
 ![ijava](https://img-blog.csdnimg.cn/20200622231815666.png)

# 4. 安装Java内核

用cmd定位到第3步解压后的文件夹中，执行以下命令安装：

```
python install.py --sys-prefix
1
```

![安装Java内核](https://img-blog.csdnimg.cn/20200622232127341.png)

# 5. 查看Jupyter对Java的支持是否添加成功

在cmd中执行以下命令：

```
jupyter kernelspec list
1
```

![查看Jupyter对Java的支持是否添加成功](https://img-blog.csdnimg.cn/20200621164054934.png)

## Jupyter notebook运行Java

![Jupyter notebook运行Java](https://img-blog.csdnimg.cn/20200621171209765.png)		