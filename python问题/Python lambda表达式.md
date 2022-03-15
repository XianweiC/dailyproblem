# Python: lambda表达式

python中的lambda表达式相当于一个匿名函数，不同于常规函数的地方在于，它仅有一个返回值



语法：

```
lambda <形参1, 形参2, ...>: (操作)(实参1, 实参2)
```



例如：

```python
def func1(a, b):
	return a + b

print(func1(1, 3))
print((lambda a,b: a+b)(1, 2))
```

结果：

```python
4
3
```

