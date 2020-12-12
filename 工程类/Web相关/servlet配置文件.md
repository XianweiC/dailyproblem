# servlet配置

## 1.servlet需要在web目录下的WEB-INF--->web.xml文件中配置servlet信息

```xml
<!--声明servlet-->
<servlet>
	<servlet-name>这里是servlet的name</servlet-name>
	<servlet-class>servlet所处的位置，需要包括完整的包名</servlet-class>
</servlet>
<!--映射servlet地址-->
<servlet-mapping>
	<servlet-name>servlet的name</servlet-name>
	<url-pattern>映射到服务器的地址</url-pattern>
</servlet-mapping>
```

注：关于映射地址，是指在服务器上的虚拟映射地址，也就是在网址栏显示的地址

## 2.在servlet 3.0新特性

**servlet新特性，可以通过注解来实现配置servlet，具体实现方法为：**

```java
@webservlet(name = "这里是servlet的name", urlpatterns = "这里制定映射到服务器的地址")
```

此时就无需在web.xml中编写配置信息。