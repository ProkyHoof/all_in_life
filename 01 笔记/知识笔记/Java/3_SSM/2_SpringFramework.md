---
tags:
  - 知识
类型: 计算机
领域: SSM
来源: "[黑马程序员Java零基础视频教程_上部(Java入门，含斯坦福大学练习题+力扣算法题和大厂java面试题）](https://www.bilibili.com/video/BV17F411T7Ao?vd_source=aae3c81bc41fca87a978ef4700fc0a91)"
日期: 2026-10-08
关联:
---
# 1 技术体系结构
## 1.1 总体技术体系
1. 单一架构：  

一个项目，一个工程，导出为一个 war 包，在一个 Tomcat 上运行。也叫 all in one。  
单一架构，项目主要应用技术框架：Spring、SpringMVC、Mybatis。  

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%20840dff07f8853363.png)  

2. 分布式架构：  

一个项目（对应 IDEA 中的一个 project），拆分成很多个模块，每个模块是一个 IDEA 中的一个 module，每一个工程都是运行在自己的 Tomcat 上，模块之间可以互相调用，每一个模块内部可以看成是一个架构的应用。  
分布式架构、项目主要应用技术框架：SpringBoot（SSM）、SpringCloud，中间件等。  
## 1.2 框架概念和理解
框架（Framework）是一个集成了基本结构、规范、设计模式、编程语言和程序库等基础组件的软件系统，它可以用来构建更高级别的应用程序。框架的设计和实现旨在解决特定领域中的常见问题，帮助开发人员更高效、更稳定地实现软件开发目标。  
框架的优点包括以下几点：  
1. 提高开发效率。  
2. 降低开发成本。  
3. 提高应用程序的稳定性。  
4. 提高标准化的解决方案。  

站在文件结构的角度理解框架，可以将框架总结：框架 = jar包 + 配置文件。  
常见的单一框架 JavaEE 项目框架演进，从 SSH、SSH2 过渡到了 SSM：SpringMVC、Spring、MyBatis。  
# 2 SpringFramework 介绍
## 2.1 Spring 和 SpringFramework 概念
Spring 技术栈（全家桶）：广义上的 Spring 泛指以 SpringFramework 为基础的 Spring 技术栈。  
SpringFramework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。  
SpringFramework（基础框架）：狭义上的 Spring 特指 Spring Framework，通常将它称为 Spring 框架。  
## 2.2 SpringFramework 主要功能模块
Core Container：核心容器，在 Spring 环境下使用任何功能都必须基于 IoC 容器。  
AOP & Aspects：面向切面编程。  
TX：声明式事务管理。  
SpringMVC：提供了面向 Web 应用程序的集成功能。  
## 2.3 SpringFramework 主要优势
1. 丰富的生态系统。  
2. 模块化的设计。  
3. 简化 Java 开发。  
4. 不断创新和发展。  

# 3 Spring IoC 容器和核心概念
## 3.1 组件和组件管理概念
### 3.1.1 什么是组件
Controller：控制层组件。  
Service：业务逻辑层组件。  
Dao：持久化层组件。  
### 3.1.2 Spring 充当组件管理角色（IoC）
组件可以完全交给 Spring 框架进行管理，Spring 框架替代了程序员原有的 new 对象和对象属性赋值等动作。  

> 注意：组件是映射到应用程序中所有可重用组件的 Java 对象，应该是可复用的功能对象。  
> 1. 组件一定是对象。  
> 2. 对象不一定是组件。  

### 3.1.3 组件交给 Spring 管理优势
1. 降低了组件之间的耦合性。  
2. 提高了代码的可重用性和可维护性。  
3. 方便了配置和管理。  
4. 交给 Spring 管理的对象（组件），方可享受 Spring 框架的其他功能（AOP、声明式事务管理）等。  

## 3.2 Spring IoC 容器和容器实现
### 3.2.1 普通和复杂容器
普通容器：数组、集合 List、集合 Set。  
复杂容器：Servlet 容器能够管理 Servlet（init、service、destroy）、Filter、Listener 这样的组件的一生，所以它是一个复杂容器。  

```vtable
{"rows":[[{"t":"阶段","rs":1,"cs":1},{"t":"触发时机","rs":1,"cs":1},{"t":"次数","rs":1,"cs":1}],[{"t":"创建对象","rs":1,"cs":1},{"t":"默认情况：接收到第一次请求 修改启动顺序后：Web应用启动过程中","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}],[{"t":"初始化操作","rs":1,"cs":1},{"t":"创建对象之后","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}],[{"t":"处理请求","rs":1,"cs":1},{"t":"接收到请求","rs":1,"cs":1},{"t":"多次","rs":1,"cs":1}],[{"t":"销毁操作","rs":1,"cs":1},{"t":"Web应用卸载之前","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}]]}
```

总结：Spring 管理组件的容器，就是一个复杂容器，不仅存储组件，也可以管理组件之间依赖关系，并且创建和销毁组件等。  
### 3.2.2 Spring IoC 容器介绍
Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系。  
### 3.2.3 Spring IoC 容器具体接口和实现类
Spring IoC 容器接口：  
BeanFactory 接口提供了一种高级配置机制，能够管理任何类型的对象，它是 Spring IoC 容器标准化超接口。  
ApplicationContext 是 BeanFactory 的子接口，它扩展了以下功能：  
1. 更容易与 Spring 的 AOP 功能集成。  
2. 消息资源处理（用于国际化）。  
3. 特定于应用程序给予此接口实现，例如 Web 应用程序的 WebApplicationContext。  

BeanFactory 提供了配置框架和基本功能，而 ApplicationContext 添加了更多特定于企业的功能。ApplicationContext 是 BeanFactory 的完整超集。  

```vtable
{"rows":[[{"t":"实现类","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"ClassPathXmlApplicationContext","rs":1,"cs":1},{"t":"通过读取类路径下的XML格式的配置文件创建IoC容器对象","rs":1,"cs":1}],[{"t":"FileSystemXmlApplicationContext","rs":1,"cs":1},{"t":"通过文件系统路径读取XML格式的配置文件创建","rs":1,"cs":1}],[{"t":"AnnotationConfigApplicationContext","rs":1,"cs":1},{"t":"通过读取Java配置类创建IoC容器对象","rs":1,"cs":1}],[{"t":"WebApplicationContext","rs":1,"cs":1},{"t":"专门为Web应用准备，基于Web环境创建IoC容器对象，并将对象引入存入ServletContext域中","rs":1,"cs":1}]]}
```

Spring 框架提供了多种配置方式：XML 配置方式、注解方式和 Java 配置类方式。  
## 3.3 Spring IoC/DI 概念总结
### 3.3.1 IoC 容器
Spring IoC 容器，负责实例化、配置和组装 bean（组件）核心容器。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。  
### 3.3.2 IoC（Inversion of Control）控制反转
IoC 主要是针对对象的创建和调用控制而言的，也就是说，当应用程序需要使用一个对象时，不再是应用程序直接创建该对象，而是由 IoC 容器来创建和管理，即控制权由程序转移到 IoC 容器中，也就是"反转"了控制权。  
这种方式基本上是通过依赖查找的方式来实现的，即 IoC 容器维护着构成应用程序的对象，并负责创建这些对象。  
### 3.3.3 DI（Dependency Injection）依赖注入
DI 是指在组件之间传递依赖关系的过程中，将依赖关系在容器内部进行处理，这样就不必在应用程序代码中硬编码对象之间的依赖关系，实现了对象之间的解耦合，在 Spring 中，DI 是通过 XML 配置文件或注解的方式实现的。  
它提供了三种形式的依赖注入：构造函数注入、Setter 方法注入和接口注入。  
# 4 Spring IoC 实践和应用
## 4.1 Spring IoC/DI 实现步骤
### 4.1.1 基于 XML 的 IoC 配置
1. 配置元数据：  

基于 XML 的配置元数据的基本结构：  

```xml
<!-- 添加一些约束,配置文件等标签并不是随意命名 -->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="" [1] class="" [2]>
    </bean>
</beans>
```

