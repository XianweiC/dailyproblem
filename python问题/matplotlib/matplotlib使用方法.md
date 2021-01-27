# `matplotlib`使用方法



```python
import matplotlib.pyplot as plt

# 声明一个画布
plt.figure()
# 单个图片大小
plt.figure(figsize=(10,10))

# 读取一张图片
plt.imshow(filename)
# 使图片以灰度显示
plt.imshow(filename,cmap=plt.cm.binary)

#显示色彩条
plt.colorbar()

#显示网格
plt.grid()

# x方向标签名称
plt.xlabel(label_name)
# y方向标签名称
plt.ylabel(label_name)

# 显示图像
plt.show()

# 清除画布
plt.clf()
```

```python
# 定义画布显示的布局
plt.subplot(a,b,c)
'''a行b列，c为该张图片在整张画布中的位置'''
# 例如
plt.figure()
p1 = plt.subplot(2,1,label='name1')
p2 = plt.subplot(2,1,2,label='name2')

p1.set_title('title1')
```

