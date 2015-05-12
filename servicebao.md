# service包

service包里面也装了两种类型的文件，一种是以`ConditionBuilder`结尾的java类，一种是以`Service`结尾的java类。

ConditonBuilder类的主要作用是构造Condition类，Condition类主要装载了数据库sql语句的查询条件，我们后文细说。

`Service`类都继承自`org.siqisource.stone.service.AbstractService<T>`，其中T是指模块的model，它包含18个数据库操作方法。