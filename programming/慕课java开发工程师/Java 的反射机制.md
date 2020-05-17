## Java 的反射机制

### 概述

**什么是 Java 的反射机制？**

Java 的反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能成为 Java 语言的反射机制。



.java 文件被编译为 .class 文件，类加载器 ClassLoader 加载 .class 文件进内存。

![Java 的反射机制](https://tva1.sinaimg.cn/large/007S8ZIlgy1gevmuq6f61j310508xaan.jpg)



**Java 的反射机制的作用**

用来编写一些通用性较高的代码或者框架的时候使用。





### 反射的 API

- Class 类

Class 类的实例表示正在运行的 Java 应用程序中的类和接口

- Constructor 类

关于类的单个构造方法的信息以及对它的访问权限

- Field 类

Field 提供有关类或接口的单个字段的信息，以及对它的动态访问权限

- Method 类

Method 提供关于类或接口上单独某个方法的信息

![image-20200517122809771](https://tva1.sinaimg.cn/large/007S8ZIlgy1gevc3cexo6j30w60ergom.jpg)



### Class 类

Java 中 java.lang.Class 类用于表示一个类的字节码（.class）文件



如何得到某个 class 文件对于的 Class 对象

- 已知类和对象的情况下

  类名.class

  对象.getClass() ---- Object 类提供

- 未知类和对象的情况下

  Class.forName("包名.类名")



Class 类代表某个类的字节码，并提供了加载字节码的方法：forName("包名.类名")，forName 方法用于加载类字节码到内存中并封装成一个 Class 对象





### Constructor 类

Constructor 类的实例对象代表类的一个构造方法



- 得到某个类的所有的构造方法

```java
Constructor[] constructor = class.forName("java.lang.String").getConstructor();
```



- 得到指定的构造方法并调用

```java
Constructor[] constructor = class.forName("java.lang.String").getConstructor(String.class);
String str = (String)constructor.newInstance("abc");
```



- Class 类的 newInstance() 方法用来调用类的默认构造方法

```java
String obj = (String)Class.forName("java.lang.String").newInstance();
```





## Field 类

Filed 类代表某个类中的一个成员变量，并提供动态的访问权限

- Field 对象的获得

```java
// 得到所有的成员变量
Field[] fields = clz.getFields(); // 获取所有的 public 属性（包括父类继承）
Field[] fields = clz.getDeclaredFields(); // 获取所有声明的属性

// 得到指定的成员变量
Field name = clz.getField("name");
Field name = clz.getDeclaredField("name");
```



- 设置 Field 变量是否可以访问

```java
field.setAccessible(boolean);
```



- Field 变量值的读取和设置

```java
field.get(obj);
field.set(obj.value);
```





## Method 类

- Method 类代表某个类中的一个成员方法
- Method 对象的获得

```java
// 获取所有方法 
getDeclaredMethods();
getMethod();

// 获取指定的方法
getDeclaredMethod(String name, Class<?>...parameterTypes);
getMethod(String name, Class<?>...parameterTypes);
```



- 通过反射执行方法

```java
invoke(Object obj, Object...args);
```

