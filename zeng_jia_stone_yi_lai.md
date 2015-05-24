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

我们将版本好统一写在properties中，用maven-compiler-plugin设置好编译的选项，最终的pom.xml文件内容如下：
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.siqisoft</groupId>
	<artifactId>hoterp</artifactId>
	<packaging>war</packaging>
	<version>0.0.1-SNAPSHOT</version>
	<name>hoterp Maven Webapp</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<sourceVersion>1.6</sourceVersion>
		<targetVersion>1.6</targetVersion>

		<!-- Build Dependency Version Properties -->
		<stone.version>1.0.5</stone.version>
		<javaee-web-api.version>6.0</javaee-web-api.version>
		<javax-jstl.version>1.1.2</javax-jstl.version>
		<taglibs-standard.version>1.1.2</taglibs-standard.version>
		<jdbc.postgresql.version>9.1-901.jdbc4</jdbc.postgresql.version>

		<!-- Plugin Dependency Version Properties -->
		<maven-compiler-plugin.version>2.3.2</maven-compiler-plugin.version>
	</properties>

	<dependencies>

		<dependency>
			<groupId>org.siqisource</groupId>
			<artifactId>stone</artifactId>
			<version>${stone.version}</version>
		</dependency>

		<dependency>
			<groupId>postgresql</groupId>
			<artifactId>postgresql</artifactId>
			<version>${jdbc.postgresql.version}</version>
		</dependency>

		<!-- jee -->
		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<scope>provided</scope>
			<version>${javaee-web-api.version}</version>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>${javax-jstl.version}</version>
		</dependency>
		<dependency>
			<groupId>taglibs</groupId>
			<artifactId>standard</artifactId>
			<version>${taglibs-standard.version}</version>
		</dependency>
	</dependencies>

	<build>
		<finalName>hoterp</finalName>

		<plugins>

			<!-- Compiler -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>${maven-compiler-plugin.version}</version>
				<configuration>
					<encoding>${sourceEncoding}</encoding>
					<source>${sourceVersion}</source>
					<target>${targetVersion}</target>
				</configuration>
			</plugin>
			
		</plugins>

	</build>
</project>

```
