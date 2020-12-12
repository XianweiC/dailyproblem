# python将字符串转化成列表

## 1.字符串转化成列表

```python
str = 'tomorrow'
list(str)
#如果直接这样，会分割成单个字符
['t','o','m','o','r','r','o','w']

str.split('这里传入任何字符串没有的分割单位都可以，但是不能为空')
['tomorrow']
```

