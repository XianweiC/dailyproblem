# CSS 实现添加半透明背景

## 问题

当希望设置半透明背景时，css中opacity属性在添加时，会继承给子标签，即：

```html
<div class="wrapper">
    <button class="child">I am child node.</button>
</div>
```

当添加css:

```css
.wrapper{
    background-img:url(path);
    opacity: 0.5;
}

.child{
    //子结点
}
```

此时，子结点也会受父节点修饰影响，从而变成半透明。

## 解决方案

将父结点容器设置为`relative`定位，并添加一个`absolute`定位到原来的位置，从而替代原本的背景位置



```html
<div class="wrapper">
    <button class="child"></button>
    <button class="background"></button>
</div>
```

此时的css:

```css
.wrapper{
    width: 100%;
    height: 100%;
}

.child{
    position: relative;
}

.background{
    opacity: 0.5;
    position: absolute;
    background-image: url(path);
}
```

