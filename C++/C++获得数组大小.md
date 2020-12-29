# C++获得数组大小

```c++
//可以把这个方法定义成宏，方便使用
//如：#define length(array) sizeof(array)/sizeof(array[0])
int length = sizeof(array)/sizeof(array[0]);
```

思路：sizeof()返回的是数组所占内存，而sizeof(array[0])返回的是数组第一个元素所占内存，由此可以得出数组长度。

测试一下：

```c++
#include<cstdio>

#define length(array) sizeof(array)/sizeof(array[0])

int main()
{
    int a[] = {0,1,2,3,4};
    printf("%d",length(a));
    return 0;
}
```

输出：

```
5
Process finished with exit code 0
```

-----

## 更进一步的

获取二维数组的长度。。。

```c++
#include<cstdio>
#include<iostream>
using namespace std;

//该宏得出二维数组的行数
#define length(array) sizeof(array)/sizeof(array[0])
//该宏得出二维数组的列长度
#define row(array) sizeof(array[0])/sizeof(array[0][0])

int main()
{
    int a[] = {0,1,2,3,4};
    int array[][3] = {{1,2,3},{4,5,6}};

    int lengths = length(array);
    cout<<lengths<<endl;

    int sum = sum(array);
    cout<<sum<<endl;
    
    printf("a的长度：%d\n",length(a));
    
    printf("array行数：%d\n", length(array));
    printf("每行列数：%d\n",row(array));
    return 0;
}
```

