# servlet配置文件

## servlet需要在web目录下的WEB-INF--->web.xml文件中配置servlet信息

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

