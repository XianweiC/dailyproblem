# Python—requests模块详解         

### 1、模块说明

requests是使用Apache2 licensed 许可证的HTTP库。

用python编写。

比urllib2模块更简洁。

Request支持HTTP连接保持和连接池，支持使用cookie保持会话，支持文件上传，支持自动响应内容的编码，支持国际化的URL和POST数据自动编码。

在python内置模块的基础上进行了高度的封装，从而使得python进行网络请求时，变得人性化，使用Requests可以轻而易举的完成浏览器可有的任何操作。

现代，国际化，友好。

requests会自动实现持久连接keep-alive

### **2、基础入门**

**1）导入模块**

```
import requests
```

**2）发送请求的简洁**

　　示例代码：获取一个网页（个人github）

```
import requests

r = requests.get('https://github.com/Ranxf')       # 最基本的不带参数的get请求
r1 = requests.get(url='http://dict.baidu.com/s', params={'wd': 'python'})      # 带参数的get请求
```

我们就可以使用该方式使用以下各种方法

```
1   requests.get(‘https://github.com/timeline.json’)                                # GET请求
2   requests.post(“http://httpbin.org/post”)                                        # POST请求
3   requests.put(“http://httpbin.org/put”)                                          # PUT请求
4   requests.delete(“http://httpbin.org/delete”)                                    # DELETE请求
5   requests.head(“http://httpbin.org/get”)                                         # HEAD请求
6   requests.options(“http://httpbin.org/get” )                                     # OPTIONS请求
```

**3）为url传递参数**

```
>>> url_params = {'key':'value'}       #    字典传递参数，如果值为None的键不会被添加到url中
>>> r = requests.get('your url',params = url_params)
>>> print(r.url)
　　your url?key=value
```

**4）响应的内容**

```
r.encoding                       #获取当前的编码
r.encoding = 'utf-8'             #设置编码
r.text                           #以encoding解析返回内容。字符串方式的响应体，会自动根据响应头部的字符编码进行解码。
r.content                        #以字节形式（二进制）返回。字节方式的响应体，会自动为你解码 gzip 和 deflate 压缩。

r.headers                        #以字典对象存储服务器响应头，但是这个字典比较特殊，字典键不区分大小写，若键不存在则返回None

r.status_code                     #响应状态码
r.raw                             #返回原始响应体，也就是 urllib 的 response 对象，使用 r.raw.read()   
r.ok                              # 查看r.ok的布尔值便可以知道是否登陆成功
 #*特殊方法*#
r.json()                         #Requests中内置的JSON解码器，以json形式返回,前提返回的内容确保是json格式的，不然解析出错会抛异常
r.raise_for_status()             #失败请求(非200响应)抛出异常
```

post发送json请求：

```
1 import requests
2 import json
3  
4 r = requests.post('https://api.github.com/some/endpoint', data=json.dumps({'some': 'data'}))
5 print(r.json())
```

**5）定制头和cookie信息**

```
header = {'user-agent': 'my-app/0.0.1''}
cookie = {'key':'value'}
 r = requests.get/post('your url',headers=header,cookies=cookie) 
data = {'some': 'data'}
headers = {'content-type': 'application/json',
           'User-Agent': 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:22.0) Gecko/20100101 Firefox/22.0'}
 
r = requests.post('https://api.github.com/some/endpoint', data=data, headers=headers)
print(r.text)
```

**6）响应状态码**

使用requests方法后，会返回一个response对象，其存储了服务器响应的内容，如上实例中已经提到的 r.text、r.status_code……
获取文本方式的响应体实例：当你访问 r.text 之时，会使用其响应的文本编码进行解码，并且你可以修改其编码让 r.text 使用自定义的编码进行解码。

```
1 r = requests.get('http://www.itwhy.org')
2 print(r.text, '\n{}\n'.format('*'*79), r.encoding)
3 r.encoding = 'GBK'
4 print(r.text, '\n{}\n'.format('*'*79), r.encoding)
```

示例代码：

```
1 import requests
2 
3 r = requests.get('https://github.com/Ranxf')       # 最基本的不带参数的get请求
4 print(r.status_code)                               # 获取返回状态
5 r1 = requests.get(url='http://dict.baidu.com/s', params={'wd': 'python'})      # 带参数的get请求
6 print(r1.url)
7 print(r1.text)        # 打印解码后的返回数据
```

运行结果：

```
/usr/bin/python3.5 /home/rxf/python3_1000/1000/python3_server/python3_requests/demo1.py
200
http://dict.baidu.com/s?wd=python
…………

Process finished with exit code 0
 r.status_code                      #如果不是200，可以使用 r.raise_for_status() 抛出异常
```

**7）响应**

```
r.headers                                  #返回字典类型,头信息
r.requests.headers                         #返回发送到服务器的头信息
r.cookies                                  #返回cookie
r.history                                  #返回重定向信息,当然可以在请求是加上allow_redirects = false 阻止重定向
```

**8）超时**

```
r = requests.get('url',timeout=1)           #设置秒数超时，仅对于连接有效
```

**9)会话对象，能够跨请求保持某些参数**

```
s = requests.Session()
s.auth = ('auth','passwd')
s.headers = {'key':'value'}
r = s.get('url')
r1 = s.get('url1') 
```

**10）代理**

```
proxies = {'http':'ip1','https':'ip2' }
requests.get('url',proxies=proxies)
```

汇总：

