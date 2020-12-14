# `sql-server`——触发器

## 引言：

触发器，是一种特殊的存储过程，用它来控制关联的表。它不能被显式地调用﹐而是在往表中插入记录﹑更新记录或者删除记录时被自动地激活。所以触发器可以用来实现对表实施复杂的完整性约束。

**个人理解：**

触发器，正如其名，是在某一特定情况下才执行的特殊的存储过程。

## 触发器的建立

```sql
CREATE TRIGGER Delete_Trigger
    ON Student
    FOR DELETE
    AS
    SELECT *
    FROM Student;
```

这一触发器是在执行DELETE语句时才触发，效果是执行select语句显示表中的所有信息。

## 触发器的执行

由于触发器不能显式执行，需要按照建立时的条件才能触发

```sql
例如：
DELETE FROM Student WHRER Sage=23
--执行后就可以显示表中所有信息
```

## 触发器的修改

```sql
ALTER TRIGGER Delete_Trigger
...
...
```

触发器的修改可以类比与存储过程的修改。

## 触发器的删除

```sql
DROP TRIGGER Delete_Trigger
```

