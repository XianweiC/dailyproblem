# numpy.dot()的使用

dot()返回的是两个数组的点积(dot product)

1.如果处理的是一维数组，则得到的是两数组的內积

```python
In : d = np.arange(0,9)
Out: array([0, 1, 2, 3, 4, 5, 6, 7, 8])
In : e = d[::-1]
Out: array([8, 7, 6, 5, 4, 3, 2, 1, 0])

In : np.dot(d,e) 
Out: 84
1234567
```

2.如果是二维数组（矩阵）之间的运算，则得到的是矩阵积（mastrix product）。

```python
In : a = np.arange(1,5).reshape(2,2)
Out:
array([[1, 2],
       [3, 4]])

In : b = np.arange(5,9).reshape(2,2)
Out: array([[5, 6],
            [7, 8]])

In : np.dot(a,b)
Out:
array([[19, 22],
       [43, 50]])
```