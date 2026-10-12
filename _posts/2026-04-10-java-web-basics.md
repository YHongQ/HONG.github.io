---
layout: single
title: "JAVA WEB 基础"
date: 2026-04-10
categories: ["学习笔记"]
tags: ["Java", "Java Web", "三层架构", "IOC", "DI", "AOP", "数据库连接池", "Mybatis", "JWT", "事务管理", "Lombok"]
description: "JAVA WEB 基础知识，参考黑马程序员。"
---

## JAVA WEB

### 1. 三层架构
![alt text](/assets/images/posts/java-web-basics/image.webp)
![alt text](/assets/images/posts/java-web-basics/image-1.webp)

### 2. 分层解耦
![alt text](/assets/images/posts/java-web-basics/image-2.webp)
![alt text](/assets/images/posts/java-web-basics/image-3.webp)

1. IOC(控制反转)
![alt text](/assets/images/posts/java-web-basics/image-5.webp)
![alt text](/assets/images/posts/java-web-basics/image-6.webp)

2. DI(依赖注入)
![alt text](/assets/images/posts/java-web-basics/image-9.webp)

![alt text](/assets/images/posts/java-web-basics/image-10.webp)


### 3. 数据库连接池

![alt text](/assets/images/posts/java-web-basics/image-11.webp)


### 4. lombok

![alt text](/assets/images/posts/java-web-basics/image-12.webp)

### 5. SQL预编译

![alt text](/assets/images/posts/java-web-basics/image-13.webp)


### 6. Mybatis 版本差异
![alt text](/assets/images/posts/java-web-basics/image-14.webp)


### 7. Restful 分格推荐
![alt text](/assets/images/posts/java-web-basics/image-15.webp)
![alt text](/assets/images/posts/java-web-basics/image-16.webp)


### 8. JWT令牌技术
![alt text](/assets/images/posts/java-web-basics/image-17.webp)
![alt text](/assets/images/posts/java-web-basics/image-18.webp)

统一校验
1. Filter (Java Web组件之一，用于在请求处理过程中拦截请求，进行校验)

![alt text](/assets/images/posts/java-web-basics/image-19.webp)
![alt text](/assets/images/posts/java-web-basics/image-20.webp)

2. Interceptor (Spring框架组件之一，用于在请求处理过程中拦截请求，进行校验)


![alt text](/assets/images/posts/java-web-basics/image-21.webp)

![alt text](/assets/images/posts/java-web-basics/image-22.webp)

校验拦截框架逻辑
![alt text](/assets/images/posts/java-web-basics/image-23.webp)



- 全局异常处理器
@RestControllerAdvice (用于定义全局异常处理方法)
@ExceptionHandler (用于指定处理的异常类型)


### 9. 事务管理

@Transactional (用于开启事务)

![alt text](/assets/images/posts/java-web-basics/image-24.webp)

事务回滚设置异常类型范围，用于指定在哪些异常情况下回滚事务。
``` java

@Transactional(rollbackFor = Exception.class)

```

![alt text](/assets/images/posts/java-web-basics/image-25.webp)

![alt text](/assets/images/posts/java-web-basics/image-26.webp)

 事务传播行为：required (默认值，嵌套进入事务时，继续使用当前事务；如果当前事务不存在，创建新的事务) requiresNew (事务嵌套时，创建新的事务)
![alt text](/assets/images/posts/java-web-basics/image-27.webp)


### 10. AOP 面向切面编程

![alt text](/assets/images/posts/java-web-basics/image-28.webp)
![alt text](/assets/images/posts/java-web-basics/image-30.webp)
AOP的实现是通过动态代理技术实现的，具体实现原理如下：
1. 代理对象创建：当需要对某个类的方法进行增强时，AOP框架会创建一个代理对象，这个代理对象实现了与目标对象相同的接口或者继承了目标对象的类。
2. 方法拦截：当调用代理对象的方法时，AOP框架会拦截这个方法调用，并根据配置的切面逻辑执行相应的增强操作。
![alt text](/assets/images/posts/java-web-basics/image-31.webp)

![alt text](/assets/images/posts/java-web-basics/image-32.webp)

@Pointcut (用于定义切面的切点表达式) 可以反复使用


AOP 多切面执行顺序：
 1. 与类名的顺序决定切片执行顺序
 2. 也可以通过 @Order 注解来指定切面的执行顺序，默认值为 0，值越小优先级越高

切入点表达式：
1. execution(* com.example.service.*.*(..)) (匹配com.example.service包下的所有方法)
   - ![alt text](/assets/images/posts/java-web-basics/image-33.webp)
   - ![alt text](/assets/images/posts/java-web-basics/image-34.webp)
   - 
2. annotation(com.example.annotation.MyAnnotation) (匹配所有使用MyAnnotation注解的方法)

   - 



### 11. 配置

![alt text](/assets/images/posts/java-web-basics/image-35.webp)

### 12. Bean对象的管理

1. Bean对象的获取

bean对象获取通过IOC容器ApplicationContext实现
 - ApplicationContext (Spring框架的核心接口，用于管理Bean对象)
 - ApplicationContext.getBean(String beanName) (根据Bean的名称获取Bean对象)
 - ApplicationContext.getBean(Class<T> beanType) (根据Bean的类型获取Bean对象)
 - ApplicationContext.getBean(String beanName, Class<T> beanType) (根据Bean的名称和类型获取Bean对象)


2. Bean对象的作用域

![alt text](/assets/images/posts/java-web-basics/image-36.webp)

通过注解 @Scope 来指定Bean的作用域，默认值为 singleton。

通过@Lazy 注解来指定Bean的懒加载.


3. 第三方Bean对象的管理
![alt text](/assets/images/posts/java-web-basics/image-37.webp)


### 13. springboot 原理


1. springboot 启动原理

通过依赖注入，将Bean对象注入到需要使用的地方。

2. springboot 自动配置原理

通过 @EnableAutoConfiguration 注解来启用自动配置功能，Spring Boot会根据类路径中的依赖和配置文件中的设置，自动配置应用程序所需的Bean对象和配置。

@ComponentScan (用于指定自动扫描的包路径)
默认值为当前类所在包，也可以通过 @ComponentScan 注解来指定自动扫描的包路径。

Import (用于导入其他配置类)
默认值为空，也可以通过 @Import 注解来导入其他配置类。
![alt text](/assets/images/posts/java-web-basics/image-38.webp)


![alt text](/assets/images/posts/java-web-basics/image-39.webp)


![alt text](/assets/images/posts/java-web-basics/image-40.webp)


![alt text](/assets/images/posts/java-web-basics/image-41.webp)
