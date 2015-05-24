# 使用stone-sdk

通过前文的配置，已经将stone-sdk与我们的hoterp项目结合起来。我们再次启动tomcat，访问`http://localhost:3234/stone-sdk`,通过容器数据源，初始化数据库，设置完管理员密码后，停止tomcat，再次启动tomcat，再次访问`http://localhost:3234/stone-sdk`，将会显示登录界面。