# mapper包

mapper包用来存放数据库操作的接口，这些接口都应继承自`org.siqisource.stone.orm.MybatisMapper<T>`,其中T代表的数据库表对应的`model`类。mapper包只存放接口，不需要写实现类，但是要在mapper接口对应的mapper.xml配置文件中，写上12条sql语句，以使其支持从`MybatisMapper`继承来的12个方法。
这个写了12条sql语句的mapper.xml文件，应该放在项目的`src/main/resources/mappers`目录下，我们在写完后一般不要去改动它。

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
    <td>insertBatch(List&lt;T> models)</td>
    <td>向数据库批量插入多条记录。</td>
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


