# CSS样式细节



```css

//首行缩进
text-indent:2em;

//字间距
letter-spacing:

//行间距
line-height:2em;


//设置文本一行显示
.view-text{
  /**
	思路：
	1.设置inline-block属性
	2.强制不换行
	3.固定高度
	4.隐藏超出部分
	5.显示“……”
  */
  display: inline-block;
  white-space: nowrap; 
  width: 100%; 
  overflow: hidden;
  text-overflow:ellipsis;
}
```