Spring IoC 容器管理一个或多个组件，这些组件是使用你提供给容器的配置元数据（例如，以 XML `<bean/>` 定义的形式）创建的。  
`<bean/>` 标签 == 组件信息声明。  
1. id 属性是标志单个 Bean 定义的字符串。  
2. class 属性定义 Bean 的类型并使用完全限定的类名。  
2. 实例化 IoC 容器：  

提供给 ApplicationContext 构造函数的位置路径是资源字符串地址，允许容器从各种外部资源（如本地文件系统、Java CLASSPATH 等）加载配置元数据。  
3. 获取 Bean（组件）：  

ApplicationContext 是一个高级工厂的接口，能够维护不同 bean 及其依赖项的注册表，通过使用 T getBean(String name, `Class<T>` requiredType)，您可以检索 bean 的实例。  

```java
// 实例化IoC容器,读取外部配置文件,最终会在容器内进行IoC和DI动作
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```

```java
// 创建IoC容器对象,指定配置文件,IoC也开始实例组件对象
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
// 获取IoC容器的组件对象
PetStoreService service = context.getBean("petStore", PetStoreService.class);
// 使用组件对象
List<String> userList = service.getUsernameList();
```

```xml
<!-- pom.xml -->
<dependencies>
    <!-- spring context依赖
         当你引入Spring Context依赖之后,表示将Spring的基础依赖引入了 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>
    <!-- junit5测试 -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
```

4. 基于无参构造：  

当通过构造函数方法创建一个 bean（组件对象）时，所有普通类都可以由 Spring 使用并与之兼容，也就是说，正在开发的类不需要实现任何特定的接口或以特定的方式进行编码，只需指定 Bean 类信息就足够了，但是，默认情况下，我们需要一个默认（空）构造函数。  
1. 准备组件类：  

```java
public class HappyComponent {
    // 默认包含无参数构造函数
    public void doWork() {
        System.out.println("HappyComponent.doWork");
    }
}
```

2. xml 配置文件编写：  

创建携带 Spring 约束的 xml 配置文件。  
编写配置文件：resources/spring-bean-01.xml。  

```xml
<!-- 创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.HappyComponent"/>
```

1. bean 标签：通过配置 bean 标签告诉 IoC 容器需要创建对象的组件信息。  
2. id 属性：bean 的唯一标识，方便后期获取 Bean。  
3. class 属性：组件类的全限定名。  
4. 注意：要求当前组件类必须包含无参数构造函数。  
5. 基于静态工厂方法实例化：  

除了使用构造函数实例化对象，还有一类是通过工厂模式实例化对象，接下来我们讲解如何定义使用静态工厂方法创建 Bean 的配置。  
1. 准备组件类：  

```java
public class ClientService {
    private static ClientService clientService = new ClientService();
    private ClientService() {}
    public static ClientService createInstance() {
        return clientService;
    }
}
```

2. xml 配置文件编写：  

文件：resources/spring-bean-01.xml。  

```xml
<bean id="clientService" class="example.ClientService" factory-method="createInstance"/>
```

1. class 属性：指定工厂类的全限定名。  
2. factory-method：指定静态工厂方法，注意，该方法必须是 static 方法。  
6. 基于实例工厂方法实例化：  
1. 准备组件类：  

```java
public class DefaultServiceLocator {
    private static ClientService clientService = new ClientServiceImpl();
    public ClientService createClientServiceInstance() {
        return clientService;
    }
}
```

2. xml 配置文件编写：  

文件：resources/spring-bean-01.xml。  

```xml
<!-- 工厂类进行IoC配置 -->
<bean id="serviceLocator" class="example.DefaultServiceLocator"></bean>
<!-- 根据工厂对象的实例工厂进行实例化组件对象 -->
<bean id="clientService" factory-bean="serviceLocator" factory-method="createClientServiceInstance"/>
```

1. factory-bean 属性：指定当前容器中工厂 Bean 的名称。  
2. factory-method：指定实例工厂方法名。注意，实例方法必须是非 static 的。  

### 4.1.2 依赖注入配置 DI
1. 目标：  

通过配置文件，实现 IoC 容器中 Bean 之间的引用（依赖注入 DI 配置）。  
主要涉及注入场景，基于构造函数的依赖注入和基于 Setter 的依赖注入。  
2. 基于构造函数的依赖注入（单个构造参数）：  
1. 介绍：  

基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。  
2. 准备组件类：  

```java
public class UserDao {}
public class UserService {
    private UserDao userDao;
    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }
}
```

3. 编写配置文件：  

文件：resources/spring-02.xml。  

```xml
<beans>
    <!-- 应用类bean声明 -->
    <bean id="userService" class="x.y.UserService">
        <!-- 构造函数引用 -->
        <constructor-arg ref="userDao"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

1. constructor-arg 标签：可以引用构造参数 ref 引用其他 bean 的标签。  
3. 基于构造函数的依赖注入（多构造参数解析）：  
1. 介绍：  

基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。  
2. 准备组件类：  

```java
public class UserDao {}
public class UserService {
    private UserDao userDao;
    private int age;
    private String name;
    public UserService(int age, String name, UserDao userDao) {
        this.userDao = userDao;
        this.age = age;
        this.name = name;
    }
}
```

3. 编写配置文件：  

```xml
<!-- 场景1 多参数,可以按照相应构造函数的顺序注入数据 -->
<beans>
    <bean id="userService" class="x.y.UserService">
        <!-- value直接注入基本类型值 -->
        <constructor-arg value="18"/>
        <constructor-arg value="张三"/>
        <constructor-arg ref="userDao"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

```xml
<!-- 场景2 多参数,可以按照相应构造函数的名称注入数据 -->
<beans>
    <bean id="userService" class="x.y.UserService">
        <constructor-arg name="name" value="张三"/>
        <constructor-arg name="userDao" ref="userDao"/>
        <constructor-arg name="age" value="18"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

```xml
<!-- 场景3 多参数,可以按照相应构造函数的角标注入数据 index从0开始,构造函数(0,1,2,3...) -->
<beans>
    <bean id="userService" class="x.y.UserService">
        <constructor-arg index="1" value="张三"/>
        <constructor-arg index="2" ref="userDao"/>
        <constructor-arg index="0" value="18"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

4. 基于 Setter 方法依赖注入：  
1. 介绍：  

开发中，除了构造函数注入（DI），更多的使用 Setter 方法进行注入。  
2. 准备组件类：  

```java
public class MovieFinder {}
public class SimpleMovieLister {
    private MovieFinder movieFinder;
    private String movieName;
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
    public void setMovieName(String movieName) {
        this.movieName = movieName;
    }
}
```

3. 编写配置文件：  

```xml
<beans>
    <bean id="movieFinder" class="x.y.MovieFinder"/>
    <bean id="simpleMovieFinder" class="x.y.SimpleMovieLister">
        <!-- Setter方法,注入movieFinder对象的标识 name=属性名 ref=引用bean的Id值 -->
        <property name="movieFinder" ref="movieFinder"/>
        <!-- Setter方法,注入基本数据类型movieName name=属性名 value=基本类型值 -->
        <property name="movieName" value="怎么是猪脚"/>
    </bean>
</beans>
```

1. property 标签：可以给 Setter 方法对应的属性赋值。  
2. property 标签：name 属性代表 set 方法标识、ref 代表引用 bean 的标识 Id、value 属性代表基本属性值。  

总结：  
依赖注入（DI）包含引用类型和基本数据类型、同时注入的方法也有很多种。主流的注入方法为 Setter 方法注入和构造函数注入。  

> 注意：引用其他 bean，使用 ref 属性，直接注入基本类型值，使用 value 属性。  

### 4.1.3 IoC 容器创建和使用
1. 介绍：  

想要配置文件中声明组件类信息真正的进行实例化成 Bean 对象和形成 Bean 之间的引用关系，我们需要声明 IoC 容器对象，读取配置文件，实例化组件和关系维护的过程都是在 IoC 容器中实现。  
2. 容器实例化：  

