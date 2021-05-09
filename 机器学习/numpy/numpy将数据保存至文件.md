# `numpy`将数据保存至文件



## 引言

由于数据挖掘作业需要进行聚类分析，便产生生成随机数据方便联系的想法，保存至文件更便于读取。



## 实现

```python
import numpy as np

points = np.random.randn(1000,2)	# 产生一千组随机点坐标 相当于[1000,2]维矩阵

np.savetxt("./random_points.txt", points, fmt='%f',delimiter='\t')
'''
arg0:filename
arg1:input_data
arg2:format，这里我选择浮点形式，你也可以使用np.float32
arg3:分隔符
'''
```

