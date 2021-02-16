# `window.setTimeout`函数用法

该方法的作用是设置一定时间后触发指定的函数。但不能通过直接通过直接调用的方式来实现。

**1.箭头函数**

```javascript
window.setTimeout( => () {
	//content    
}, 'time'
)
```

**2.匿名函数**

```javascript
window。setTimeout(function (){
	//content
}, 'time'
)
```