```
# HTTP请求类型
# get类型
r = requests.get('https://github.com/timeline.json')
# post类型
r = requests.post("http://m.ctrip.com/post")
# put类型
r = requests.put("http://m.ctrip.com/put")
# delete类型
r = requests.delete("http://m.ctrip.com/delete")
# head类型
r = requests.head("http://m.ctrip.com/head")
# options类型
r = requests.options("http://m.ctrip.com/get")

# 获取响应内容
print(r.content) #以字节的方式去显示，中文显示为字符
print(r.text) #以文本的方式去显示

#URL传递参数
payload = {'keyword': '香港', 'salecityid': '2'}
r = requests.get("http://m.ctrip.com/webapp/tourvisa/visa_list", params=payload) 
print（r.url） #示例为http://m.ctrip.com/webapp/tourvisa/visa_list?salecityid=2&keyword=香港

#获取/修改网页编码
r = requests.get('https://github.com/timeline.json')
print （r.encoding）


#json处理
r = requests.get('https://github.com/timeline.json')
print（r.json()） # 需要先import json    

# 定制请求头
url = 'http://m.ctrip.com'
headers = {'User-Agent' : 'Mozilla/5.0 (Linux; Android 4.2.1; en-us; Nexus 4 Build/JOP40D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Mobile Safari/535.19'}
r = requests.post(url, headers=headers)
print （r.request.headers)

#复杂post请求
url = 'http://m.ctrip.com'
payload = {'some': 'data'}
r = requests.post(url, data=json.dumps(payload)) #如果传递的payload是string而不是dict，需要先调用dumps方法格式化一下

# post多部分编码文件
url = 'http://m.ctrip.com'
files = {'file': open('report.xls', 'rb')}
r = requests.post(url, files=files)

# 响应状态码
r = requests.get('http://m.ctrip.com')
print(r.status_code)
    
# 响应头
r = requests.get('http://m.ctrip.com')
print (r.headers)
print (r.headers['Content-Type'])
print (r.headers.get('content-type')) #访问响应头部分内容的两种方式
    
# Cookies
url = 'http://example.com/some/cookie/setting/url'
r = requests.get(url)
r.cookies['example_cookie_name']    #读取cookies
    
url = 'http://m.ctrip.com/cookies'
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies) #发送cookies

#设置超时时间
r = requests.get('http://m.ctrip.com', timeout=0.001)

#设置访问代理
proxies = {
           "http": "http://10.10.1.10:3128",
           "https": "http://10.10.1.100:4444",
          }
r = requests.get('http://m.ctrip.com', proxies=proxies)


#如果代理需要用户名和密码，则需要这样：
proxies = {
    "http": "http://user:pass@10.10.1.10:3128/",
}
```



```
# HTTP请求类型
# get类型
r = requests.get('https://github.com/timeline.json')
# post类型
r = requests.post("http://m.ctrip.com/post")
# put类型
r = requests.put("http://m.ctrip.com/put")
# delete类型
r = requests.delete("http://m.ctrip.com/delete")
# head类型
r = requests.head("http://m.ctrip.com/head")
# options类型
r = requests.options("http://m.ctrip.com/get")

# 获取响应内容
print(r.content) #以字节的方式去显示，中文显示为字符
print(r.text) #以文本的方式去显示

#URL传递参数
payload = {'keyword': '香港', 'salecityid': '2'}
r = requests.get("http://m.ctrip.com/webapp/tourvisa/visa_list", params=payload) 
print（r.url） #示例为http://m.ctrip.com/webapp/tourvisa/visa_list?salecityid=2&keyword=香港

#获取/修改网页编码
r = requests.get('https://github.com/timeline.json')
print （r.encoding）


#json处理
r = requests.get('https://github.com/timeline.json')
print（r.json()） # 需要先import json    

# 定制请求头
url = 'http://m.ctrip.com'
headers = {'User-Agent' : 'Mozilla/5.0 (Linux; Android 4.2.1; en-us; Nexus 4 Build/JOP40D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Mobile Safari/535.19'}
r = requests.post(url, headers=headers)
print （r.request.headers)

#复杂post请求
url = 'http://m.ctrip.com'
payload = {'some': 'data'}
r = requests.post(url, data=json.dumps(payload)) #如果传递的payload是string而不是dict，需要先调用dumps方法格式化一下

# post多部分编码文件
url = 'http://m.ctrip.com'
files = {'file': open('report.xls', 'rb')}
r = requests.post(url, files=files)

# 响应状态码
r = requests.get('http://m.ctrip.com')
print(r.status_code)
    
# 响应头
r = requests.get('http://m.ctrip.com')
print (r.headers)
print (r.headers['Content-Type'])
print (r.headers.get('content-type')) #访问响应头部分内容的两种方式
    
# Cookies
url = 'http://example.com/some/cookie/setting/url'
r = requests.get(url)
r.cookies['example_cookie_name']    #读取cookies
    
url = 'http://m.ctrip.com/cookies'
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies) #发送cookies

#设置超时时间
r = requests.get('http://m.ctrip.com', timeout=0.001)

#设置访问代理
proxies = {
           "http": "http://10.10.1.10:3128",
           "https": "http://10.10.1.100:4444",
          }
r = requests.get('http://m.ctrip.com', proxies=proxies)


#如果代理需要用户名和密码，则需要这样：
proxies = {
    "http": "http://user:pass@10.10.1.10:3128/",
}
```