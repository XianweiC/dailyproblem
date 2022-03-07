# C++ sort()函数使用小结

该方法包含在头文件

```c++
#include <algorithm>
```

例如：

```c++
//默认升序排列
sort(begin, end)

struct Student s[100]
//使用重载的函数来自定义排序方法
//切记重载放法不要括号
sort(s, s+100, compare)

bool compare(Student a, Student b)
{
    //降序
    return a.score > b.score;
}
```

