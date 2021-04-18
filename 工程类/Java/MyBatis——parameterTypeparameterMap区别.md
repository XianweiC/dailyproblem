# MyBatis——parameterType/parameterMap区别



在进行学习过程中，曾经困扰许久，出现错误而找不到原因



parameterMap，适合单参数的情况

如：

```java
List<> selectByQuery(@Param("id") String id, @Param("entityId") String entityId);
```



此时在Mapper.xml中：
```XML
<select id = "selectByQuery" paramterMap = "map" ></select>
```
