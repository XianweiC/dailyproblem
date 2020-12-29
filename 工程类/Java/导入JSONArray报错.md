# 导入JSONArray报错

```
java.lang.NoClassDefFoundError: net/sf/json/JSONArray  cn.xaut.Servlet.ShowS。。。。

原因是：不但要在IDEA中project structure下导入jar包，还需要将jar包移动到WEBCONTENT->WEB-INF->lib文件夹下
```



# 调用Servlet FireFox报错

# xml 解析错误：语法错误     xml解析错误：找不到根元素

问题描述：

火狐浏览器在调试的时候报： 

1、xml 解析错误：语法错误

解决方法：

在servlet代码中，doGet/doPost方法中添加如下方法

```
response.setContentType("text/text;charset=utf-8");

response.setCharacterEncoding("UTF-8");
```

2、xml解析错误：找不到根元素

解决办法（传给前台一个结果）：

response.getWriter().print("success");

