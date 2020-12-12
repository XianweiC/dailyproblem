# JQuery技术

## 引言：JQuery本质上是一个JS库,可通过script标签导入。

```javascript
使用方法
$(selector).click()
选择器.触发事件

$(document).ready(function(){
    //这是JQuery的标准入口函数，可以理解为当web文件完全加载完时触发
})

常见的选择器：
/*可以类比为css选择器*/
$("p").click()//标签选择器
$(".class").click()//类选择器
$("#id").click()//id选择器

所有的事件方法，必须以回调函数作为参数
注：回调函数，可以理解为将返回值作为参数的函数
例如：
$("p").click(function(){
    //该function便是回调函数
})
```

