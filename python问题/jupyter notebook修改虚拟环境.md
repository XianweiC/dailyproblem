# `jupyter notebook`修改虚拟环境

## 引言：

在进行深度学习过程中，需要经常切换环境，虽然在命令行可以使用`conda activate env-name`来激活环境，但是却不知从哪里修改`jupyter-notebook`的内核。下面进行整理。



## 步骤

### 1.进入命令行,激活目标环境

```bash
conda activate env-name
```

### 2.安装`ipykernel`

```
conda install ipykernel
```

### 3.添加环境

```
python -m ipykernel install --user（非服务器可缺省） --name 环境名称
```

### 4.重新打开notebook

```
>jupyternote book
选择服务-->改变服务，即可发现成功添加
```

