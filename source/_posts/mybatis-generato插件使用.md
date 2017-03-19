---
title: mybatis-generator 插件使用
tag:
  - java
  - mybatis-generator
  - mbg
categories:
  - java
date: 2017-03-19 20:55:46
---

mybaits在业务系统中的使用很广泛，mybatis-generator就是一款是实用的插件用来生成model和mapper。

<!-- more -->

mybaits在业务系统中的使用很广泛，mybatis-generator就是一款是实用的插件用来生成model和mapper。

## maven插件配置
pom.xml文件配置：
```
<dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.0</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.5</version>
                <configuration>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

## mybatis-generator 配置

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!-- 配置文件，放在resource目录下即可 -->
    <properties resource="generator.properties"></properties>
    <!--数据库驱动lib放在根目录下 -->
    <classPathEntry location="lib/mysql-connector-java-5.1.9.jar"/>
    <context id="MysqlTables" targetRuntime="MyBatis3">
        <property name="autoDelimitKeywords" value="true"/>
        <!--可以使用``包括字段名，避免字段名与sql保留字冲突报错-->
        <property name="beginningDelimiter" value="`"/>
        <property name="endingDelimiter" value="`"/>
        <commentGenerator>
            <property name="suppressDate" value="true"/>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>
        <!--数据库链接地址账号密码-->
        <jdbcConnection driverClass="${jdbc.driverClass}" connectionURL="${jdbc.connectionURL}" userId="${jdbc.userId}"
                        password="${jdbc.password}">
        </jdbcConnection>
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>
        <!--生成Model类存放位置-->
        <javaModelGenerator targetPackage="com.bangnizhao.bzep.model" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!--生成映射文件存放位置-->
        <sqlMapGenerator targetPackage="mapping" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!--生成Dao类存放位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.bangnizhao.bzep.mapper" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!--生成对应表及类名 -->
        <table tableName="t_user_info" domainObjectName="UserInfo" enableCountByExample="true"
               enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true"
               selectByExampleQueryId="true">
           <!--mysql 下可取插入的自增型id-->
            <generatedKey column="id" sqlStatement="SELECT LAST_INSERT_ID()" identity="true" type="post"/>
        </table>
        <table tableName="t_user_login_his" domainObjectName="UserLoginHistory" enableCountByExample="true"
               enableUpdateByExample="true" enableDeleteByExample="true" enableSelectByExample="true"
               selectByExampleQueryId="true">
            <generatedKey column="seri_id" sqlStatement="SELECT LAST_INSERT_ID()" identity="true" type="post"/>
        </table>
    </context>
</generatorConfiguration>
```
enableXXXExample 是一个很有用的配置，可以帮助生成基本的增删查（包含统计）改接口，其中查询接口是非常强大的。然而这些查询仅限于单表查询，其实单表查询的情况比例是非常大的，实在需要级联查询、特殊查询的时候可以再单独写sql。

### 条件查询示例

```
//根据手机号码查询用户
public UserInfo getByPhoneNo(String phoneNo) {
        UserInfoExample userInfoExample = new UserInfoExample();
        userInfoExample.createCriteria()
                .andUserPhoneEqualTo(phoneNo);
        List<UserInfo> userInfos = userInfoMapper.selectByExample(userInfoExample);
        return SaftyListUtil.getFirst(userInfos);
    }
```
### 条件更新示例
```
//更新某个人的所有消息状态
@Transactional
    public void updateStatusByUserId(int userId, MessageStatus newStatus, MessageStatus oldStatus) {
        MessageInfoDetailExample messageInfoDetailExample = new MessageInfoDetailExample();
        messageInfoDetailExample.createCriteria()
                .andReceiverUserIdEqualTo(userId)
                .andStatusEqualTo(oldStatus.getCode());
        MessageInfoDetail messageInfoDetail = new MessageInfoDetail();
        messageInfoDetail.setStatus(newStatus.getCode());
        messageInfoDetailMapper.updateByExampleSelective(messageInfoDetail, messageInfoDetailExample);
    }
```

## 运行插件

如果需要覆盖之前生成的类和mapper，需要加入参数`-Dmybatis.generator.overwrite=true`，遗憾的是，1.3.5版本时mapper文件只能追加，不能覆盖。所以在运行之前需要手动删除mapper。做个脚本就可解决，详见附录。

```
mvn -Dmybatis.generator.overwrite=true mybatis-generator:generate
```

## 附录

window下bat：
```
RMDIR src\main\resources\mapping /s/q
mvn -Dmybatis.generator.overwrite=true mybatis-generator:generate
```

shell:
```
DIR="src/main/resource/mapping" 
if [ -e  "$DIR" ]  
then
  rm -rf $DIR
  echo "delete mappig dir"
else
  echo "no mapping dir"
fi
mvn -Dmybatis.generator.overwrite=true mybatis-generator:generate
```

