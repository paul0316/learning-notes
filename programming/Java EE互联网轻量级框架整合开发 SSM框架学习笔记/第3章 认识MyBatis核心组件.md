# 第3章 认识MyBatis核心组件

## 3.1 持久层的概念和 MyBatis的特点

持久层可以将业务数据存储到硬盘上，具有长期存储能力，只要磁盘不损坏，在断电和其他情况下，重新开启系统仍然可以读取这些数据。一般执行持久任务的都是数据库系统，持久层可以使用巨大的磁盘空间，也比较廉价，它的缺点就是比较慢。这在一般的系统里是没有问题，但是针对互联网的秒杀情况下，每秒都要执行成千上万次的数据操作，这就不能忍受了，极大可能会宕机。在这种情况下，我们可以使用Redis处理它。

![image-20200507153804742](https://tva1.sinaimg.cn/large/007S8ZIlgy1gejxdy7h84j30da06lq5d.jpg)

MyBatis最大的优点：

- 不屏蔽SQL，意味着可以更为精确地定位SQL语句，可以对其进行优化和改造，这有利于互联网系统性能的提高，符合互联网需要性能优化的特点。
- 提供强大、灵活的映射机制，方便Java开发者使用。
- 在MyBatis中，提供了使用Mapper的接口编程，只要一个接口和一个XML文件就能创建映射器，进一步简化我们的工作，使得很多框架API在MyBatis中消失，开发者更能集中于业务逻辑。





## 3.2 准备MyBatis环境

https://github.com/mybatis/mybatis-3/releases

下载MyBatis所需要的包和源码







## 3.3 MyBatis的核心组件

- SqlSessionFactoryBuilder（构造器）：它会根据配置或者代码来生成SqlSessionFactory，采用的是分步构建的Builder模式。
- SqlSessionFactory（工厂接口）：依靠它来生成SqlSession，使用的是工厂模式。
- SqlSession（会话）：一个既可以发送SQL执行返回结果，也可以获取Mapper的接口。在现有的技术中，一般我们会让其在业务逻辑代码中“消失”，而使用的是MyBatis提供的SQL Mapper接口编程技术，它能提高代码的可读性和可维护性。
- SQL Mapper（映射器）：MyBatis新设计存在的组件，它是由一个Java接口和XML文件（或者注解）构成，需要给出对应的SQL和映射规则。它负责发送SQL去执行，并返回结果。

![image-20200507175830637](https://tva1.sinaimg.cn/large/007S8ZIlgy1gek1fzjhzgj308p0a0dih.jpg)

无论是映射器还是SqlSession都可以发送SQL到数据库执行。





## 3.4 SqlSessionFactory

在MyBatis中， 既可以通过读取配置的XML文件的形式生成 SqlSessionFactory，也可以通过Java代码的形式去生成SqlSessionFactory。推荐使用XML的形式，因为代码的方式在需要修改的时候会比较麻烦。

SqlSessionFactory的唯一作用就是生产MyBatis的核心接口对象SqlSession，所以它的责任是唯一的。



### 3.4.1 使用XML构建SqlSessionFactory

在MyBatis中，XML分为两大类，一类是基础配置文件，通常只有一个，主要是配置一些最基本的上下文参数和运行环境；另一类是映射文件，它可以配置映射文件、SQL、参数等信息。

mybatis-config.xml

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <!-- 数据库环境 -->
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/ssm"/>
        <property name="username" value="root"/>
        <property name="password" value="password"/>
      </dataSource>
    </environment>
  </environments>
  
  <!-- 映射文件 -->
  <mappers>
    <mapper resource="com/learn/ssm/chapter3/mapper/RoleMapper.xml"/>
  </mappers>
</configuration>
```



通过XML构建SqlSessionFactory

```java
SqlSessionFactory sqlSessionFactory = null;
// 读取mybatis-config.xml文件
String resource = "mybatis-config.xml";
InputSteam inputStream;
try {
    inputStream = Resource.getResourceAsStream(resource);
    SqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
} catch (IOException e) {
	e.printStackTrace();
}
```







### 3.4.2 使用代码创建SqlSessionFactory













## 3.5 SqlSession

在MyBatis中，SqlSession是其核心接口。

- 获取Mapper接口
- 发送SQL给数据库
- 控制数据库事务

```java
SqlSession sqlSession = sqlSessionFactory.openSession();
```



```java
// 定义SqlSession
SqlSession sqlSession = null;
try {
    // 打开SqlSession会话
    sqlSession = SqlSessionFactory.openSession();
    // some code...
    sqlSession.commit(); // 提交事务
} catch (Exception ex) {
    sqlSession.rollback(); // 回滚事务
} finally {
    if (sqlSession != null) {
        sqlSession.close();
    }
}
```







## 3.6 映射器

映射器是MaBatis中最重要、最复杂的组件，他由一个接口和对应的XML文件（或者注解）组成。它可以配置以下内容：

- 描述映射规则。
- 提供失去了语句，并可以配置SQL参数类型，返回类型、缓存刷新等信息。
- 配置缓存。
- 提供动态SQL。

先定义一个POJO

```java
package com.learn.ssm.chapter3.pojo;
public class Role {
    private Long id;
    private String roleName;
    private String note;
    /** setter and getter **/
}
```

映射器的作用就是将SQL查询到的结果映射为一个POJO，或者将POJO的数据插入到数据库中，并定义一些关于缓存等的重要内容。

MyBatis使用了动态代理技术让接口能够运行，我们现在只需要知道MyBatis会为这个接口生成一个代理对象，代理对象会去处理相关的逻辑。





### 3.6.1 用XML实现映射器

两部分：接口和XML

接口

```java
package com.learn.ssm.chapter3.mapper;
public interface RoleMapper {
    public Role getRole(Long id);
}
```





```java

```









### 3.6.3 SqlSession 发送 SQL





















### 3.6.4 用 Mapper 接口发送 SQL











### 3.6.5 对比两种发送 SQL 方式

















## 3.7 生命周期



















