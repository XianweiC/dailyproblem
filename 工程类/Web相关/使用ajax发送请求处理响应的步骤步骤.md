# 使用ajax发送请求/处理响应的步骤步骤

## 1.发送请求

### 1>初始化`XMLHttpRequest`对象

由于IE浏览器和其他浏览器初始化方式有所不同，需要考虑这种情况

```javascript
function createRequest(){
    let xhr = false;
    if(window.XMLHttpRequest){
        //Chrome、FireFox
        xhr = new XMLHttpRequest();
        return xhr;
    }else if(window.ActiveXObject){
        try{
            xhr = new ActiveXObject("Msxml2.XMLHTTP");
            return xhr;
        } catch(e) {
            xhr = new ActiveXObject("Micorsoft.XMLHTTP");
            return xhr;
        } chtch(e){}
    }
    
    if(!xhr){
        alert("浏览器不支持XMLHttpRequest");
        return false;
    }
}
```

### 2>为`XMLHttpRequest`对象指定一个返回结果处理函数(回调函数),调用该方法不能添加括号和参数，如需添加参数，可采用 使用匿名函数的方法来进行。

```javascript
xhr.onreadystatechange = getResult;
or
xhr.onreadystatechange = function(){
	getResult(param);
};
```

### 3>创建一个与服务器的连接

参数包括，请求方式、URL、是否为异步请求，默认为true

```
xhr.open("GET/POST","URL",true/false);
```

### 4>向服务器发送请求

```javascript
//GET方式
xhr.send(null);

//POST需设置请求头
xhr.setRequestHeader("COntent-Type","application/x-www-form-urlencoded");
xhr.send(content);
```

------------------

## 2.处理响应

处理响应是通过`onreadystatechange`来指定回调函数实现的

```javascript
function getResult(){
    if(xhr.readystate == 4){
        if(xhr.status == 200){
            alert(xhr.responseText);
        }else{
            alert("请求的页面有错误！");
        }
    }
}
```

