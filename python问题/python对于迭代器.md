# python对于迭代器



例如，csv的reader()方法会返回一个迭代器，如何控制它呢？



```python
csv_file = open('filename', 'r')

reader = csv.reader(csv_file)

for row in reader:
	print(row)
'''这种方法可以遍历每一行

or
'''

next(reader) # 每次会返回一个对象，并将指针指向下一行
```

