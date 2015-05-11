# 模块的包结构

从java的视角看，stone的每个业务模块，基本的包名是：`groupId.artifactId.moduleId`。它下面包含的4个子包：`model`、`mapper`、`service`、`controller`。

**model**：这个包里面放两种javabean：一种是和数据库表的字段一一对应的类，另一种是因为表现层的需要，拼凑出来的视图层面的javabean。

第一种情况，举个例子：有个user表，里面有4个字段：id、account、first_name、second_name。那么它对应的bean类，就有4个属性：id、account、firstName、secondName。它的主要作用，是在单表操作时，配合read、update、insert几个方法，作为参数传给mybatis框架，或者作为结果，由mybatis框架返回。

有个特殊情况，如果业务上有需要，可以给这种bean加List属性，用来装载一对多情况下多的部分。比如：一个用户对应多个订单，那么，除了上述的4个属性，还可以多加一个属性：```List<Order> orderList```。



