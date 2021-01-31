# `mysql`创建触发器

## 引言：

由于在课程设计中需要用到mysql，因此总结一下mysql的触发器建立过程

```sql
CREATE TRIGGER <trigger_name>
BEFORE | AFTER
INSERT | UPDATE | DELETE
ON <table_name>
FOR EACH ROW
BEGIN
	sql语句
END;
```

before和after有什么区别？

其实要理解这个区别，一定要牢记的就是，`mysql`在插入操作的时候，是先将数据保存在内存`new`表中，再将数据写入磁盘，删除操作时，是先将要删除的数据保存在内存的old表中，再写入磁盘完成删除。

这个before和after是相对这个临时表 new或old相对而言的。定义after就是指在临时表从内存更新到磁盘之后才触发，定义before就是指，在临时表更新到磁盘之前触发。