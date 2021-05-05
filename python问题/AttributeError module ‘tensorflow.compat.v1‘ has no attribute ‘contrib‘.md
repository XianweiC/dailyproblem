# AttributeError: module ‘tensorflow.compat.v1‘ has no attribute ‘contrib‘



## 原代码：



```python
initializer = tf.contrib.layers.xavier_initializer()
```



报错原因是，tf2中删除了contrib这个库，因此无法使用xavier_initializer()初始化。但是提供了相同功能的函数：
glorot uniform initializer(),两者的初始化方式是相同的。因此使用如下代码，即可解决上述问题。

```python
initializer=tf.glorot_uniform_initializer()
```

