# 第一章 认识SSM框架和Redis

## 1.1 Spring框架

IOC（Inversion of Control，控制反转）

AOP（Aspect Oriented Programming，面向切面编程）

### 1.1.1 Spring IoC简介

JavaBean的创建、事件、行为等，由IoC容器管理。Java Bean之间会存在一定的依赖关系，比如班级是由老师和学生组成的。假设老师和学生都是Java Bean，那么他们之间是存在依赖关系的。Spring IoC管理对象和依赖关系，采用的不是人为的主动创建，而是由Spring IoC自己通过描述创建的，也就是说Spring是依靠描述来完成对象的创建和其依赖关系的。



```xml
<bean id="socket" class="socket1"/>
<bean id="user" class="xxx.User">
	<property name="socket" ref="socket"/>
</bean>
```



```xml
<bean id="socket" class="socket2"/>
```





### 1.1.2 Spring AOP

IoC的目标是为了管理Bean，而Bean是Java面向对象的基础设计，比如声明一个用户类、插座类都是基于面向对象的概念。

SpringAOP常用于处理事务的编程，我们做完第一步数据库更新，不知道下一步是否会成功，如果在下一步失败，会使用数据库事务的回滚功能去回滚事务，使得第一步的数据库更新也作废。

```java
/*
Spring AOP处理订单伪代码
*/
private void proceed(Order order) {
    // 判断生产部门是否通过订单，数据库记录订单
    boolean pflag = productionDept.isPass(order);
    if (pflag) { // 如果生产部门通过进行财务部门审批
        if (financialDept.isOverBudget(order)) {
            // 抛出异常回滚事务，之前的订单操作也会被回滚
            throws new RuntimeException("预算超支！")
        }
    }
}
```

只要知道发生的异常。Spring就会回滚事务即可。







## 1.2 MyBatis简介

MyBatis的前身是Apache的开源项目iBatis。是一个基于Java的**持久层框架**。

MyBatis的优势在于灵活，他几乎可以替代JDBC，同时提供接口编程。目前MyBatis的数据访问层DAO（Data Access Object）是不需要实现类的，他只需要一个接口和XML（或者注解）。





MyBatis的Hibernate的区别？

他们都是持久层框架，都会涉及数据库。必须有一张数据库表。

定义角色 POJO（Plain Ordinary Java Object）

```java
public class Role implements java.io.Serializable {
    private Integer id;
    private String roleName;
    private String note;
    /* setter and getter */
}
```







### 1.2.1 Hibernate简介

要将POJO和数据库映射起来需要给这些框架提供映射规则。



![image-20200507090258265](https://tva1.sinaimg.cn/large/007S8ZIlgy1gejlyrvvbnj30c005fwg9.jpg)

通过XML和注解提供映射规则，这里先将XML方式，因为在MyBatis中注解方式会受到一定的限制。

我们把POJO对象和数据库相互映射的框架称为对象关系映射（ORM，Object Relational Mapping）框架。Hibernate是全自动框架，基本不需要编写SQL就可以通过映射关系来操作数据库，是一种全表映射的体现；而MyBatis不是，需要我们提供SQL去运行。





### 1.2.2 MyBatis

不屏蔽SQL的优势在于，程序员 可以自定义SQL规则，无需Hibernate自动生成规则，这样能够更加精确地定义SQL。从而优化性能，更加符合互联网高并发、大数据、高性能、高响应的要求。

resultMap用于定义映射规则

```java
<? xml version ＝ ” 1. 。 ” encoding＝ ” UTF-8 ” ？〉 < !DOCTYPE mapper PUBLIC ”－ ／／ mybat 工s . org//DTD Mapper 3 . 0//EN ” http: //mybatis .org/dtd/mybatis- 3-mapper . dtd" >

”

<mapper namespace =” com.learn . chapterl .mapper . RoleMapper ” > <resultMap id =” roleMap " type =” com . learn . chapterl.pojo . Role ” > <id property =” id ” column =” id ” /> <result property =” r oleName ” column =” r ole_name ” /> <result property =” note ” column =” note ”/> </resultMap>

<select id =” getRole ” resultMap select id, role name , note </select>

=” roleMap ” > from t role where id =

＃｛工 d}

<delete id =” deleteRole " parameterType delete from t role where id = #{id} </delete>

=” int ”>

<insert id =” insertRole ” parameterType =” com .learn . chapterl.pojo.Ro le ” > insert into t role(role name , note) values(#{roleName } , #{note}) </insert>

<update id =” updateRole ” parameterType =” com.learn update t role set role name= #{roleName}, note = #{note} where id = #{id} </update> </mapper>
```

增删改查对应四个元素，insert、delete、update、select。

**注意，mapper元素中的namespace属性，他要和一个接口的全限定名保持一致，而里面的SQL的id也需要和接口定义的方法完全保持一致。**

定义MyBatis映射文件

```java
package com.chapter1.mapper;
inport com.learn.chapter1.pojo.Role;

public interface RoleMapper {
    public Role getRole(Integer id);
    public int deleteRole(Integer id);
    public int insertRole(Role role);
    public int updateRole(Role role);
}
```

定义了MyBatis映射文件，但是不需要定义一个实现类。

```java
SqlSession sqlSession = null;
try {
    sqlSession = MyBatisUtil.getSqlSession();
    RoleMapper roleMapper = sqlSession.getMapper(RoleMapper.class);
} catch (Exception ex) {
    ex
} finally {
    if (sqlSession != null) {
        sqlSession.close();
    }
}
```



### 1.2.3 Hibernate 和 MyBatis 的区别



















## 1.3 SpringMVC简介

长期以来Struts2和Spring的结合一直存在很多问题，比如兼容性和类臃肿。



MVC模式把应用程序（输入逻辑、业务逻辑和UI逻辑）分为了不同的方面，同时提供这些元素之间的松耦合。

- Model（模型），封装了应用程序的数据和由它们组成的POJO。
- View（视图），负责把模型数据渲染到视图上，将数据以一定形式展现给用户。
- Controller（控制器），负责处理用户请求，并建立适当的模型把它传递给视图渲染。

















## 1.4 最流行的NoSQL——Redis

当前最流行的NoSQL。



![image-20200507093524171](https://tva1.sinaimg.cn/large/007S8ZIlgy1gejmwnge46j30ey07xmxo.jpg)



- 响应快速
- 支持6种数据类型
- 操作都是原子的
- MultiUtility







## 1.5 SSM+Redis结构框图及概述

Spring+SpringMVC+MyBatis（SSM）作为主流框架，SSM+Redis的结构框图。

![image-20200507093829708](https://tva1.sinaimg.cn/large/007S8ZIlgy1gejmzq8648j30hs0a779m.jpg)

各个组件的功能

- Spring IoC承担了一个资源管理、整合、即插即拔的功能。
- Spring AOP可以提供切面管理，特别是数据库事务管理的功能。
- Spring MVC用于把模型、视图和控制器分层，组成一个有机灵活的系统。
- MyBatis提供了一个数据库访问的持久层，通过MyBatis-Spring项目，它便能和Spring无缝连接。
- Redis作为缓存工具，他提供了高速度处理数据和缓存数据的功能，使得系统大部分只需要访问缓存。而无需从数据库磁盘中重复读/写；在一些需要高速运算的场合中，也可以先用它来完成运算，再把数据批量存入数据库，这些便能极大地提升互联网系统的性能和响应能力。

