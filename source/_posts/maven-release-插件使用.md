---
title: maven release 插件使用
tag:
  - java
  - maven
categories:
  - java
date: 2017-03-19 20:57:08
---

关于release与snapshot的区别这里不再赘述，maven项目在生产环境部署的时候一定是需要打release包的。

<!-- more -->


关于release与snapshot的区别这里不再赘述，maven项目在生产环境部署的时候一定是需要打release包的。

 [maven-release-plugin](http://maven.apache.org/maven-release/maven-release-plugin/) 可用于构建release版本项目，实现自动打tag、递增版本号、分发release版本jar包至仓库。

pom.xml配置：

``` 
<!--git 远程仓库配置-->
<scm>
        <connection>scm:git:http://项目git地址</connection>
        <url>项目git地址（不加'.git后缀'）</url>
        <developerConnection>scm:项目git地址</developerConnection>
 </scm>

 <!--构建配置-->
 <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-release-plugin</artifactId>
                <version>2.5.3</version>
                <configuration>
                    <tagNameFormat>v@{project.version}</tagNameFormat>
                    <autoVersionSubmodules>true</autoVersionSubmodules>
                </configuration>
            </plugin>
        </plugins>
    </build>
   
    <!--分发配置-->
    <distributionManagement>
        <repository>
            <id>deploymentRepo</id>
            <name>releases</name>
            <url>http://somehost/repository/maven-releases/</url>
            <uniqueVersion>true</uniqueVersion>
        </repository>
        <snapshotRepository>
            <id>deploymentRepo</id>
            <name>snapshots</name>
            <url>http://somehost/repository/maven-snapshots/</url>
            <uniqueVersion>true</uniqueVersion>
        </snapshotRepository>
    </distributionManagement>
```
由于会将构建的包分发到仓库，需要在maven的配置文件setting.xml下加入权限配置：
```
    <server>
      <id>your id</id>
      <username>your username</username>
      <password>your pass</password>
    </server>
```

这里最关键的一点是scm节点配置，无论项目是使用git、svn或是其他版本控制工具，都可以在这里配置，详细的配置可参考[scms-overview](http://maven.apache.org/scm/scms-overview.html)。

下面是一个项目配置示例：
```
   <scm>
        <connection>scm:git:http://git-local.bnz.com/srv/bnz-ep.git</connection>
        <url>http://git-local.bnz.com/srv/bnz-ep</url>
        <developerConnection>scm:git:http://git-local.bnz.com/srv/bnz-ep.git</developerConnection>
    </scm>
```

如果需要跳过单元测试，可以加入参数 `-Darguments="-DskipTests"`，直接使用`-Dmaven.test.skip=true`是**无效**的。

在执行`mvn release:perform`时默认会生成api文档，如果默写注释不符合规范的话会造成构建失败，可以加参数`-DuseReleaseProfile=false`取消构建api文档，或则需要根据规范书写注释。
```
mvn release:prepare
mvn release:perform
```

如果在构建过程中出现错误，rollback回滚即可
```
mvn release:rollback
```



