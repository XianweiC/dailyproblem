# `sql-server` ——存储过程

## 引言：

**存储过程（Stored Procedure）是一种在数据库中存储复杂程序，以便外部程序调用的一种数据库对象。**

**存储过程是为了完成特定功能的`SQL`语句集，经编译创建并保存在数据库中，用户可通过指定存储过程的名字并给定参数(需要时)来调用执行。**

**存储过程思想上很简单，就是数据库` SQL` 语言层面的代码封装与重用。**

### 个人理解：

存储过程，可以看做是一个封装好的`sql`函数,通过调用这个函数即可执行一系列的`SQL`语句。

--------------------------

## 存储器的创建：

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

## 存储器的执行：

```sql
1> EXEC getUser 201215121; --EXEC ‘存储器名’ ‘传递的参数’
2> go
Sno          Sname                Ssex       Sage   Sdept               
------------ -------------------- ---------- ------ --------------------
201215121    yong                 male           20 CS                  
```



### 解释一下：

存储过程的的创建包括：声明---->传递的参数---->执行的`sql`部分

声明：

CREATE PROCEDURE 'name'

传递参数：

`@Param `  '参数类型'

执行部分，需要用begin...end包裹

## 存储过程的删除

一句`sql`语句,使用`proc`简写也可以

```sql
1> DROP PROCEDURE/PROC getUser;
2> go
1> EXEC getUser 201215121;
2> go
Msg 2812, Level 16, State 62, Server ThinkPad-E580, Line 1
找不到存储过程 'getUser'
```

## 存储过程的修改

例如修改存储过程的参数、执行的`sql`语句等。

```sql
ALTER PROCEDURE getUser @Sno int,
                        @Sage int
as
    set nocount on;
begin
    select * from Student where Sno = @Sno AND Sage = @Sage
end;
```

在这里，我进行了简单修改，也就是增加了一个字段作为`select`条件

```sql
EXEC getUser 201215121, 20
```

### 执行结果

```sql
1> EXEC getUser 201215121, 20
2> go
Sno          Sname                Ssex       Sage   Sdept               
------------ -------------------- ---------- ------ --------------------
201215121    yong                 male           20 CS                  
```

