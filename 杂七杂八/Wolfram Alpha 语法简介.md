# Wolfram Alpha 语法简介

Wolfram  Alpha是新一代知识搜索引擎，它可以作为一个Web版的数学计算工具来用，功能非常强大。输入方面，WA的语法很接近自然语言，习惯用英语的人一般很快就能适应。但是如果英语不好，尤其是对各种术语和表达方式不习惯，使用起来就会有些吃力。下面列出一些常见的运算的输入方法，以供参考。

基本运算和符号：
绝对值：abs()

根号：sqrt()

圆周率：pi （其他希腊字母也类似）

正无穷：+infinity

一般运算：

大多数情况下，只需要输入f(x)，WA就会返回一系列有关f(x)的计算结果。不过，也可以通过下面的方法来有针对性的对f(x)进行运算。

画图：plot f(x)

分解因式：factor f(x)

展开：expand f(x)

化简：simplify f(x)

配方：complete the square f(x)

化为部分分式：partial fractions f(x)


其他运算：
使用的时候，请注意变量的替换。一些显而易见的变量我没有标注（例如点坐标）。

值表：Table[f(x),{x,a,b,c}]，其中a=起始值, b=终了值, c=步长

求两点间距离：distance between (x1,y1)(x2,y2)

求过两点直线的斜率：slope of line through (x1,y1)(x2,y2)

求过两点直线的方程：equation of a line through (x1,y1)(x2,y2)

求过三点的圆的方程：circle through (x1,y1)(x2,y2)(x3,y3)

求过三点的抛物线的方程：parabola through (x1,y1)(x2,y2)(x3,y3)

求f(x)中x趋于a时的极限：limit f(x) as x->a

求f(x)的n阶导数：D[f(x),{x,n}]

求f(x)的不定积分：integrate f(x)

求f(x)的定积分：integrate f(x) from a to b，其中a=积分下限, b=积分上限

求极值可疑点（即导数为0或不存在的点）：critical points f(x)

求拐点：inflection points f(x)

求极大值点：local maxima f(x)

求极小值点：local minima f(x)

求最大值点：maximize f(x)

求最小值点：minimize f(x)

求n从a取到b时表达式f(n)的各项和：sum f(n) for n=a to b 