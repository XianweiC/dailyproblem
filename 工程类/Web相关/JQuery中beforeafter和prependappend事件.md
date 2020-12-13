# `JQuery`中`before/after`和`prepend/append`方法

引言：

在进行`JavaWeb`复习过程中，对于标题所述两对事件的区别不够了解，因此总结如下。

`prepend()/append()`是在被选元素的内部嵌入。

`before()/after()`是在被选元素外面追加。

--------------------

语言总是单薄的，直接上代码。

```javascript
$(document).ready(function(){
			$(".test1").click(function(){
				$(".test1").after('明天');
			})
			$(".test1").dblclick(function(){
				$(".test1").hide()
			})
    		$(".test2").click(function(){
				$(".test2").append('昨天');
			})
			$(".test2").dblclick(function(){
				$(".test2").hide()
			})
		})
```

```html
<p class="test1">你好</p>
<p class="test2">你也好</p>
```

当鼠标单击时，双击之后，可以发现，“明天”被保留了下来，“昨天”则随着文本一起消失。

这是由于，`before()/after()`方法相当于添加在p标签之后，即`</p>`之后，不会受到`hide()`事件的影响。

但`prepend()/append()`方法是添加在p标签之内，只是位于p标签的文本前后，所以随着p标签一起隐去了。