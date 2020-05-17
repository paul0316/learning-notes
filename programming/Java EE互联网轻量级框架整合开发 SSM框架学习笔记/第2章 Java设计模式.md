# 第2章 Java设计模式

## 2.1 Java反射技术









### 2.1.1 通过反射构建对象

ReflectServiceImpl类

```java
public class ReflectServiceImpl {
    public void sayHello(String name) {
        System.out.println("Hello " + name);
    }
}
```



通过反射的方式构建实例对象

```java
public ReflectServiceImpl getInstance() {
    ReflectServiceImpl object = null;
    try {
        object = ()
    }
}
```











反射的优点是只要配置就可以生成对象，可以解除程序的耦合度，比较灵活。反射的缺点就是运行比较慢。但是大部分情况下为了灵活度，降低程序的耦合度，我们还是会使用反射的，比如Spring IoC容器。





### 2.1.2 反射方法













## 2.2 动态代理模式和责任链模式



动态代理意义在于生成一个占位（又称为代理对象），从而控制真实对象的访问。

什么是代理模式？

假设这样一个场景，你的公司是一家软件公司，你是一位软件工程师。客户带着需求去找公司显然不会直接和你谈，而是去找商务谈，此时客户会认为商务就代表公司。

![image-20200507105349223](https://tva1.sinaimg.cn/large/007S8ZIlgy1gejp63pleyj30e203sjsw.jpg)



在Java中有很多种代理技术，比如JDK、CGLIB、Javaassist、ASM，其中动态代理技术有两种：一种是JDK动态代理，这就JDK自带的功能；另一种是CGLIB，这是第三方提供的一个技术。目前，Spring常用的就是JDK和CGLIB，而MyBatis还使用了Javaassist。



### 2.2.1 JDK动态代理















### 2.2.2 CGLIB动态代理















### 2.2.3 拦截器









### 2.2.4 责任链模式











## 2.3 观察者（Observer）模式



### 2.3.1 概述





### 2.3.2 实例













## 2.4 工厂模式和抽象工厂模式







### 2.4.1 普通工厂模式











### 2.4.2 抽象工厂模式











## 2.5 建造者模式





### 2.5.1 概述





### 2.5.2 Builder模式实例



## 2.6 总结

动态代理和责任链模式是本章乃至全书的重点，很多框架的底层都是通过他们实现的，尤其是Spring和MyBatis，只有掌握好这些内容，才能真正理解Spring AOP和MyBatis的底层运行原理。

