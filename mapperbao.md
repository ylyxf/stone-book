# mapper包

mapper包用来存放数据库操作的接口，这些接口都应继承自`org.siqisource.stone.orm.MybatisMapper<T>`,其中T代表的数据库表对应的`model`类。

mapper包只存放接口，不需要写实现类，但是要在mapper接口对应的mapper.xml文件中，写上12条sql语句，以使其支持从`MybatisMapper`继承来的12个方法。这个写了12条sql语句的mapper.xml文件，应该放在项目的`src/main/resources/mappers`目录下，我们在写完后一般不要去改动它。

以订单系统为例：我们应该在mapper包下面增加OrderMapper.java文件，同时在`src/main/resources/mappers`目录下增加OrderMapper.xml文件。

如果模块内的mapper需要增加新的方法，则在mapper包内新增加一个同名mapper.xml文件，用来写新方法对应的sql。

还以订单列表为例，订单列表要显示客户、供应商的名字，从MybatisMapper继承下来的操作，都是针对单表的。此时，需要为OrderMapper类添加新方法：

```
    @Repository
    public interface OrderMapper extends MybatisMapper<Order>{
        public List<OrderView> listOrder(@Param("condition")Condition condition,@Param("rowBounds") RowBounds rowBounds);
    }
```
然后在mapper包下面，新建一个OrderMapper.xml文件，把上一节的那个联表查询的sql写进去。

这样分离后，比较清晰，天然继承的单表操作对应的sql语句，在一个很远的mappers文件夹里躺着，除非字段变化，否则不要去动它。而联表查询等操作的sql语句，则与Mapper.java放在同一个包下面。Mapper.java增减方法，这个Mapper.xml也要做相应修改。

附：`MybatisMapper`有12个方法，对应数据库的增删改查四个操作。

<table>
    <tr>
    <th>方法名</th><th>用途</th>
    </tr>
    <tr>
    <td>
    *新增（3）*
    </td>
    <td>
    </td>
    </tr>
    <tr>
    <td> insert(T model)</td>
    <td>直接插入单个的javaben，在数据库形成一条记录。</td>
    </tr>
    <tr>
    <td>insertPartitive(@Param("fields") PartitiveFields fields)</td>
    <td>向数据库插入一条记录，单仅设置fields参数中包含的列的值。</td>
    </tr>
    <tr>
    <td>
    *删除（2）*
    </td>
    <td>
    </td>
    </tr>
    <tr>
    <td> delete(Object... id)</td>
    <td>根据id删除数据库的记录,支持输入多个id（联合主键）。</td>
    </tr>
    <tr>
    <td>deleteBatch(Condition condition)</td>
    <td>根据条件从数据库删除多条记录。</td>
    </tr>
    <tr>
    <td>
    *修改（3）*
    </td>
    <td>
    </td>
    <tr>
    <td> update(T model)</td>
    <td>根据主键更新其它所有字段。</td>
    </tr>
    <tr>
    <td>updatePartitive(PartitiveFields fields, Object... id)</td>
    <td>根据主键更新指定的字段</td>
    </tr>
    <tr>
    <td>updateBatch(PartitiveFields fields,Condition condition)</td>
    <td>根据条件批量更新指定的字段</td>
    </tr>
    <tr>
    <td>
    *查询（4）*
    </td>
    <td>
    </td>
    <tr>
    <tr>
    <td>T read(Object... id)</td>
    <td>根据主键读出记录。</td>
    </tr>
    <tr>
    <td>int count(Condition condition)</td>
    <td>返回符合条件的记录数量</td>
    </tr>
    <tr>
    <td>List&lt;T> list(Condition condition)</td>
    <td>返回全部符合条件的记录列表</td>
    </tr>
    <tr>
    <td>List&lt;T> list(Condition condition,RowBounds rowBounds)</td>
    <td>返回rowBounds指定页码的符合条件的记录列表</td>
    </tr>
</tbale>