```java
// 创建IoC容器并且读取配置文件
public void createIoC() {
    // 创建容器 选择合适的容器即可
    // 接口  BeanFactory ApplicationContext
    // ------------------------------------------------------------------------
    // 实现类 可以直接通过构造函数进行实例化
    // ClassPathXmlApplicationContext 读取类路径下的xml配置方式 classes
    // FileSystemXmlApplicationContext 读取指定文件位置的xml配置方式
    // AnnotationConfigApplicationContext 读取配置类方式的IoC容器
    // WebApplicationContext web项目专属的配置的IoC容器
    // 方式1:直接创建容器并且指定配置文件即可 [推荐]
    // 构造函数(String...配置文件)可以填写一个或者多个
    ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring-03.xml");
    // 方式2:先创建IoC容器对象,再指定配置文件,再刷新
    // 源码的配置过程 创建容器[spring]和配置文件指定分开[自己指定]
    ClassPathXmlApplicationContext applicationContext2 = new ClassPathXmlApplicationContext();
    // 外部配置文件的设置
    applicationContext2.setConfigLocations("spring-03.xml");
    // 调用IoC和DI的流程
    applicationContext2.refresh();
}

// 在IoC容器中读取组件Bean
public void getBeanFromIoC() {
    // 1 创建IoC容器对象
    ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext();
    applicationContext.setConfigLocations("spring-03.xml");
    applicationContext.refresh();
    // 2 读取IoC容器的组件
    // 方案1:直接根据BeanId获取即可 返回值类型是Object 需要强转[不推荐]
    HappyComponent happyComponent1 = (HappyComponent) applicationContext.getBean("happyComponent");
    // 方案2:根据beanId 同时指定Bean的类型class
    HappyComponent happyComponent2 = applicationContext.getBean("happyComponent", HappyComponent.class);
    // 方案3:直接根据类型接收
    // TODO 根据Bean的类型获取,同一个类型,在IoC容器中只能有一个Bean
    // TODO 如果IoC容器中存在多个同类型的Bean会出现:NoUniqueBeanDefinitionException
    // TODO IoC的配置一定是实现类,但是可以根据接口类型取值
    HappyComponent happyComponent3 = applicationContext.getBean(HappyComponent.class);
    happyComponent2.doWork();
}
```

### 4.1.4 组件（Bean）作用域和周期方法配置
1. 组件周期方法配置：  
1. 周期方法概念：  

在组件中定义方法，然后当 IoC 容器实例化和销毁组件对象的时候进行调用，这两个方法称为生命周期方法。  
类似于 Servlet 的 init/destroy 方法。  
2. 周期方法声明：  

```java
public class JavaBean {
    // 周期方法要求:方法命名随意,但是要求方法必须是public void 无形参列表
    public void init() {
        // 初始化逻辑
    }
    public void cleanup() {
        // 释放销毁逻辑
    }
}
```

3. 周期方法配置：  

```xml
<beans>
    <!-- init-method="初始化方法名"
         destroy-method="销毁方法名"
         SpringIoC容器就会在对应的时间节点回调对应的方法,可以在其中写对应的业务 -->
    <bean id="javaBean" class="com.prokyhoof.ioc04.JavaBean" init-method="init" destroy-method="cleanup"/>
</beans>
```

2. 组件作用域配置：  
1. Bean 作用域概念：  

`<bean>` 标签声明 Bean，只是将 Bean 的信息配置给 SpringIoC 容器。  
在 IoC 容器中，这些 `<bean>` 标签对应的信息转成 Spring 内部 BeanDefinition 对象，BeanDefinition 对象内，包含定义的信息（id、class 属性等等）。  
这意味着，BeanDefinition 与类概念一样，SpringIoC 容器可以根据 BeanDefinition 对象反射创建多个 Bean 对象实例。  
具体创建多少个 Bean 的实例对象，由 Bean 的作用域 Scope 属性指定。  
2. 作用域可选值：  

```vtable
{"rows":[[{"t":"取值","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1},{"t":"创建对象的时机","rs":1,"cs":1},{"t":"默认值","rs":1,"cs":1}],[{"t":"singleton","rs":1,"cs":1},{"t":"在IoC容器中，这个Bean的对象始终为单实例","rs":1,"cs":1},{"t":"IoC容器初始化时","rs":1,"cs":1},{"t":"是","rs":1,"cs":1}],[{"t":"prototype","rs":1,"cs":1},{"t":"这个Bean在IoC容器中有多个实例","rs":1,"cs":1},{"t":"获取Bean时","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}]]}
```

如果是在 WebApplicationContext 环境下还会有另外两个作用域（但不常用）：  

```vtable
{"rows":[[{"t":"取值","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1},{"t":"创建对象的时机","rs":1,"cs":1},{"t":"默认值","rs":1,"cs":1}],[{"t":"request","rs":1,"cs":1},{"t":"请求范围内有效的实例","rs":1,"cs":1},{"t":"每次请求","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}],[{"t":"session","rs":1,"cs":1},{"t":"会话范围内有效的实例","rs":1,"cs":1},{"t":"每次会话","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}]]}
```

```xml
<!-- 声明一个组件信息,默认就是单例模式 一个Bean标签对应一个beanDefinition组件对象 -->
<bean id="javaBean" class="com.prokyhoof.ioc04.JavaBean" scope="singleton"/>
```

### 4.1.5 FactoryBean 特征和使用
1. FactoryBean 简介：  

FactoryBean 接口是 Spring IoC 容器实例化逻辑的可插拔特点。  
用于配置复杂的 Bean 对象，可以将创建过程存储在 FactoryBean 的 getObject 方法。  
`FactoryBean<T>` 接口提供三种方法：  
1. T getObject()：返回此工厂创建的对象的实例，该返回值会被存储到 IoC 容器。  
2. boolean isSingleton()：如果此 Factory 返回单例，则返回 true，否则返回 false，此方法的默认实现返回 true（注意，lombok 插件使用，可能会影响效果）。  
3. Class<?> getObjectType()：返回 getObject() 方法返回的对象类型，如果事先不知道类型，则返回 null。  
2. FactoryBean 使用场景：  
1. 代理类的创建。  
2. 第三方框架整合。  
3. 复杂对象实例化等。  
3. FactoryBean 应用：  
1. 准备 FactoryBean 实现类：  

```java
public class JavaBean {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```

2. 准备 FactoryBean 类：  

```java
// 1 实现FactoryBean接口<返回值类型>
public class JavaBeanFactoryBean implements FactoryBean<JavaBean> {
    @Override
    public JavaBean getObject() throws Exception {
        // 使用自己的方式实例化对象就可以了
        JavaBean javaBean = new JavaBean();
        return javaBean;
    }

    @Override
    public Class<?> getObjectType() {
        return JavaBean.class;
    }
}
```

3. xml 配置：  

```xml
<!-- id getObject方法返回的对象的标识
     class FactoryBean标准工厂类 -->
<bean id="javaBean" class="com.prokyhoof.ioc05.JavaBeanFactoryBean"/>
```

4. FactoryBean 和 BeanFactory 区别：  

