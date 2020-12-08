# 对于JavaScript的一些理解

1.**安全性**：JavaScript不允许访问本地**硬盘**，不能将数据写入到**服务器**上，并且不允许对**网络文档**进行修改和删除，只能通过浏览器实现信息浏览或动态交互，从而有效地防止数据的丢失。

var file = new FileSystemObject("test.txt")

*解释：Javascript确实不允许直接访问本地硬盘，此处对于文件的访问，是来自于FSO（FileSystemObject）所带来的功能，与javas本身的特性并不冲突。*

2.Javascript中的类

javascript中的类按照类似json格式进行定义,甚至，，，连函数也不例外！

例如：

```javascript
let person = {
	var name:"",
	var age:"",
	hello:function{
		alert("你好我叫"+name+"今年"+age+"岁")
	}
}
```
