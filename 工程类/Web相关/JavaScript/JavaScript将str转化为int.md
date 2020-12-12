# JavaScript将str转化为int

## 1.常规做法

```javascript
parseInt(str);
parseFloat(str);
```

## 2.骚操作

来自于偶然的脑洞，既然javascript是弱类型语言，那么是不是可以将str先减去0，自动转换成int类型呢？

不废话，直接操作。

```javascript
var a = "2";
alert(a+1);
//21
var b = a - 0;
alert(b+1);
//3
```