FactoryBean 是 Spring 中一种特殊的 Bean，可以在 getObject() 工厂方法自定义的逻辑创建 Bean。是一种能够生产其他 Bean 的 Bean。FactoryBean 在容器启动时被创建，而在实际使用时则是调用 getObject() 方法来得到其所生产的 Bean。因此，FactoryBean 可以自定义任何所需的初始化逻辑，生产出一些定制化的 Bean。  
一般情况下，整合第三方框架，都是通过定义 FactoryBean 实现。  
BeanFactory 是 Spring 框架的基础，其作为一个顶级接口定义了容器的基本行为，例如管理 Bean 的生命周期、配置文件的加载和解析，Bean 的装配和依赖注入等。BeanFactory 接口提供了访问 Bean 的方式，例如 getBean() 方法获取指定的 Bean 实例。它可以从不同的来源（例如 MySQL 数据库、XML 文件、Java 配置类等）获取 Bean 定义、并将其转换为 Bean 实例。同时，BeanFactory 还包含很多子类（例如，ApplicationContext 接口）提供了额外的强大功能。  
总得来说，FactoryBean 和 BeanFactory 的区别主要在于前者是用于创建 Bean 的接口，它提供了更加灵活的初始化定制功能，而后者是用于管理 Bean 的架构基础接口，提供了基本的容器功能和 Bean 生命周期管理。  
### 4.1.6 基于 XML 方式整合三层架构组件
将三层架构中的 Controller、Service、Dao 组件全部声明到 xml 配置文件中，通过 ref 引用完成组件之间的依赖注入，这是 SSM（SpringMVC + Spring + MyBatis）整合前的纯 Spring 三层搭建方式。  
1. 准备组件类：  

```java
public interface UserDao {
    void save();
}
@Repository
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("UserDao.save");
    }
}
```

```java
public class UserService {
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void save() {
        userDao.save();
    }
}
```

```java
public class UserController {
    private UserService userService;
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    public void save() {
        userService.save();
    }
}
```

2. xml 配置（resources/spring-04.xml）：  

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!-- Dao层组件 -->
    <bean id="userDao" class="com.prokyhoof.dao.UserDaoImpl"/>
    <!-- Service层组件,注入Dao -->
    <bean id="userService" class="com.prokyhoof.service.UserService">
        <property name="userDao" ref="userDao"/>
    </bean>
    <!-- Controller层组件,注入Service -->
    <bean id="userController" class="com.prokyhoof.controller.UserController">
        <property name="userService" ref="userService"/>
    </bean>
</beans>
```

3. 获取并使用：  

```java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("spring-04.xml");
UserController controller = context.getBean("userController", UserController.class);
controller.save();
```

> 注意：三层架构中每一层只依赖自己的下一层，依赖关系通过 setter 注入维护，后续整合 MyBatis 时，Dao 层会替换为 MyBatis 的 Mapper 实现。  

## 4.2 基于注解方式管理 Bean
### 4.2.1 注解理解
和 XML 配置文件一样，注解本身并不能执行，注解本身仅仅只是做一个标记，具体的功能是框架检测到注解标记的位置，然后针对这个位置按照注解标记的功能来执行具体操作。  
本质上，所有一切的操作都是 Java 代码来完成的，XML 和注解只是告诉框架中的 Java 代码如何执行。  
### 4.2.2 扫描理解
Spring 为了知道程序员在哪些地方标记了什么注解，就需要通过扫描的方式，来进行检测。然后根据注解进行后续操作。  
### 4.2.3 准备 Spring 项目和组件
1. 准备项目 pom.xml：  

```xml
<dependencies>
    <!-- Spring Context依赖
         当你引用Spring Context依赖之后,表示将Spring的基础依赖引入了 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>
    <!-- junit5测试 -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
```

2. 准备组件类：  

普通组件：  

```java
public class CommonComponent {}
```

Controller 组件：  

```java
public class XxxController {}
```

Service 组件：  

```java
public class XxxService {}
```

Dao 组件：  

```java
public class XxxDao {}
```

### 4.2.4 组件添加标记注解
1. 组件标记注解和区别：  

Spring 提供了以下多个注解，这些注解可以直接标注在 Java 类上，将它们定义成 SpringBean。  

```vtable
{"rows":[[{"t":"注解","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"@Component","rs":1,"cs":1},{"t":"该注解用于描述Spring中的Bean，它是一个泛化的概念，仅仅表示容器中的一个组件（Bean），并且可以作用在引用的任何层次，例如Service层、Dao层等，使用时只需将注解标注在相应类上即可","rs":1,"cs":1}],[{"t":"@Repository","rs":1,"cs":1},{"t":"该注解用于将数据访问层（Dao层）的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}],[{"t":"@Service","rs":1,"cs":1},{"t":"该注解通常作用在业务层（Service层），用于将业务层的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}],[{"t":"@Controller","rs":1,"cs":1},{"t":"该注解通常作用在控制层（Controller层），用于将控制层的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}]]}
```

@Controller、@Service、@Repository 这三个注解只是在 @Component 注解的基础上起了三个新的名字。  
对于 Spring 使用 IoC 容器管理这些组件来说没有区别，也就是语法层面没有区别，所以 @Controller、@Service、@Repository 这三个注解只是给开发人员看的，让我们能够便于分辨组件的作用。  

> 注意：虽然他们本质上一样，但是为了代码的可读性，程序结构严谨，不能乱标记。  

### 4.2.5 配置文件确定扫描范围
情况 1：基本扫描配置：  

```xml
<!-- 配置自动扫描的包
     1 包要精准
     2 会扫描指定的包和子包内容
     3 多个包可以使用","分割 -->
<beans>
    <context:component-scan base-package="com.prokyhoof.components"/>
</beans>
```

情况 2：指定排除组件：  

```xml
<beans>
    <context:component-scan base-package="com.prokyhoof.components">
        <!-- context:exclude-filter标签:指定排除规则
             type属性:指定根据什么来进行排除,annotation取值表示根据注解来排除
             expression属性:指定排除规则的表达式,对于注解来说指定全类名即可 -->
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
</beans>
```

情况 3：指定扫描文件：  

```xml
<!-- 仅扫描 = 关闭默认规则 + 追加规则
     use-default-filters属性:取值false表示关闭默认扫描规则 -->
<context:component-scan base-package="com.prokyhoof.ioc.components" use-default-filters="false">
    <!-- context:include-filter标签:指定在原有扫描规则的基础上追加规则 -->
    <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

### 4.2.6 组件 BeanName 问题
在我们使用 XML 方式管理 Bean 的时候，每个 Bean 都有一个唯一标识——id 属性的值，便于在其他地方引用，现在使用注解后，每个组件仍然应该有一个唯一标识。  
默认情况：  
类名首字母小写就是 Bean 的 id。例如：SoldierController 类对应的 Bean 的 id 就是 soldierController。  
使用 value 属性指定：  

```java
@Controller(value = "tianDog")
public class SoldierController {}
```

当注解中只设置一个属性时，value 属性的属性名可以省略。  
### 4.2.7 组件（Bean）作用域和周期方法注解
1. 组件周期方法配置：  
1. 周期方法概念：  

在组件类中定义方法，然后当 IoC 容器实例化和销毁组件对象的时候进行调用。这两个方法我们称为生命周期方法。  
类似于 Servlet 的 init/destroy 方法，可以在周期方法完成初始化和释放资源等工作。  
2. 周期方法声明：  

```java
public class BeanOne {
    // 周期方法要求:方法命名随意,但是要求方法必须是public void 无形参列表
    @PostConstruct // 注解指定初始化方法
    public void init() {
        // 初始化逻辑
    }
}
public class BeanTwo {
    @PreDestroy // 注解指定销毁方法
    public void cleanup() {
        // 释放资源逻辑
    }
}
```

2. 组件作用域配置：  
1. Bean 作用域概念：  

`<bean>` 标签声明 Bean、只是将 Bean 的信息配置给 SpringIoC 容器。  
在 IoC 容器中，这些 `<bean>` 标签对应的信息转成 Spring 内部 BeanDefinition 对象，BeanDefinition 对象内，包含定义的信息（id、class 属性等等）。  
这意味着，BeanDefinition 与类概念一样，SpringIoC 容器可以根据 BeanDefinition 对象反射创建多个 Bean 对象实例。  
具体创建多少个 Bean 的实例对象，由 Bean 的作用域 Scope 属性指定。  
2. 作用域可选值：  

```vtable
{"rows":[[{"t":"取值","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1},{"t":"创建对象的时机","rs":1,"cs":1},{"t":"默认值","rs":1,"cs":1}],[{"t":"singleton","rs":1,"cs":1},{"t":"在IoC容器中，这个Bean的对象初始为单实例","rs":1,"cs":1},{"t":"IoC容器初始化时","rs":1,"cs":1},{"t":"是","rs":1,"cs":1}],[{"t":"prototype","rs":1,"cs":1},{"t":"这个Bean在IoC容器中有多个实例","rs":1,"cs":1},{"t":"获取Bean时","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}]]}
```

