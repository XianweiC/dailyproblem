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
```