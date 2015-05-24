# 配置stone-sdk

stone仅仅是一个jar包，为基于stone的项目在运行时提供各种功能。

在开发和运维过程中，我们还希望能有一些工具，䏻帮助我们快速开发和配置。于是，和stone搭配的，还有一套stone development kit（下文简称stone-sdk）工具集。

stone-sdk是一个webapp，以war包的方式发布在maven仓库中。我们可以利用tomcat-maven插件，将这个war和我们要开发的应用部署到一起，便于我们使用。

那么，我们最终的pom文件将如下所示：

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
		<tomcat7-maven-plugin.version>2.0</tomcat7-maven-plugin.version>
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

			<!-- Tomcat7 -->
			<plugin>
				<groupId>org.apache.tomcat.maven</groupId>
				<artifactId>tomcat7-maven-plugin</artifactId>
				<version>${tomcat7-maven-plugin.version}</version>
				<configuration>
					<port>3234</port>
					<path>/hoterp</path>
					<uriEncoding>UTF-8</uriEncoding>
					<contextFile>${basedir}/tomcat-context.xml</contextFile>
					<webapps>
						<webapp>
							<groupId>org.siqisource</groupId>
							<artifactId>stone-sdk</artifactId>
							<version>${stone.version}</version>
							<type>war</type>
							<asWebapp>true</asWebapp>
						</webapp>
					</webapps>
				</configuration>
			</plugin>
		</plugins>

	</build>
</project>

```

我们注意到在tomcat-maven插件中增加了stone-sdk依赖，它的type是war。

我们还注意到，在tomcat-maven插件上，增加了一个contextFile配置，指向了项目根目录下的tomcat-context.xml文件，这个文件用于配置数据源。

通常情况下，一个web应用的数据源要么是应用自身维护，要么是容器通过jndi方式提供。我们在stone开发过程中，优先使用容器数据源，让tomcat帮助我们管理数据源。通过tomcat-context.xml，我们把之前准备的数据库和我们创建的webapp项目关联起来：
```
<?xml version='1.0' encoding='utf-8'?>
<Context>
	<Resource name="jdbc/hoterp" global="jdbc/hoterp" auth="Container"
		type="javax.sql.DataSource" driverClassName="org.postgresql.Driver"
		url="jdbc:postgresql://127.0.0.1:5432/hoterp" username="hoterp"
		password="hoterp" maxActive="100" maxIdle="20" minIdle="5" maxWait="10000" />
</Context>
```