如果是在 WebApplicationContext 环境下还会有另外两个作用域（不常用）：  

```vtable
{"rows":[[{"t":"取值","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1},{"t":"创建对象的时机","rs":1,"cs":1},{"t":"默认值","rs":1,"cs":1}],[{"t":"request","rs":1,"cs":1},{"t":"请求范围内有效的实例","rs":1,"cs":1},{"t":"每次请求","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}],[{"t":"session","rs":1,"cs":1},{"t":"会话范围内有效的实例","rs":1,"cs":1},{"t":"每次会话","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}]]}
```

3. 作用域配置：  

```java
@Scope(scopeName = ConfigurableBeanFactory.SCOPE_SINGLETON) // 单例,默认值
// @Scope(scopeName = ConfigurableBeanFactory.SCOPE_PROTOTYPE) // 多例,二选一
public class BeanOne {
    // 周期方法要求:方法命名随意,但是要求方法必须是public void 无形参列表
    @PostConstruct // 注解指定初始化方法
    public void init() {
        // 初始化逻辑
    }
}
```

### 4.2.8 Bean 属性赋值：引用类型自动装配（DI）
1. 设定场景：  
1. SoldierController 需要 SoldierService。  
2. SoldierService 需要 SoldierDao。  

同时在各个组件中声明要调用的方法。  
3. SoldierController 中声明方法：  

```java
import org.springframework.stereotype.Controller;
@Controller(value = "tianDog")
public class SoldierController {
    private SoldierService soldierService;
    public void getMessage() {
        soldierService.getMessage();
    }
}
```

4. SoldierService 中声明方法：  

```java
@Service("smallDog")
public class SoldierService {
    private SoldierDao soldierDao;
    public void getMessage() {
        soldierDao.getMessage();
    }
}
```

5. SoldierDao 中声明方法：  

```java
@Repository
public class SoldierDao {
    public void getMessage() {
        System.out.println("I am a soldier");
    }
}
```

2. 自动装配实现：  
1. 前提：  

参与自动装配的组件（需要装配、被装配）全部都必须在 IoC 容器中。  

> 注意：不区分 IoC 的方式，XML 和注解都可以。  

2. @Autowired 注解：  

在成员变量上直接标记 @Autowired 注解即可，不需要提供 setXxx() 方法。  
3. 佛系装配：  

给 @Autowired 注解设置 required = false 属性表示：能装就装，装不上就不装，但是实际开发时，基本上所有需要装配的地方都是必须装配的。  

```java
@Controller(value = "tianDog")
public class SoldierController {
    // 给@Autowired注解设置required = false属性表示,能装就装,装不上就不装
    @Autowired(required = false)
    private ISoldierService soldierService;
}
```

4. 扩展 JSR-250 注解 @Resource：  
1. 理解 JSR 系列注解：  

JSR（Java Specification Requests）是 Java 平台标准化进程中的一种技术规范，而 JSR 注解是其中一部分重要的内容。  

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%209ed89dbd303bda94.png)  
![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%2047782c4287f71813.png)  

@Resource 注解属于 JDK 扩展包，所以不在 JDK 当中，需要额外引入以下依赖（高于 JDK11 或低于 JDK8 需要引入以下依赖）：  

```xml
<dependency>
    <groupId>jakarta.annotation</groupId>
    <artifactId>jakarta.annotation-api</artifactId>
    <version>2.1.1</version>
</dependency>
```

2. @Resource 使用：  

```java
@Controller
public class XxxController {
    // 1 如果没有指定name,先根据属性名查找IoC中组件XxxService
    // 2 如果没有指定name,并且属性名没有对应的组件,会根据属性类型查找
    // 3 可以指定name名称查找。@Resource(name = "test") == @Autowired + @Qualifier(value = "test")
    @Resource
    private XxxService xxxService;
}
```

### 4.2.9 Bean 属性赋值：基本类型属性赋值（DI）
@Value 通常用于注入外部化属性。  
声明外部配置 application.properties：  

```properties
catalog.name = MovieCatalog
```

xml 引入外部配置：  

```xml
<!-- 引入外部配置文件 -->
<context:property-placeholder location="application.properties"/>
```

