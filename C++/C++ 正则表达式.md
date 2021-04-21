# C++ 正则表达式

由于编译原理学习过程中需要使用，故整理一下。

## 引入头文件 

```#include <regex>```

## 声明规则

```c++
//匹配注释
std::regex regExpression("//.*");

//匹配成功返回true
bool ret = std::regex_match(string s, regExpression);
```



