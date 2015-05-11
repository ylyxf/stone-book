# 模块的包结构

从java的视角看，stone的每个业务模块，基本的包名是：`groupId.artifactId.moduleId`。它下面包含的4个子包：`model`、`mapper`、`service`、`controller`。

**model**：这个包里面放两种javabean：一种是和数据库表的字段一一对应的类，另一种是因为表现层的需要，拼凑出来的视图层面的javabean。

第一种情况，举个例子：有个user表，里面有4个字段：id、account、first_name、second_name。那么它对应的bean类，就有4个属性：id、account、firstName、secondName。它的主要作用，是在单表操作时，配合read、update、insert几个方法，作为参数传给mybatis框架，或者作为结果，由mybatis框架返回。

有个特殊情况，如果业务上有需要，可以给这种bean加List属性，用来装载一对多情况下多的部分。比如：一个用户对应多个订单，那么，除了上述的4个属性，还可以多加一个属性：```List<Order> orderList```。

第二种情况，举个例子：在数据库设计上，有个订单表，订单表上记录了客户Id、供应商Id。而在订单的列表上，需要显示客户名、供应商名。

它对应的sql语句可能是这样的：

```
select order.* , client.name as client_name ,supplier.name as supplier_name from order,client,supplier where order.client_id = client.id and order.supplier_id = supplier.id;
```

此时，可以继承订单类，写一个因为表现层显示需要而定义的类：OrderView:

```
public OrderView extends Order {

    private String clientName;
    
    private String supplierName;

}
```
它主要是用于在联表查询时，配合mybatis框架装载list的返回值。


***命名规则提醒***：上面的例子虽是虚拟，但是命名规则是真实的，我们通过上面的例子来归纳一下，在stone中的命名规则:
1. 数据库的表名、字段名都是小写的英文单词，不要用拼音，更不要用拼音的首写字母。数据库的表、字段名，如果有多个单词，请用下划线分开。
2. java的属性名，使用首字母小写的驼峰表示法命名。如果属性是复数，一般后缀加List，而不是加s或者es，因为好多英语不好的人（包括作者），分不清什么时候该加s，什么时候加es。
3. 设计表的时候，字段名里不要再重复表名：如客户表，叫client，那么表里的字段客户名，不要叫client_name,直接叫name。但是在关联查询的时候，需要起个别名，让人能识别出来它是client_name而不是别的什么name。