@Value 注解读取配置：  

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class CommonComponent {
    // 情况1:${key} 取外部配置key对应的值
    // 情况2:${key:defaultValue} 没有key,可以给与默认值
    @Value("${catalog.name:prokyhoof}")
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```

## 4.3 基于配置类方法管理 Bean
### 4.3.1 完全注解开发理解
Spring 完全注解配置（Fully Annotation-based Configuration）是指通过 Java 配置类代码来配置 Spring 应用程序，使用注解来替代原本在 XML 配置文件中的配置，相对于 XML 配置，完全注解配置具有更强的类型安全性和更好的可读性。  
### 4.3.2 配置类和扫描注解

```java
// 添加@Configuration代表配置类
@Configuration
@ComponentScan(value = {"com.prokyhoof.ioc01", "com.prokyhoof.ioc02"})
@PropertySource(value = "classpath:jdbc.properties")
public class JavaConfiguration {
}
```

测试创建 IoC 容器：  

```java
// AnnotationConfigApplicationContext根据配置类创建IoC容器对象
ApplicationContext iocContainerAnnotation = new AnnotationConfigApplicationContext(JavaConfiguration.class);
```

可以使用 no-arg 构造函数实例化 AnnotationConfigApplicationContext，然后使用 register() 方法对其进行配置。此方法在以编程方式生成 AnnotationConfigApplicationContext 时特别有用。  

```java
// AnnotationConfigApplicationContext-IoC容器对象
ApplicationContext iocContainerAnnotation = new AnnotationConfigApplicationContext();
// 外部设置配置类
iocContainerAnnotation.register(JavaConfiguration.class);
// 刷新后方可生效
iocContainerAnnotation.refresh();
```

总结：  
@Configuration 指定一个类为配置类，可以添加配置注解，替代配置 xml 文件。  
@ComponentScan(basePackage = {"包","包"}) 替代 `<context:component-scan>` 标签实现注解扫描。  
@PropertySource("classpath:配置文件地址") 替代 `<context:property-placeholder>` 标签。  
配合 IoC/DI 注解：可以进行完整注解开发。  
### 4.3.3 @Bean 定义组件

```java
@ComponentScan(value = {"com.prokyhoof.ioc_01", "com.prokyhoof.ioc_02"})
@PropertySource(value = "classpath:jdbc.properties")
@Configuration
public class JavaConfiguration {
    // 方法的返回值类型 = Bean组件的类型或者他的接口和父类
    // 方法的名字 = BeanId
    @Value("${prokyhoof.url}")
    private String url;
    @Value("${prokyhoof.driverClassName}")
    private String driverClassName;
    @Value("${prokyhoof.username}")
    private String username;
    @Value("${prokyhoof.password}")
    private String password;

    @Bean
    public DruidDataSource dataSource() {
        DruidDataSource druidDataSource = new DruidDataSource();
        druidDataSource.setUrl(url);
        druidDataSource.setDriverClassName(driverClassName);
        druidDataSource.setUsername(username);
        druidDataSource.setPassword(password);
        return druidDataSource;
    }
}
```

### 4.3.4 高级特性：@Bean 注解细节
1. @Bean 生成 BeanName 问题：  

@Bean 注解源码：  

```java
public @interface Bean {
    // 前两个注解可以指定Bean的标识
    @AliasFor("name")
    String[] value() default {};
    @AliasFor("value")
    String[] name() default {};
    // autowireCandidate 属性来指定该Bean是否候选用于自动装配
    // autowireCandidate 属性默认值为true,表示该Bean是一个默认的装配目标
    // 可被候选用于自动装配,如果将autowireCandidate属性设置为false,则说明该Bean不是默认的装配目标,不会被候选用于自动装配
    boolean autowireCandidate() default true;
    // 指定初始化方法
    String initMethod() default "";
    // 指定销毁方法
    String destroyMethod() default "(inferred)";
}
```

问题 1：BeanName 的问题。  
默认：方法名。  
指定：name/value 属性起名字，覆盖方法名。  
问题 2：周期方法如何指定。  
原有注解方案：@PostConstruct + @PreDestroy 注解指定。  
Bean 属性指定：initMethod/destroyMethod 指定。  
问题 3：作用域。  
和以前还是一样 @Scope 注解，默认是单例。  
问题 4：如何引用其他的 ioc 组件。  
直接调用对方的 Bean 方法即可。  
直接形参变量进行引入，要求必须有对应的组件，如果有多个形参名，组件 id 标识即可。  
### 4.3.5 高级特性：@Import 扩展
@Import 注解允许从另一个配置类加载 @Bean 定义。  

```java
@Configuration
public class ConfigA {
    @Bean
    public A a() {
        return new A();
    }
}

@Configuration
@Import(ConfigA.class)
public class ConfigB {
    @Bean
    public B b() {
        return new B();
    }
}
```

现在，在实例化上下文时不需要同时指定 ConfigA.class 和 ConfigB.class，只需显示提供 ConfigB：  

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(ConfigB.class);
    // now both beans A and B will be available
    A a = ctx.getBean(A.class);
    B b = ctx.getBean(B.class);
}
```

此方法简化了容器实例化，因为只需要处理一个类，而不是要求在构建期间记住可能大量的 @Configuration 类。  
## 4.4 三种配置方式总结
### 4.4.1 XML 方式配置总结
1. 所有内容写到 xml 格式配置文件中。  
2. 声明 bean 通过 `<bean>` 标签。  
3. `<bean>` 标签包含基本信息（id、class）和属性信息 `<property name value/ref>`。  
4. 引入外部的 properties 文件可以通过 `<context:property-placeholder>`。  
5. IoC 具体容器实现选择 ClassPathXmlApplicationContext 对象。  

### 4.4.2 XML + 注解方式配置总结
1. 注解负责标记 IoC 的类和进行属性装配。  
2. xml 文件依然需要，需要通过 `<context:component-scan>` 标签指定注解范围。  
3. 标记 IoC 注解：@Component、@Service、@Controller、@Repository。  
4. 标记 DI 注解：@Autowired、@Qualifier、@Resource、@Value。  
5. IoC 具体容器实现选择 ClassPathXmlApplicationContext 对象。  

### 4.4.3 完全注解方式配置总结
1. 完全注解方式指的是去掉 xml 文件，使用配置类 + 注解实现。  
2. xml 文件替换成使用 @Configuration 注解标记的类。  
3. 标记 IoC 注解：@Component、@Service、@Controller、@Repository。  
4. 标记 DI 注解：@Autowired、@Qualifier、@Resource、@Value。  
5. `<context:component-scan>` 标签指定注解范围使用 @ComponentScan(basePackages = {"com.prokyhoof.components"}) 替代。  
6. `<context:property-placeholder>` 引入外部配置文件使用 @PropertySource({"classpath:application.properties", "classpath:jdbc.properties"}) 替代。  
7. `<bean>` 标签使用 @Bean 注解和方法实现。  
8. IoC 具体容器实现选择 AnnotationConfigApplicationContext 对象。  

## 4.5 整合 Spring5-Junit5 搭建测试环境
1. 导入相关依赖：  

```xml
<!-- junit5测试 -->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.3.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>6.0.6</version>
    <scope>test</scope>
</dependency>
```

2. 整合测试注解使用：  

```java
// @SpringJunitConfig(locations = {"classpath:spring-context.xml"}) // 指定配置文件xml
@SpringJunitConfig(value = {BeanConfig.class}) // 指定配置类
public class Junit5IntegrationTest {
    @Autowired
    private User user;
    @Test
    public void testJunit5() {
        System.out.println(user);
    }
}
```

# 5 Spring AOP 面向切面编程
## 5.1 解决技术代理模式
### 5.1.1 代理模式
二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类间接调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——解耦。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。  
### 5.1.2 静态代理
主动创建代理类。  

```java
public class CalculatorStaticProxy implements Calculator {
    // 将换代理的目标对象声明为成员变量
    private Calculator target;
    public CalculatorStaticProxy(Calculator target) {
        this.target = target;
    }
    @Override
    public int add(int i, int j) {
        // 附加功能由代理类中的代理方法来实现
        System.out.println("参数是:" + i + ", " + j);
        // 通过目标对象来实现核心业务逻辑
        int addResult = target.add(i, j);
        System.out.println("方法内部 result = " + addResult);
        return addResult;
    }
}
```

静态代理确实实现了解耦，但是由于代码都是写死的，完全不具备任何的灵活性，就拿日志功能来说，将来其他地方也需要附加日志，那还得再声明更多个静态代理类，那就产生了大量重复的代码，日志功能还是分散的，没有统一管理。  
### 5.1.3 动态代理
动态代理技术分类：  
1. JDK 动态代理：JDK 原生的实现方式，需要被代理的目标类必须实现接口，会根据目标类的接口动态生成一个代理对象。代理对象和目标对象有相同的接口。  
2. cglib：通过继承被代理的目标类实现代理，所以不需要目标类实现接口。  

```java
public class ProxyFactory {
    private Object target;
    public ProxyFactory(Object target) {
        this.target = target;
    }
    public Object getProxy() {
        // newProxyInstance():创建一个代理实例
        // 其中有三个参数:
        // 1 classloader:加载动态生成的代理类的类加载器
        // 2 interfaces:目标对象实现的所有接口的class对象所组成的数组
        // 3 invocationHandler:设置代理对象实现目标对象方法的过程,即代理类中如何重写接口中的抽象方法
        ClassLoader classLoader = target.getClass().getClassLoader();
        Class<?>[] interfaces = target.getClass().getInterfaces();
        InvocationHandler invocationHandler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                Object result = null;
                try {
                    System.out.println("[动态代理][日志]" + method.getName() + ",参数:" + Arrays.toString(args));
                    result = method.invoke(target, args);
                    System.out.println("[动态代理][日志]" + method.getName() + ",结果:" + result);
                } catch(Exception e) {
                    e.printStackTrace();
                    System.out.println("[动态代理][日志]" + method.getName() + ",异常:" + e.getMessage());
                } finally {
                    System.out.println("[动态代理][日志]" + method.getName() + ",方法执行完毕");
                }
                return result;
            }
        };
        return Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);
    }
}
```

## 5.2 面向切面编程思维（AOP）
### 5.2.1 面向切面编程思想 AOP
AOP（Aspect Oriented Programming）面向切面编程。  
### 5.2.2 AOP 术语名词介绍
1. 横切关注点：  

从每个方法中抽取出来的同一类非核心业务。在同一个项目中，我们开始使用多个横切关注点对相关方法进行多个不同方面的增强。  
2. 通知（增强）：  

每一个横切关注点上要做的事情都需要写一个方法来实现，这样的方法就叫通知方法。  
1. 前置通知：在被代理的目标方法前执行。  
2. 返回通知：在被代理的目标方法成功结束后执行。  
3. 异常通知：在被代理的目标方法异常结束后执行。  
4. 环绕通知：使用 try...catch...finally 结构围绕整个被代理的目标方法，包括上面四种通知对应的所有位置。  
3. 连接点 JoinPoint：  

这也是一个纯逻辑概念，不是语法定义的。  
指那些被拦截到的点。在 Spring 中，可以被动态代理拦截目标类的方法。  
4. 切入点 PointCut：  

定位连接点的方式，或者可以理解成被选中的连接点。  
是一个表达式，比如 execution()。符合条件的每个方法都是一个具体的连接点。  
5. 切面 Aspect：  

切入点和通知的结合。是一个类。  
6. 目标 Target：  

被代理的目标对象。  
7. 代理 Proxy：  

向目标对象应用通知之后创建的代理对象。  
8. 织入：  

指把通知应用到目标上，生成代理对象的过程。可以在编译期织入，也可以在运行期织入，Spring 采用后者。  
## 5.3 Spring AOP 框架介绍和关系梳理
1. AOP 一种区别于 OOP 的编程思维，用来完善和解决 OOP 的非核心代码冗余和不方便统一维护问题。  
2. 代理技术（动态代理 | 静态代理）是实现 AOP 思维编程的具体技术，但是自己使用动态代理实现代码比较繁琐。  
3. Spring AOP 框架，基于 AOP 编程思维，封装动态代理技术，简化动态代理技术实现的框架！Spring AOP 内部帮助我们实现动态代理，我们只需写少量的配置，指定生效范围即可，即可完成面向切面思维编程的实现。  

## 5.4 Spring AOP 基于注解方式实现和细节
### 5.4.1 Spring AOP 底层技术组成

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%209a44fd5c25773cfb.png)  

