# 将SpringMVC打包并发布到Tomcat

## pom.xml添加如下


```xml
<packaging>war</packaging>
<build>
    <finalName>myapp</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.0</version>
            <configuration>
                <webResources>
                    <resource>
                        <!-- 原配置文件的目录，相对于pom.xml文件的路径 -->
                        <directory>src/myapp/WEB-INF</directory>
                        <!-- 目标路径 -->
                        <targetPath>WEB-INF</targetPath>
                    </resource>
                </webResources>
            </configuration>
        </plugin>
    </plugins>
</build>
```

运行

```cmd
mvn clean package
```

