​		 		

# python中list切片详解		

语法：`[start:stop:step]`

step代表切片步长；切片区间为[start，stop)，包含start但不包含stop

1.step > 0，从左往右切片

2.step <0，从右往左切片

3.start、stop、step 为空值时的理解：

start、stop默认为列表的头和尾，并且根据step的正负进行颠倒；step的默认值为1

4.start、stop为负，无论step正负，start、stop代表的是列表从左到右的倒数第几个元素

```python
st = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
print(st[2:6:2])
print(st[6:2:-2])
print(st[::1])
print(st[::-1])  # 倒序输出
print(st[-1])


输出结果：
['c', 'e']
['g', 'e']
['a', 'b', 'c', 'd', 'e', 'f', 'g']
['g', 'f', 'e', 'd', 'c', 'b', 'a']
g
```