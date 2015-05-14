# 各层的调用关系

stone的业务模块调用关系是：浏览器请求->controller->service->mapper->数据库。
model极其子类贯穿调用过程，作为参数携带数据，最终将浏览器的请求传递到数据库，并并携带数据库的数据返回给浏览器

跨模块调用一般发生在service层面，Controller类仅包含本模块的Service，然后在Service类中，@autoWired其它模块的Service类作为成员变量。这样便于更好地在Service层面控制事务。

较常见的特殊情况是，在Controller层会包含`org.siqisource.stone.security.service.SecurityService`，它一般用于获得当前用户或者构建带有授权信息的查询条件。
