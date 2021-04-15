# Spring MVC踩坑



如下所示目录结构，记住

**web中静态资源文件不要放到`WEb-INF`目录下**,否则需要在XML中配置`mvc:resources mapping="" location="/WEB-INF/"`

只把`view`也就是jsp放在该目录下

```
root
├─src
│  ├─main
│  │  ├─java
│  │  │  └─edu
│  │  │      └─xaut
│  │  │          ├─controller
│  │  │          ├─dao
│  │  │          └─service
│  │  └─resources
│  └─test
│      └─java
└─web
    ├─static
    │  ├─css
    │  ├─img
    │  └─js
    └─WEB-INF
        └─view
```

