# mapper包

mapper包用来存放数据库基本操作的接口，它们都继承自`org.siqisource.stone.orm.MybatisMapper<T>`接口,其中T代表的数据库表对应的`model`类。

`MybatisMapper`有13个方法，对应数据库的增删改查四个操作。

**新增(3)：**
<table>
    <tr>
    <th>方法名</th><th>用途</th>
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
</tbale>

**删除(2)：**
<table>
    <tr>
    <th>方法名</th><th>用途</th>
    </tr>
    <tr>
    <td> delete(Object... id)</td>
    <td>根据id删除数据库的记录,支持输入多个id（联合主键）。</td>
    </tr>
    <tr>
    <td>deleteBatch(Condition condition)</td>
    <td>根据条件从数据库删除多条记录。</td>
    </tr>
</tbale>

**修改(3)：**
<table>
    <tr>
    <th>方法名</th><th>用途</th>
    </tr>
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
</tbale>


