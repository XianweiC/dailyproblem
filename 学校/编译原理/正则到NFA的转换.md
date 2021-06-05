# 正则到NFA的转换     

# 有穷自动机

**作用**：将输入的序列转换成一个状态图，方便之后的处理。通常被用在词法分析器中。
 1）有穷自动机是一个识别器，对每个可能的的输入串简单的回答“是”或“否”。
 2）有穷自动机分为两类：
 a)不确定的有穷自动机（NFA）对其边上的标号没有任何限制。一个符号标记离开同一状态的多条边，并且空串ε也可以作为标号。
 b)确定的有穷自动机（DFA）有且只有一条离开该状态，以该符号位标号的边。

# 不确定的有穷自动机

### 定义

![NFA组成](https://img-blog.csdnimg.cn/20190403192826118.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_20,color_FFFFFF,t_70)

### 正则式转NFA

这里看一个示例，下图为正则表达式 (a | b) * abb转换为NFA
 [不懂正则表达式的同学可以看这里](https://blog.csdn.net/qq_40294512/article/details/88997304)

![一个示例](https://img-blog.csdnimg.cn/20190403193118982.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_20,color_FFFFFF,t_70)
 然后我们来具体看看是正则式怎么完成这个转换的：
 先一起来看几个简单的小例子，应该就懂了。
 ![1](https://img-blog.csdnimg.cn/20190403193634981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
 ![2](https://img-blog.csdnimg.cn/20190403193712336.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
 ![3](https://img-blog.csdnimg.cn/20190403193734120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
 ![4](https://img-blog.csdnimg.cn/20190403193751486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_20,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403193901589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_20,color_FFFFFF,t_70)
 看到这，基本就懂了NFA的构建了。其实并不难，很简单。
 这里再提一点，抛砖引玉一下，就是对于计算机来讲，构建NFA时通常采用的是自底向上的组合法，而人的逻辑通常是自顶向下的分解法。略微有些差异，感兴趣的同学可以研究讨论一下这一点，这里不做过多的提及。
 做完转换图后，我们还是要把他变成一个表，因为只有变成一个表，才能有效的将数据录入的计算机内进行运算与处理。还是用之前的例子吧。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190403194508961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_20,color_FFFFFF,t_70)
 找出所有可以被匹配的字符即符号集合∑作为每一列的字段名，然后从起始态开始
 1）状态0可以匹配a，匹配后可以到状态0或状态1，记为{0,1}。匹配b只能得到状态0，记为{0}。
 2）状态1可以匹配a，没有匹配到，记为∅。匹配b得到状态2，记为{2}。
 3）状态0可以匹配a，没有匹配到，记为∅。匹配b得到状态3，记为{3}。
 4）状态0可以匹配a，没有匹配到，记为∅。匹配b没有匹配到，记为∅。

至此，状态表建立完成。正则式（RE）转不确定型有穷自动机（NFA）完成。