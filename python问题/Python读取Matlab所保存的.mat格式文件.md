# Python读取Matlab所保存的.mat格式文件

读取Mathlab所保存的文件

```
#coding:UTF-8
```

```python
import scipy.io as scio

file_path = 'your_file_path'
data = scio.loadmat(file_path)
```