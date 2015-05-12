# 模块的包结构

从java的视角看，典型的stone风格的业务模块，基本的包名是：`groupId.artifactId.moduleId`。它下面包含的4个子包：`model`、`mapper`、`service`、`controller`。

他们及相关文件在业务系统中的位置大概如下图所示(以一个订单管理模块为例)：

```
src/main/java
    |-groupId
        |-artifactId
              |-moduldeId（order）
                    |-controller
                        |--OrderController.java
                        |--OrderForm.java
                    |-service
                        |--OrderConditionBuilder.java
                        |--OrderService.java
                    |-mapper
                        |--OrderMapper.java
                        |--OrderMapper.xml
                    |-model
                        |--Order.java
                        |--OrderView.java
src/main/resources
    |-mappers
        |--OrderMapper.xml
```



