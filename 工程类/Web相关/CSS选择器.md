# CSS选择器

## 页面包含CSS的方式

```
行间样式 => 直接在标签内引用
内嵌式 => 在header里的style标签下编写
链接式 => 在header里通过link标签导入
```

权重比较（进制：256进制）

!important Infinity
行间样式		1000
id					100
class				10
标签          		1
通配符        	0

## CSS选择器

### 1.通配符选择器

```html
*{
	//修饰页面内所有标签，包括html、head、body
}
```

### 2.标记选择器（标签选择器）

```html
<a href=""></a>

a{
	font-size:25px;
}
```

### 3.类选择器class

```html
<a class="aaa" href=""></a>

.aaa{

}
```

### 4.属性选择器

```css
[id]{
	//修饰所有含该属性的标签，无论它们id、class的值是什么
}

[class]{
    
}
```

### 5.id选择器

```html
<a id="name" href=""></a>

#name{

}
```

## 6.行间样式

```html
<div style="border:2px"></div>
```

## 7. !important

添加于css属性之后

```css
.name{
	font-size:5px !important
}
```