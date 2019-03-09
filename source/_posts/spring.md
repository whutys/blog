---
title: spring
type: categories
copyright: true
date: 2019-01-10 19:47:56
categories: [java,javaweb]
tags: spring容器
---

### 1.ioc控制反转

将对象bean的创建交给spring容器。

使用技术：1.xml配置文件2.dom4j解析3.工厂设计模式4.反射

bean实例化三种方式：

1.无参构造（默认）

```xml
<bean id="bean1" class="bean1ClassPath"></bean>
```

2.静态工厂

```xml
<bean id="bean2" class="bean2factoryClassPath" factory-method="getBean2"></bean>
```

3.实例工厂

```xml
<bean id="bean3factory" class="bean3factoryClassPath"></bean>
<bean id="bean3" factory-bean="bean3factory" factory-method="getBean3"></bean>
```

bean参数：id,class（类路径）,name（同id）.scope（singleton、prototype、request、session、globalsession）

bean属性注入：set方法、有参构造、接口（spring不支持）

```xml
<bean id="" class="">
<constructor-arg name="" value=""></constructor-arg>
</bean>

<bean id="" class="">
<property name="" value=""></property>
</bean>
```

IOC与DI：DI属性注入在IOC创建基础上进行

### 2.aop面向切面编程，拓展功能不修改源代码

采用横向抽取替代传统纵向继承

底层使用 动态代理实现（有接口使用jdk，没接口使用cglib）

**术语：**

**连接点（Joinpoint）**	程序执行的某个特定位置：如类开始初始化前、类初始化后、类某个方法调用前、调用后、方法抛出异常后。一个类或一段程序代码拥有一些具有边界性质的特定点，这些点中的特定点就称为“连接点”。Spring仅支持方法的连接点，即仅能在方法调用前、方法调用后、方法抛出异常时以及方法调用前后这些程序执行点织入通知。连接点由两个信息确定：第一是用方法表示的程序执行点；第二是用相对点表示的方位。

**切点（Pointcut）**    每个程序类都拥有多个连接点，如一个拥有两个方法的类，这两个方法都是连接点，即连接点是程序类中客观存在的事物。AOP通过“切点”定位特定的连接点。连接点相当于数据库中的记录，而切点相当于查询条件。切点和连接点不是一对一的关系，一个切点可以匹配多个连接点。

**通知（Advice）**	通知是织入到目标类连接点上的一段程序代码，在Spring中，通知除用于描述一段程序代码外，还拥有另一个和连接点相关的信息，这便是执行点的方位。结合执行点方位信息和切点信息，我们就可以找到特定的连接点。

前置通知（Before）：在目标方法被调用之前调用通知功能；        后置通知（After）：在目标方法完成之后调用通知，此时不会关心方法的输出是什么；        返回通知（After-returning）：在目标方法成功执行之后调用通知；        异常通知（After-throwing）：在目标方法抛出异常后调用通知；        环绕通知（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行自定义的行为。

**目标对象（Target）**	通知逻辑的织入目标类。如果没有AOP，目标业务类需要自己实现所有逻辑，而在AOP的帮助下，目标业务类只实现那些非横切逻辑的程序逻辑，而性能监视和事务管理等这些横切逻辑则可以使用AOP动态织入到特定的连接点上。

**引介（Introduction）**	 引介是一种特殊的通知，它为类添加一些属性和方法。这样，即使一个业务类原本没有实现某个接口，通过AOP的引介功能，我们可以动态地为该业务类添加接口的实现逻辑，让业务类成为这个接口的实现类。

**织入（Weaving）**		织入是将通知添加对目标类具体连接点上的过程。AOP像一台织布机，将目标类、通知或引介通过AOP这台织布机天衣无缝地编织到一起。根据不同的实现技术，AOP有三种织入的方式：    a、编译期织入，这要求使用特殊的Java编译器。    b、类装载期织入，这要求使用特殊的类装载器。    c、动态代理织入，在运行期为目标类添加通知生成子类的方式。**把切面应用到目标对象来创建新的代理对象的过程，Spring采用动态代理织入，而AspectJ采用编译期织入和类装载期织入。**

**代理（Proxy）**	一个类被AOP织入通知后，就产出了一个结果类，它是融合了原类和通知逻辑的代理类。根据不同的代理方式，代理类既可能是和原类具有相同接口的类，也可能就是原类的子类，所以我们可以采用调用原类相同的方式调用代理类。

**切面（Aspect）**	切面由切点和通知组成，它既包括了横切逻辑的定义，也包括了连接点的定义，Spring AOP就是负责实施切面的框架，它将切面所定义的横切逻辑织入到切面所指定的连接点中。

aspectj

spring配合aspectj完成aop操作。

