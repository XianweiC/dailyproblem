# conda相关操作

## conda创建虚拟环境

```bash
xianwei@ThinkPad-E580:~
➤ conda env list                                                         (base)
#查看环境列表
# conda environments:
#
base                  *  /home/xianwei/miniconda3
tensorflow               /home/xianwei/miniconda3/envs/tensorflow
zhrtvc                   /home/xianwei/miniconda3/envs/zhrtvc
--------------------------------------------------------------

conda create -n 'envname' python='指定的python版本号'
#创建虚拟环境

conda remove -n 'envname' --all
#删除该环境

conda active 'envname'
#进入环境

#如果想要修改环境的python版本
conda install python=<version>
#例如：
conda install python=3.5

# 更新conda版本
conda update -n base -c defaults conda
```

## 更改镜像源

添加国内源：

```bash
#清华源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main

conda config --set show_channel_urls yes

运行 conda clean -i 清除索引缓存，保证用的是镜像站提供的索引。
```

换回默认源：

```
conda config --remove-key channels
```

在执行conda config 命令的时候

会在当前用户目录下创建 .condarc 文件，可以查看更换源前后该文件内容的变化。