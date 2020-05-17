# MyBatis 的解析和运行原理

MyBatis 的运行过程大致分为两大步：第一步，读取配置文件缓存到 Configuration 对象，用以创建 SqlSessionFactory；第二步，SqlSession 的执行过程。



## 7.1 构建 SqlSessionFactory 过程

SqlSessionFactory 是 MyBatis 的核心类之一，最重要的功能就是提供创建 MyBatis 的核心接口 SqlSession。采用 Builder 模式创建 SqlSessionFactory。

第一步：

第二步：

