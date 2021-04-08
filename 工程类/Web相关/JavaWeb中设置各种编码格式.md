# `JavaWeb`中设置各种编码格式

## 引言：JSP中一系列编码格式实在是搞得人晕头转向，下面来整理一下。

先看一段代码：

```jsp
<%@ page pageEncoding="UTF-8" contentType="text/html;charset=UTF-8"%>
```

```java
request.setCharacterEncoding("UTF-8");

response.setCharacterEncoding("UTF-8");
response.setContentType("text/html;charset=UTF-8");
```

## 1.**`pageEncoding=”UTF-8”`**

作用是设置`JSP`页面本身的编码，也就是编译成`Servlet`时使用的编码。 

## 2.**`contentType=”text/html;charset=UTF-8”`**

作用是指定服务器响应给浏览器的编码。

## 3.`request.setCharacterEncoding(“UTF-8”)`

作用是设置对客户端请求和数据库取值时的编码，不指定的话使用`iso-8859-1`(注：自`Tomcat 8.0`之后，编码格式默认为`UTF-8`)。(只解决POST乱码) 

解决GET乱码可以修改tomcat的`server.xml`中的 `URIEncoding`属性 
或使用`str = new String(str.getBytes("iso-8859-1"),"utf-8");` 

## 4.`response.setCharacterEncoding(“UTF-8”)`

作用是指定服务器响应给浏览器的编码。

## 5、`response.setContentType(“text/html;charset=utf-8”)`

作用是指定服务器响应给浏览器的编码。同时，浏览器也是根据这个参数来对其接收到的数据进行重新编码（或者称为解码）。

对于发送数据，服务器按照**`response.setCharacterEncoding—>contentType—>pageEncoding`**的优先顺序，对要发送的数据进行编码。