# JDBC操作的一些细节

## Statement接口的execute()、executeUpdate()、executeQuery()方法

1>execute()一般用于执行单条SQL语句，执行成功2返回true，失败返回false。

2>executeQuery()一般用于执行查询类型(SELECT)类型的语句，此方法返回查询所获取的结果集，以`ResultSet`对象保存。

2>executeUpdate()一般用于执行`insert/delete/update`类型的SQL语句，返回更新所影响的行数。