1. 动态代理（InvocationHandler）：JDK 原生的实现方式，需要被代理的目标类必须实现接口，因为这个技术要求代理对象和目标对象实现同样的接口。  
2. cglib：通过继承被代理的目标类实现代理，所以不需要目标类实现接口。  
3. AspectJ：早期的 AOP 实现的框架，Spring AOP 借用了 AspectJ 中的 AOP 注解。  

### 5.4.2 初步实现
1. 加入依赖：  

```xml
<!-- spring-aspects会帮我们传递过来aspectjweaver -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>6.0.6</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>6.0.6</version>
</dependency>
```

2. 准备接口：  

```java
public interface Calculator {
    int add(int i, int j);
    int sub(int i, int j);
    int mul(int i, int j);
    int div(int i, int j);
}
```

3. 纯净实现类：  

```java
@Component
public class CalculatorImpl implements Calculator {
    @Override
    public int add(int i, int j) {
        return i + j;
    }
    @Override
    public int sub(int i, int j) {
        return i - j;
    }
    @Override
    public int mul(int i, int j) {
        return i * j;
    }
    @Override
    public int div(int i, int j) {
        return i / j;
    }
}
```

4. 配置类：  

```java
@Configuration
@ComponentScan("com.prokyhoof")
@EnableAspectJAutoProxy // 开启aspectj的注解 <aop:aspectj-autoproxy/>
public class JavaConfig {
}
```

5. 增强类：  

```java
@Component
@Aspect
public class LogAdvice {
    @Before("execution(* com.prokyhoof.service.impl.*.*(..))")
    public void start() {
        System.out.println("方法开始了");
    }
}
```

### 5.4.3 获取通知细节信息
1. JoinPoint 接口：  

需要获取方法签名、传入的实参等信息时，可以在通知方法声明 JoinPoint 类型的形参。  
1. JoinPoint 接口通过 getSignature() 方法获取目标方法的签名（方法声明时的完整信息）。  
2. 通过目标方法签名对象获取方法名。  
3. 通过 JoinPoint 对象获取外界调用目标方法时传入的实参列表组成的数组。  

```java
// @Before注解标注前置通知方法
// value属性:切入点表达式,告诉Spring当前通知方法要套用哪个目标方法上
// 在前置通知方法形参位置声明一个JoinPoint类型的参数,Spring就会将这个对象传入
// 根据JoinPoint对象就可以获取目标方法名称,实际参数列表
@Before(value = "execution(public int com.prokyhoof.aop.api.Calculator.add(int, int))")
public void printLogBeforeCore(JoinPoint joinPoint) {
    // 1 通过JoinPoint对象获取目标方法签名对象
    // 方法的签名:一个方法的全部声明信息
    Signature signature = joinPoint.getSignature();
    // 2 通过方法的签名对象获取目标方法的详细信息
    String methodName = signature.getName();
    System.out.println("methodName = " + methodName);
    int modifiers = signature.getModifiers();
    System.out.println("modifiers = " + modifiers);
    String declaringTypeName = signature.getDeclaringTypeName();
    System.out.println("declaringTypeName = " + declaringTypeName);
    // 3 通过JoinPoint对象获取外界调用目标方法传入的实参列表
    Object[] argList = joinPoint.getArgs();
    // 4 由于数组直接打印看不到具体数据,所以转换为List集合
    System.out.println("[AOP前置通知]" + methodName + "方法开始了,参数列表:" + argList);
}
```

2. 方法返回值：  

在返回通知中，通过 @AfterReturning 注解的 returning 属性获取目标方法的返回值。  

```java
// @AfterReturning注解标记返回通知方法
// 在返回通知中获取目标方法返回值分两步
// 1 在@AfterReturning注解中通过returning属性设置一个名称
// 2 使用returning属性设置的名称在通知方法中声明一个对应的形参
@AfterReturning(value = "execution(public int com.prokyhoof.aop.api.Calculator.add(int, int))",
        returning = "targetMethodReturnValue")
public void printLogAfterCoreSuccess(JoinPoint joinPoint, Object targetMethodReturnValue) {
    String methodName = joinPoint.getSignature().getName();
    System.out.println("[AOP返回通知]" + methodName + "方法成功结束了,返回值是:" + targetMethodReturnValue);
}
```

3. 异常对象捕捉：  

在异常通知中，通过 @AfterThrowing 注解的 throwing 属性获取目标方法抛出异常对象。  

```java
// @AfterThrowing注解标记异常通知方法
// 在异常通知中获取目标方法抛出的异常分两步
// 1 在@AfterThrowing注解中声明一个throwing属性设定形参名称
// 2 使用throwing属性指定的名称在通知方法声明对象,Spring会将目标方法抛出的异常对象从这里传给我们
@AfterThrowing(value = "execution(public int com.prokyhoof.aop.api.Calculator.add(int, int))", throwing = "targetMethodException")
public void printLogAfterCoreException(JoinPoint joinPoint, Throwable targetMethodException) {
    String methodName = joinPoint.getSignature().getName();
    System.out.println("[AOP异常通知]" + methodName + "方法抛异常了,异常类型是:" + targetMethodException.getClass());
}
```

### 5.4.4 切点表达式语法
1. 切点表达式作用：  

AOP 切点表达式（Pointcut Expression）是一种用于指定切点的语言，它可以通过定义匹配规则，来选择需要被切入的目标对象。  
2. 切点表达式语法：  

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%2094ea0ea4238a20a2.png)  

### 5.4.5 重用（提取）切点表达式

```java
@Pointcut("execution(* com.prokyhoof.service.impl.*.*(..))")
public void pc() {}
```

### 5.4.6 环绕通知

```java
@Component
@Aspect
public class TxAroundAdvice {
    // 使用@Around注解标记环绕通知方法
    // 环绕通知方法形参位置声明ProceedingJoinPoint类型参数,代表要执行的目标方法
    @Around("com.prokyhoof.pointcut.MyPointCut.pc()")
    public Object transaction(ProceedingJoinPoint joinPoint) {
        Object[] args = joinPoint.getArgs();
        Object result = null;
        try {
            System.out.println("开启事务");
            result = joinPoint.proceed(args);
            System.out.println("结束事务");
        } catch(Throwable e) {
            System.out.println("事务回滚");
            throw new RuntimeException(e);
        } finally {
        }
        return result;
    }
}
```

### 5.4.7 切面优先级设置
相同目标方法上同时存在多个切面时，切面的优先级控制切面的内外嵌套顺序。  
1. 优先级高的切面：外面。  
2. 优先级低的切面：里面。  

使用 @Order 注解可以控制切面的优先级。  
1. @Order（较小的数）：优先级高。  
2. @Order（较大的数）：优先级低。  

