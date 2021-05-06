# NFA到DFA的转换及DFA的简化

# 确定型有穷自动机

确定型有穷自动机是不确定有穷自动机中的一个特例，其中：

1. 没有输出ε之上的转换动作。
2. 对每个状态s和每个输入符号a，有且只有一条标号为a的边离开s

# 确定型有穷自动机的转换

下面来看看NFA怎么转换为DFA吧
 先来看看一会会涉及到操作
 ![涉及的操作](https://img-blog.csdnimg.cn/20190405162344281.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
 以下为算法
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405162812679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)

看完算法可能还是有些懵逼，我们一起来过一遍实例。以下图为例。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191007171747390.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjk0NTEy,size_16,color_FFFFFF,t_70)

1. 先构建一个这样的表格
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019040516471895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
2. 然后从起始态出发，做空串的kleene闭包，得到{ 0,1,2,4,7}，填入NFA的第一行，DFA此时命名为A（或数字1，甚至是α都可以），然后对这个得到的闭包做  move（a）操作，即用这个闭包的所有状态去匹配a，可以得到{1,2,3,4,6,7,8}，发现是一个全新的状态，填到NFA的第二行，给其DFA命名为B，然后在a下填入B。
3. 然后还是用A去做 move（b） 操作，得到全新闭包{1,2,4,5,6,7}，例如NFA第三行，称其为C，在b的第一行填入C。至此，得到下表
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405165355871.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
4. 然后再对B做 move（a）和 move（b）操作，得到
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405165537138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
5. 操作C得到
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405165641278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
6. 操作D得到
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019040516572088.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
7. 操作E得到，此时发现旧状态全部处理完，且没有出现新状态。那么我们的DFA就求完了。
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405165748934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
8. 将状态表转换为状态图（这里需要注意，A为第一个起始状态，所以A为起始态。由于E包含接收态10，故E为接收态），整个转换过程就全部结束了。这个方法我们称其为子集构造法
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405170238404.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)

# DFA的简化

对于同一个语言，可以存在多个识别此语言的DFA，所以，求出DFA后，通常我们还需要对DFA进行简化操作，求出最简DFA。
 简化的本质是合并性质相同的状态，以减少整个图的大小。

### 算法

1. 将得到的状态进行划分 ∏ ，划分为两部分，一部分为接收态，一部分为为非接收态组。
2. 继续进行划分，通过其可以匹配的字符进行判断，若该组内所有成员匹配字符都落在同一组内，即不可再分，否则重新划分组
3. 若 ∏new = ∏ ，则进入步骤4，否则返回2
4. 在分组 ∏new 每个组中选取一个状态作为代表，代表DFA的最简状态。

### 实例

直接用上图转换出来的DFA来做。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405170238404.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)

1. 分组，得到 {A,B,C,D} {E}
2. {E} 独自分组，无法操作。 {A,B,C,D}做a操作，发现都转为状态B，做b操作，A，B，C在 {A,B,C,D} 组内成员，而D在另一个组内，重新分组得到 {A,B,C} {D} {E}
3. {D} {E}无法操作， {A,B,C} 做a操作，都在同一组内，做b操作，B不在同一组内，重新划分，重新分组得到 {A,C} {B} {D} {E}
4. {A,C} 进行a操作和b操作都在同一组内，无法继续向下划分了。操作到此结束。可以将 {A,C}合并
5. 得到以下转换表
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190405172553921.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_WWludm9rZXIncyBDU0ROIEJMT0c=,size_16,color_FFFFFF,t_70)
6. 转换为状态图后
    ![最简DFA](https://img-blog.csdnimg.cn/2019040517322514.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjk0NTEy,size_16,color_FFFFFF,t_70)
    至此我们NFA转DFA及DFA的简化全部完成了。