# 增加stone依赖

在pom.xml文件中，增加如下依赖：

<table>
    <tr>
        <th>Group Id</th>
        <th>Artifact Id</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>org.siqisource</td>
        <td>stone</td>
        <td>stone依赖</td>
    </tr>
    <tr>
        <td>postgresql</td>
        <td>postgresql</td>
        <td>数据库驱动</td>
    </tr>
    <tr>
        <td>javax</td>
        <td>javaee-web-api</td>
        <td>provided，提供web容器的基本接口，如HttpServletRequest等</td>
    </tr>
    <tr>
        <td>javax.servlet</td>
        <td>jstl</td>
        <tds>provided，jstl支持</td>
    </tr>
    <tr>
        <td>taglibs</td>
        <td>standard</td>
        <tds>provided，标准标签库</td>
    </tr>
</table>
 
增加依赖后，在项目上右键->Maven->Update Project,点击OK后，可能会报关于jfaces的错误。此时关闭Eclipse，在资源管理器中打开项目目录，在`.settings`目录下面，删除文件名包含`jfaces`的两个文件，再启动Eclipse，重新Maven->Update Project,即可解决此问题。
