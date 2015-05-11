# mapper包

mapper包用来存放数据库基本操作的接口，它们都继承自`org.siqisource.stone.orm.MybatisMapper<T>`接口,其中T代表的数据库表对应的`model`类。

`MybatisMapper`有13个方法，对应数据库的增删改查四个操作，它们的对应关系如下：




