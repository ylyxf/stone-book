# 增加tomcat-maven插件

我们在Eclipse中编写的代码，需要在web容器中运行，以验证代码写得对不对。如果有错误，还需要Eclipse和web容器结合工作，在Eclipse中增加断点，进行调试。

tomcat提供了一个maven插件，帮助我们结合maven在开发中进行调试。我们在pomx中引入tomcat的maven插件，然后在Eclipse中进行调用maven的插件，启动tomcat，完成开发中的验证与调试工作。

在pom中增加插件，代码如下：

在Eclipse中，启动tomcat的maven插件：