# 6 Spring 声明式事务
## 6.1 声明式事务概念
### 6.1.1 编程式事务
编程式事务是指手动编写程序来管理事务，即通过编写代码的方式直接控制事务的提交和回滚，在 Java 中，通常使用事务管理器（如 Spring 中的 PlatformTransactionManager）来实现编程式事务。  
编程式事务的主要优点是灵活性高，可以按照自己的需要来控制事务的粒度、模式等等，但是，编写大量的事务控制代码容易出现问题，对代码的可读性和可维护性有一定影响。  
### 6.1.2 声明式事务
声明式事务是指使用注解或 XML 配置的方法来控制事务的提交和回滚。  
开发者只需要添加配置即可，具体事务的实现由第三方框架实现，避免我们直接进行事务操作。  
使用声明式事务可以将事务的控制和业务逻辑分离开来，提高代码的可读性和可维护性。  
区别：  
1. 编程式事务需要手动编写代码来管理事务。  
2. 而声明式事务可以通过配置文件或注解来控制事务。  

### 6.1.3 Spring 事务管理器
1. 声明式事务对应依赖：  
1. spring-tx：包含声明式事务实现的基本规定（事务管理器规范接口和事务增强等等）。  
2. spring-jdbc：包含 DataSource 方法事务管理器实现类 DataSourceTransactionManager。  
3. spring-orm：包含其他持久层框架的事务管理器实现类，例如：Hibernate/Jpa 等。  
2. 事务管理器接口 PlatformTransactionManager：  

Spring 框架中事务管理的核心接口是 PlatformTransactionManager，它定义了事务的开启、提交、回滚等基本操作。  
## 6.2 基于注解的声明式事务

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%20306cf72a75d9fe86.png)  

我们现在使用的事务管理器是 org.springframework.jdbc.datasource.DataSourceTransactionManager，将来整合 JDBC 方式、JdbcTemplate 方式、Mybatis 方式的事务实现。  
DataSourceTransactionManager 类中的主要方法：  
1. doBegin()：开启事务。  
2. doSuspend()：挂起事务。  
3. doResume()：恢复挂起的事务。  
4. doCommit()：提交事务。  
5. doRollback()：回滚事务。  

### 6.2.1 事务实现

```java
@Configuration
@ComponentScan("com.prokyhoof")
@PropertySource("classpath:jdbc.properties")
@EnableTransactionManagement // 开启事务注解的支持
public class JavaConfig {
    @Bean
    public DataSourceTransactionManager transactionManager(DataSource dataSource) {
        // 内部要进行事务的操作,基于的连接池
        DataSourceTransactionManager dataSourceTransactionManager = new DataSourceTransactionManager();
        // 需要连接池对象
        dataSourceTransactionManager.setDataSource(dataSource);
        return dataSourceTransactionManager;
    }
}
```

```java
// @Transactional
// 方法上:当前方法有事务
// 类上:类下所有方法有事务
@Service
public class StudentService {
    @Autowired
    private StudentDao studentDao;

    @Transactional
    public void changeInfo() {
        studentDao.updateAgeById(88, 1);
        int i = 1 / 0;
        studentDao.updateNameById("test2", 1);
    }
}
```

### 6.2.2 事务属性：只读
1. 只读介绍：  

对一个查询操作来说，如果我们把它设置成只读，就能够明确告诉数据库，这个操作不涉及写操作，这样数据库就能够针对查询操作来进行优化。  
2. 设置方式：  

```java
// readOnly = true把当前事务设置为只读,默认是false
@Transactional(readOnly = true)
```

3. 针对 DML 动作设置只读模式：  

会抛出下面异常：  
Caused by: java.sql...Queries leading to data modification are not allowed。  

> 注意：一般情况下，都是通过类添加注解添加事务，类下的所有方法都是事务，查询方法可以通过再次添加注解，设置为只读模式，提高效率。  

### 6.2.3 超时时间
1. 需求：  

事务在执行过程中，有可能因为遇到某些问题，导致程序卡住，从而长时间占用数据库资源，而长时间占用资源，大概率是因为程序运行出现了问题（可能是 Java 程序或 MySQL 数据库或网络连接等）。  
此时这个很可能出问题的程序应该被回滚，撤销它已做的操作，事务结束，把资源让出来，让其他正常程序可以执行。  
2. 设置超时时间：  

```java
@Service
public class StudentService {
    @Autowired
    private StudentDao studentDao;

    // timeout设置事务超时时间,单位秒,默认是-1,永不超时,不限制事务时间
    @Transactional(readOnly = false, timeout = 5)
    public void changeInfo() {
        studentDao.updateAgeById(100, 1);
        // 休眠4秒,等待方法超时
        try {
            Thread.sleep(4000);
        } catch(InterruptedException e) {
            throw new RuntimeException(e);
        }
        studentDao.updateNameById("test", 1);
    }
}
```

### 6.2.4 事务异常指定
指定异常回滚和指定异常不回滚。  
默认情况下，指定发生运行时异常（RuntimeException）事务才会回滚。  
我们可以指定 Exception 异常来控制所有异常都回滚。  

```java
@Transactional(rollbackFor = Exception.class)
public void changeInfo() throws FileNotFoundException {
    studentDao.updateAgeById(99, 1);
    new FileInputStream("xxxx");
    studentDao.updateNameById("test", 1);
}
```

### 6.2.5 事务隔离级别
1. 事务隔离级别：  

数据库事务的隔离级别是指在多个事务并发执行时，数据系统为了保证数据一致性所遵循的规定。  
1. 读未提交（Read Uncommitted）：事务可以读取未被提交的数据，容易产生脏读、不可重复读和幻读等问题，实现简单但不太安全，一般不用。  
2. 读已提交（Read Committed）：事务只能读取已经提交的数据，可以避免脏读问题，但可能引发不可重复读和幻读（推荐）。  
3. 可重复读（Repeatable Read）：在一个事务中，相同的查询将返回相同的结果集，不管其他事务对数据做了什么修改，可以避免脏读和不可重复读，但仍有幻读的问题。  
4. 串行化（Serializable）：最高的隔离级别，完全禁止了并发，只允许一个事务执行完毕之后才能执行另一个事务，可以避免以上所有问题，但效率低，不适用于高并发场景。  

```java
@Service
public class StudentService {
    private StudentDao studentDao;

    // isolation = 设置事务的隔离级别,mysql默认是repeatable read
    @Transactional(isolation = Isolation.REPEATABLE_READ)
    public void changeInfo() {
        studentDao.updateAgeById(100, 1);
    }
}
```

### 6.2.6 事务传播行为
1. 事务传播行为要研究的问题：  

```java
@Transactional
public void MethodA() {
    MethodB();
}

// 在被调用的子方法中设置传播行为,代表如何处理调用的事务。是加入,还是新事务等
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void MethodB() {}
```

2. propagation 属性：  

@Transactional 注解通过 propagation 属性设置事务的传播行为，它的默认值是 Propagation propagation() default Propagation.REQUIRED。  
propagation 属性的可选值由 org.springframework.transaction.Propagation 枚举类提供。  

```vtable
{"rows":[[{"t":"名称","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1}],[{"t":"REQUIRED（默认值）","rs":1,"cs":1},{"t":"当前方法必须工作在事务中，如果当前线程上有已经开启的事务可用，那么就在这个事务中运行，如果当前线程上没有已经开启的事务，那么就自己开启新事务，在新事务中运行 所以当前方法有可能和其他方法共用事务 在共用事务的情况下：当前方法会因为其他方法回滚而受连累","rs":1,"cs":1}],[{"t":"REQUIRES_NEW","rs":1,"cs":1},{"t":"当前方法必须工作在事务中 不管当前线程上是否有已经开启的事务，都要开启新事务 在新事务中运行 不会和其他方法共用事务，避免被其他方法连累","rs":1,"cs":1}]]}
```

> 注意：在同一个类中，对于 @Transactional 注解的方法调用，事务传播行为不会生效。这是因为 Spring 框架中使用代理模式实现事务机制，在同一个类中的方法调用并不经过代理，而是通过对象的方法调用，因此 @Transactional 注解的设置不会被代理捕获，也就不会产生任何事务传播行为的效果。  
