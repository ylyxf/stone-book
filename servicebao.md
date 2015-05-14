# service包

service包里面也装了两种类型的文件，一种是以`ConditionBuilder`结尾的java类，一种是以`Service`结尾的java类。

ConditonBuilder类的主要作用是构造Condition类，Condition类主要装载了数据库sql语句的查询条件，我们后文细说。

`Service`类都继承自`org.siqisource.stone.service.AbstractService<T>`，其中T是指模块的model，它包含18个数据库操作方法。

附：`AbstractService`的方法清单，对应数据库的增删改查四个操作。

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
    *删除（6）*
    </td>
    <td>
    </td>
    </tr>
    <tr>
    <td> delete(Object... id)</td>
    <td>根据id删除数据库的记录,支持输入多个id（联合主键）。</td>
    </tr>
    <tr>
    <td>deleteBatch(Object[] idList)</td>
    <td>根据主键id从数据库删除多条记录，仅支持单主键的情况。</td>
    </tr>
    <tr>
    <td>deleteBatch(Condition condition)</td>
    <td>根据条件从数据库删除多条记录。</td>
    </tr>
    <tr>
    <td>logicDelete(Object... id)</td>
    <td>根据id进行逻辑删除，本质是将表的logic_deleted字段设置为true。</td>
    </tr>
    <tr>
    <td>logicDeleteBatch(Condition condition) </td>
    <td>根据条件进行逻辑删除，本质是将表的logic_deleted字段设置为true。</td>
    </tr>
    <tr>
    <td>logicDeleteBatch(Object[] idList)</td>
    <td>根据id数组进行逻辑删除，本质是将表的logic_deleted字段设置为true。仅支持单主键的表</td>
    </tr>
    <tr>
    <td>
    *修改（4）*
    </td>
    <td>
    </td>
    <tr>
    <td> update(T model)</td>
    <td>根据主键更新其它所有字段。</td>
    </tr>
     <tr>
    <td> updateBatch(List&lt;T> models)</td>
    <td>根据主键更新每一个model的其它所有字段。</td>
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
    *查询（5）*
    </td>
    <td>
    </td>
    <tr>
    <tr>
    <td>T read(Object... id)</td>
    <td>根据主键读出记录。</td>
    </tr>
    <tr>
    <td>T read(Condition condition)</td>
    <td>根据条件读出一条记录。</td>
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
