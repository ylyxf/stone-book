# 搭建开发环境

在了解了老板的需求后，我们首先要搭建一个基本的开发环境。

基本的步骤是：
1. 准备好pgsql数据库。
2. 通过Eclipse创建一个普通的maven结构的web项目。
3. 在项目的pom.xml文件中增加stone依赖。
4. 在Eclipse中运行该项目，通过浏览器查看stone提供的功能。

通过上述描述，我们能看出来，我们使用Eclipse开发，使用maven做依赖管理，通过tomcat的maven插件来进行开发调试。