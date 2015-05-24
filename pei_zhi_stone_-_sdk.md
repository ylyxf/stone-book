# 配置stone-sdk

stone仅仅是一个jar包，为基于stone的项目在运行时提供各种功能。

在开发和运维过程中，我们还希望能有一些工具，䏻帮助我们快速开发。于是，和stone配套的，还有一套stone development kit（下文简称stone-sdk），它是一个webapp，以war包的方式对外发布。我们可以利用tomcat-maven插件，将这个war和我们要开发的应用部署到一起，便于我们使用。