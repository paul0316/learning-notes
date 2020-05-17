# 第4章 MyBatis 配置

## 4.1 概述



properties 属性

settings 设置

typeAliases 别名

typeHandlers 类型

objectFactory 对象工厂

plugins 插件

environments 运行环境

databaseProvider 数据库厂商标识







## 4.2 properties 属性



properties 属性可以给系统配置一些运行参数，可以放在 XML 文件或者 properties 文件中，而不是放在 Java 代码中，这样的好处是方便参数的修改，而不会引起代码的重新编译。一般而言，MaBatis提供了三种方式让我们使用 properties，它们是：

- property 子元素
- 使用 properties 文件
- 使用程序传递方式传递参数







### 4.2.1 property 子元素

















### 4.2.2 使用 properties 文件



jdbc.properties

```properties
database.driver=com.mysql.jdbc.Driver
database.url=jdbc:mysql://localhost:3306/ssm
database.username=root
database.password=password
```



在MyBatis中通过<properties>的属性 resource 来引入这个 properties 文件。

```xml
<properties resource="jdbc.properties"/>
```















### 4.2.3 程序代码传递参数





### 4.2.4 总结

推荐使用 properties 文件的方式











## 4.3 settings 设置

settings 是 MyBatis 中最复杂的配置，