# CSS绘制三角形

## 原理

由于border四个边并不是我们想象中的矩形，而是梯形，所以思路很清楚

就是将梯形的上底边尽量窄（这样就缩为一个三角形了），并设置另外三边透明即可。

## 代码



```css
div{
             width:0px;  
             height:0px;  
             border:40px solid transparent;
             border-bottom:80px solid red;
        }
```

效果如下

<div
     style="width:0px;  
             height:0px;  
             border:40px solid transparent;
             border-bottom:80px solid red;"></div>