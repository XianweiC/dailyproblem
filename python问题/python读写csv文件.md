# python读写csv文件

## 直接上代码

```python
import csv

# open 打开文件有多种模式，下面是常见的4种
# r：读数据，默认模式
# w：写数据，如果已有数据则会先清空
# a：向文件末尾追加数据
# x : 写数据，如果文件已存在则失败
# 第2至4种模式如果第一个参数指定的文件不存在，则会先创建一个空文件
with open('1.csv', 'w', newline='') as f:    
    head = ['标题列1', '标题列2']
    rows = [
                ['张三', 80],
                ['李四', 90]
            ]  
    writer = csv.writer(f) 
    #写入一行数据
    writer.writerow(head) 
    #写入多行数据
    writer.writerows(rows)
```

