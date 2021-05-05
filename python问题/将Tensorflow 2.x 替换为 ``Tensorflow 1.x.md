# 将`Tensorflow 2.x` 替换为 ```Tensorflow` 1.x



```python
import tensorflow.compat.v1 as tf
tf.compat.v1.disable_eager_execution()
或
import tensorflow.compat.v1 as tf
tf.disable_v2_behavior()

替换import tensorflow as tf
```

