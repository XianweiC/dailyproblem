# python——requests库编码问题

## 引言：

在编写微博爬虫时，分析网页异步请求的结果是十六进制的编码，需要进行编码转换，在此进行总结。

### 返回\u 16进制数字

```python
reponse.content.decode("unicode_escape")
```

### 返回乱码中文

```python
#获取网站原始编码
print(requests.utils.get_encodings_from_content(r.text)[0])
#设置编码: 
r.encoding= requests.utils.get_encodings_from_content(r.text)[0]
#打印 
print(r.text)
```

