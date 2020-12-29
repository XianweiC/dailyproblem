# C++获得数组大小

```c++
//可以把这个方法定义成宏，方便使用
//如：#define length(array) sizeof(array)/sizeof(array[0])
int length = sizeof(array)/sizeof(array[0]);
```

思路：sizeof()返回的是数组所占内存，而sizeof(array[0])返回的是数组第一个元素所占内存，由此可以得出数组长度。