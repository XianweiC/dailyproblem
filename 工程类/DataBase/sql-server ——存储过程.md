# sql-server ——存储过程

## 引言：

**存储过程（Stored Procedure）是一种在数据库中存储复杂程序，以便外部程序调用的一种数据库对象。**

**存储过程是为了完成特定功能的`SQL`语句集，经编译创建并保存在数据库中，用户可通过指定存储过程的名字并给定参数(需要时)来调用执行。**

**存储过程思想上很简单，就是数据库` SQL` 语言层面的代码封装与重用。**

### 个人理解：

存储过程，可以看做是一个封装好的`sql`函数,通过调用这个函数即可执行一系列的`SQL`语句。

--------------------------

不废话，直接上`sql`：

```sql
--存储过程的创建
CREATE PROCEDURE getUser --创建存储过程
    @Sno int --传递的参数
as
    set nocount on; --不返回计数，提高应用程序能力
begin
    --开始
    select * from Student where Sno = @Sno --执行sql语句
end;
```

其中，Student表格内容为：

```sql
Sno          Sname                Ssex       Sage   Sdept               
------------ -------------------- ---------- ------ --------------------
201215121    yong                 male           20 CS                  
201215122    liuchen              female         19 CS                  
201215123    wangmin              female         18 MA                  
201215124    zhangli              male           19 IS                  
201215125    zhangsan             male           19 EE                  
201215126    liuwu                male           20 IA                  
201215127    zhangsi              male           19 IS                  
201215128    angwu                female         23 CS                  
201215129    lanzhou              male           19 EE                  
201215130    wubai                female         19 IS                  
```

## 执行结果：

```sql
1> EXEC getUser 201215121;
2> go
Sno          Sname                Ssex       Sage   Sdept               
------------ -------------------- ---------- ------ --------------------
201215121    yong                 male           20 CS                  
```



## 解释一下：

存储过程的的创建包括：声明---->传递的参数---->执行的sql部分

声明：

CREATE PROCEDURE 'name'

传递参数：

`@Param `  '参数类型'

执行部分，需要用begin...end包裹