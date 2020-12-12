# JavaScript显示网页倒计时

## 思路：很好理解，其实就是利用window.setInterval()方法定时修改DOM.

直接看代码：

```html
<html>
<head>
	
</head>
<body>

<h1 id="num">6</h1>

<script>
	var time = clockOver();
	function clockOver(){
				
		var time = document.getElementById("num");
				//alert(time.innerHTML);
				//获取到id为time标签中的内容，现进行判断
				if(time.innerHTML == 0){
					//等于0时清除计时
					return;
				}else{
					time.innerHTML = time.innerHTML-1;
				}
			}
			//1000毫秒调用一次
			if(document.getElementById("num") != 0)
				window.setInterval("clockOver()",1000);
	</script>
</body>

</html>
```

