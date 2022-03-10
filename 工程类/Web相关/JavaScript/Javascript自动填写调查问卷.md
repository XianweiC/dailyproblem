# Javascript自动填写调查问卷

**引言：**

​	最初受朋友委托填写调查问卷，发现选项过多，于是想采用js实现快速填写

**思路**：

设置定时器不断提交（刷问卷数量），

```javascript
setTimeout(function () {
    //用于保存id
	var str = new Array(24);
	for (let i = 0; i < str.length; i++) {
		str[i] = new Array(23);
	}

    //拼接获得输入框id
	for (let i = 0; i <= 23; i++) {
		for (let j = 0; j <= 23; j++) {
			str[i][j] = "q1_" + i + "_" + j;
		}
		i = Number(i);
	}

    //生成随机数填写问卷
	for (let i = 0; i <= 23; i++) {
		for (let j = 0; j <= 23; j++) {
			document.getElementById(str[i][j]).value = Math.ceil(Math.random() * 5);
		}
	}

    //自动点击提交按钮
	document.getElementById("ctlNext").click();

    //这里定时器采用随机时间模拟真人填写
}, Math.ceil(Math.random() * 4500));
```

