---
tags:
  - knowledge
introduction: ssm 基础
start_date: 2026-10-15
---

# 1 Maven
## 1-1 简介和入门
### 1-1-1 Maven 介绍
Maven 就是个款为 Java 项目构建管理、依赖管理的工具（软件），使用 Maven 可以自动化构建、测试、打包和发布项目，大大提高了开发效率和质量。  
### 1-1-2 Maven 主要作用理解
1. 场景概念：  
   1. 将需要的依赖的信息编写到 Maven 工程的配置文件，Maven 软件就会自动下载并复制这些依赖项到项目中，也会自动下载依赖需要的依赖。确保依赖版本正确无冲突和依赖完整。  
   2. 通过个行构建命令（mvn package）快速项目构建和打包。  
2. 依赖管理：Maven 可以管理项目的依赖，包括自动下载所需依赖库、自动下载依赖需要的依赖并且保证版本没有冲突、依赖版本管理等。  
3. 构建管理：项目构建是指将源代码、配置文件、资源文件等转化为能够运行或部署的应用程序或库的过程。  

Maven 仓库分为本地仓库、中央仓库和私服（远程仓库）三类，依赖的查找顺序是：本地仓库 → 私服 → 中央仓库。  
## 1-2 基于 IDEA 的 Maven 工程创建
### 1-2-1 梳理 Maven 工程 GAVP 属性
Maven 中的 GAVP 是指 Group、ArtifactId、Version、Packaging 等四个属性的缩写。GAV 需要我们在创建项目时指定，P 有默认值，后期通过配置文件修改。有了具体的标识，方便 Maven 软件对项目进行管理和互相引用。  
GAV 遵循以下规则：  
1. GroupID 格式：com.{公司/BU}.业务线.[子业务线]，最多四级。  

   例：com.taobao.tddl、com.alibaba.sourcing.multilang。  
2. ArtifactID 格式：产品线名-模块名。  

   例：tc-client、uic-api、tair-tool、bookstore。  
3. Version 版本号格式推荐：主版本号.次版本号.修订号。  
   1. 主版本号：当做了不兼容的 API 修改，或者增加了能修改产品方向的新功能。  
   2. 次版本号：当做了向下兼容的功能新增（新增类、接口等）。  
   3. 修订号：修复 bug、没有修改方法签名的功能加强，保持 API 兼容性。  

   例：初始 - 1.0.0、修改 - 1.0.1、功能调整 - 1.1.1 等。  
Packaging 定义规则：  
指示将项目打包为什么类型的文件，IDEA 根据 Packaging 值，识别 maven 项目类型。  
- packaging 属性为 jar（默认值），代表普通的 Java 工程，打包以后是 .jar 结尾的文件。  
- packaging 属性为 war，代表 Java 的 Web 工程，打包以后 .war 结尾的文件。  
- packaging 属性为 pom，代表不会打包，用来做继承的父工程。  

### 1-2-2 IDEA 构建 Maven

> 注意：此处省略了 Version，直接给了一个默认值 `<version>1.0-SNAPSHOT</version>`。  
> 手动创建 Web 项目：  
> 1. 创建一个 JavaSE Maven 工程。  
> 2. 补全文件结构 main、webapp、WEB-INF、web.xml。  
> 3. pom.xml 中 packaging 改为 war。  
> 4. 刷新。  
> JBL 插件创建 Web 项目：  
> 1. 安装 JBL 插件。  
> 2. 创建一个 JavaSE Maven 工程。  
> 3. Maven 工程 - 右键 - JBLJavaToWeb。  

## 1-3 Maven 核心功能依赖和构建管理
### 1-3-1 依赖管理和配置
通过定义 POM 文件，Maven 能够自动解析项目的依赖关系，并通过 Maven 仓库自动下载和管理依赖，从而避免了手动下载和管理依赖的繁琐工作和可能引发的版本冲突问题。  
### 1-3-2 依赖传递和冲突
当我们引入一个库或框架时，构建工具（Maven、Gradle）会自动解析和加载其所有的直接和间接依赖，确保这些依赖都可用。  
1. 减少重复依赖。  
2. 自动管理依赖。  
3. 确保依赖版本正确性。  

依赖传递：导入依赖，会自动导入依赖的依赖（compile 依赖），简化依赖的导入，确保依赖的根本无冲突。  
依赖冲突：发现已经存在依赖（重复依赖）会终止依赖传递！避免循环依赖和重复依赖的问题！  
依赖冲突发生场景：重复依赖！  
### 1-3-3 依赖导入失败场景和解决方案
问题：  
1. 下载依赖时出现网络故障或仓库服务器宕机等原因，导致无法连接至 Maven 仓库，从而无法下载依赖。  
2. 依赖项的版本号或配置文件中的版本号错误，或者依赖项没有正确定义，导致 Maven 下载的依赖项目与实际需要的不个致，从而引发错误。  
3. 本地 Maven 仓库或缓存被污染或损坏，导致 Maven 无法正确地使用现有的依赖项，并且也无法重新下载。  

解决方案：  
1. 检查网络连接和 Maven 仓库服务器状态。  
2. 确保依赖项的版本号与项目对应的版本号匹配，并检查 POM 文件中的依赖项是否正确。  
3. 清除本地 Maven 仓库缓存（lastUpdated 文件），因为只要存在 lastUpdated 缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的 gav 属性依次向下查看文件夹，最终删除内部的文件，刷新重新下载即可。  

### 1-3-4 扩展构建管理和插件配置
构建的概念：项目构建是指将源代码、依赖库和资源文件等转换成可执行或可部署的应用程序的过程，在这个过程中包括编译源代码、链接依赖库、打包和部署等多个步骤。  
清理 - 编译 - 测试 - 报告 - 打包 - 部署。  
1. 命令方式构建：  
   - mvn clean：清理编译或打包后端的项目结构、删除 target 文件夹。  
   - mvn compile：编译项目，生成 target 文件。  
   - mvn test：执行测试源码（测试）。  
   - mvn site：生成一个项目依赖信息的展示页面。  
   - mvn package：打包项目，生成 war/jar 文件。  
   - mvn install：打包后上传到 maven 本地仓库（本地部署）。  
   - mvn deploy：只打包，上传到 maven 私服仓库（私有部署）。  

> 注意：  
> 1. 命令执行需要我们进入到项目的根路径 pom.xml 平级目录。  
> 2. 部署必须是 jar 包形式。  

2. 可视化方式构建：  

构建命令周期：简化触发构建命令过程，有序的构建命令容器（触发周期后的命令会自动触发同个周期的命令）。  
导入插件的格式：  

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.2</version>
        </plugin>
    </plugins>
</build>
```

构建命令周期可以理解成是个组固定构建命令的有序集合，触发周期后的命令，会自动触发周期前的命令！也是个种简化构建的思路！  
1. 清理周期：主要是对项目编译生成文件进行清理 clean。  
2. 默认周期：定义了真正构建时所需执行的所有步骤，它是生命周期中最核心的部分 compile - test - package - install/deploy。  
3. 报告周期：site。  

打包：mvn clean package。  
本地仓库：mvn clean install。  

```bash
// 最佳使用方法
// 打包
mvn clean package
// 重新编译
mvn clean compile
// 本地部署
mvn clean install
```

周期、命令和插件：  
周期 - 包含若干命令 - 包含若干插件。  
使用周期命令构建、简化构建过程。  
最终进行构建的是插件。  
## 1-4 Maven 继承和聚合特性
### 1-4-1 Maven 工程继承关系
1. 继承概念：  

Maven 继承是指在 Maven 的项目中，让一个项目从另一个项目中继承配置信息的机制。继承可以让我们在多个项目中共享同一个配置信息，简化项目的管理和维护工作。  
2. 继承作用：  

作用：在父工程中统一管理项目中的依赖信息，进行统一版本管理。  
它的背景是：  
1. 对一个比较大型的项目进行了模块拆分。  
2. 一个 project 下面，创建了很多个 module。  
3. 每一个 module 都需要配置自己的依赖信息。  

它背后的需求是：  
1. 多个模块要使用同一个框架，它们应该是同一个版本，所以整个项目中使用的框架版本需要统一管理。  
2. 使用框架时所需要的 jar 包组合（或者说依赖信息组合）需要经过长期摸索和反复调试，最终确定一个可用组合，这个耗费很大精力总结出来的方案不应该在新的项目中重新摸索。  

通过在父工程中为整个项目维护依赖信息的组合，既保证了整个项目使用规范、准确的 jar 包，又能够将以往的经验沉淀下来，节约时间和精力。  
3. 继承语法：  

```xml
<!-- 父工程 pom.xml -->
<!-- 父工程不打包,也不写代码 -->
<packaging>pom</packaging>

<!-- 声明版本信息 -->
<!-- 导入依赖 此处导入,所有子工程都有相应的依赖 -->
<dependencies>
    ...
</dependencies>

<!-- 声明依赖,不会下载依赖,可以被子工程继承版本号 -->
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>...</groupId>
            <artifactId>...</artifactId>
            <version>...</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

```xml
<!-- 子工程 pom.xml -->
<!-- parent标签就是来指定继承父工程的gav属性 -->
<!-- g v属性也继承父工程,可以自己定义 -->
<parent>
    <groupId>...</groupId>
    <artifactId>...</artifactId>
    <version>...</version>
</parent>
<dependencies>
    <dependency>
        <groupId>...</groupId>
        <artifactId>...</artifactId>
    </dependency>
</dependencies>
```

### 1-4-2 Maven 工程聚合关系
1. 聚合概念：  

Maven 聚合是指将多个项目组织到一个父级项目中，通过被触发父工程的构建统一按顺序触发子工程构建的过程。  
2. 聚合作用：  
   1. 统一管理子项目构建：通过聚合，可以将多个子项目组织在一起，方便管理和维护。  
   2. 优化构建顺序：通过聚合，可以对多个项目进行顺序控制，避免出现构建依赖混乱导致构建失败的情况。  
3. 聚合语法：  

```xml
<!-- 要统一管理哪些子工程的artifactId -->
<modules>
    <module>子工程1</module>
    <module>子工程2</module>
</modules>
```

# 2 SpringFramework
## 2-1 技术体系结构
### 2-1-1 总体技术体系
1. 单一架构：  

一个项目，一个工程，导出为一个 war 包，在一个 Tomcat 上运行。也叫 all in one。  
单一架构，项目主要应用技术框架：Spring、SpringMVC、Mybatis。  

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%20840dff07f8853363.png)  

2. 分布式架构：  

一个项目（对应 IDEA 中的一个 project），拆分成很多个模块，每个模块是一个 IDEA 中的一个 module，每一个工程都是运行在自己的 Tomcat 上，模块之间可以互相调用，每一个模块内部可以看成是一个架构的应用。  
分布式架构、项目主要应用技术框架：SpringBoot（SSM）、SpringCloud，中间件等。  
### 2-1-2 框架概念和理解
框架（Framework）是一个集成了基本结构、规范、设计模式、编程语言和程序库等基础组件的软件系统，它可以用来构建更高级别的应用程序。框架的设计和实现旨在解决特定领域中的常见问题，帮助开发人员更高效、更稳定地实现软件开发目标。  
框架的优点包括以下几点：  
1. 提高开发效率。  
2. 降低开发成本。  
3. 提高应用程序的稳定性。  
4. 提高标准化的解决方案。  

站在文件结构的角度理解框架，可以将框架总结：框架 = jar包 + 配置文件。  
常见的单一框架 JavaEE 项目框架演进，从 SSH、SSH2 过渡到了 SSM：SpringMVC、Spring、MyBatis。  
## 2-2 SpringFramework 介绍
### 2-2-1 Spring 和 SpringFramework 概念
Spring 技术栈（全家桶）：广义上的 Spring 泛指以 SpringFramework 为基础的 Spring 技术栈。  
SpringFramework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。  
SpringFramework（基础框架）：狭义上的 Spring 特指 Spring Framework，通常将它称为 Spring 框架。  
### 2-2-2 SpringFramework 主要功能模块
Core Container：核心容器，在 Spring 环境下使用任何功能都必须基于 IoC 容器。  
AOP & Aspects：面向切面编程。  
TX：声明式事务管理。  
SpringMVC：提供了面向 Web 应用程序的集成功能。  
### 2-2-3 SpringFramework 主要优势
1. 丰富的生态系统。  
2. 模块化的设计。  
3. 简化 Java 开发。  
4. 不断创新和发展。  

## 2-3 Spring IoC 容器和核心概念
### 2-3-1 组件和组件管理概念
#### 2-3-1-1 什么是组件
Controller：控制层组件。  
Service：业务逻辑层组件。  
Dao：持久化层组件。  
#### 2-3-1-2 Spring 充当组件管理角色（IoC）
组件可以完全交给 Spring 框架进行管理，Spring 框架替代了程序员原有的 new 对象和对象属性赋值等动作。  

> 注意：组件是映射到应用程序中所有可重用组件的 Java 对象，应该是可复用的功能对象。  
> 1. 组件一定是对象。  
> 2. 对象不一定是组件。  

#### 2-3-1-3 组件交给 Spring 管理优势
1. 降低了组件之间的耦合性。  
2. 提高了代码的可重用性和可维护性。  
3. 方便了配置和管理。  
4. 交给 Spring 管理的对象（组件），方可享受 Spring 框架的其他功能（AOP、声明式事务管理）等。  

### 2-3-2 Spring IoC 容器和容器实现
#### 2-3-2-1 普通和复杂容器
普通容器：数组、集合 List、集合 Set。  
复杂容器：Servlet 容器能够管理 Servlet（init、service、destroy）、Filter、Listener 这样的组件的一生，所以它是一个复杂容器。  

```vtable
{"rows":[[{"t":"阶段","rs":1,"cs":1},{"t":"触发时机","rs":1,"cs":1},{"t":"次数","rs":1,"cs":1}],[{"t":"创建对象","rs":1,"cs":1},{"t":"默认情况：接收到第一次请求 修改启动顺序后：Web应用启动过程中","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}],[{"t":"初始化操作","rs":1,"cs":1},{"t":"创建对象之后","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}],[{"t":"处理请求","rs":1,"cs":1},{"t":"接收到请求","rs":1,"cs":1},{"t":"多次","rs":1,"cs":1}],[{"t":"销毁操作","rs":1,"cs":1},{"t":"Web应用卸载之前","rs":1,"cs":1},{"t":"一次","rs":1,"cs":1}]]}
```

总结：Spring 管理组件的容器，就是一个复杂容器，不仅存储组件，也可以管理组件之间依赖关系，并且创建和销毁组件等。  
#### 2-3-2-2 Spring IoC 容器介绍
Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系。  
#### 2-3-2-3 Spring IoC 容器具体接口和实现类
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
### 2-3-3 Spring IoC/DI 概念总结
#### 2-3-3-1 IoC 容器
Spring IoC 容器，负责实例化、配置和组装 bean（组件）核心容器。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。  
#### 2-3-3-2 IoC（Inversion of Control）控制反转
IoC 主要是针对对象的创建和调用控制而言的，也就是说，当应用程序需要使用一个对象时，不再是应用程序直接创建该对象，而是由 IoC 容器来创建和管理，即控制权由程序转移到 IoC 容器中，也就是"反转"了控制权。  
这种方式基本上是通过依赖查找的方式来实现的，即 IoC 容器维护着构成应用程序的对象，并负责创建这些对象。  
#### 2-3-3-3 DI（Dependency Injection）依赖注入
DI 是指在组件之间传递依赖关系的过程中，将依赖关系在容器内部进行处理，这样就不必在应用程序代码中硬编码对象之间的依赖关系，实现了对象之间的解耦合，在 Spring 中，DI 是通过 XML 配置文件或注解的方式实现的。  
它提供了三种形式的依赖注入：构造函数注入、Setter 方法注入和接口注入。  
## 2-4 Spring IoC 实践和应用
### 2-4-1 Spring IoC/DI 实现步骤
#### 2-4-1-1 基于 XML 的 IoC 配置
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

#### 2-4-1-2 依赖注入配置 DI
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

#### 2-4-1-3 IoC 容器创建和使用
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

#### 2-4-1-4 组件（Bean）作用域和周期方法配置
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

#### 2-4-1-5 FactoryBean 特征和使用
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
#### 2-4-1-6 基于 XML 方式整合三层架构组件
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

### 2-4-2 基于注解方式管理 Bean
#### 2-4-2-1 注解理解
和 XML 配置文件一样，注解本身并不能执行，注解本身仅仅只是做一个标记，具体的功能是框架检测到注解标记的位置，然后针对这个位置按照注解标记的功能来执行具体操作。  
本质上，所有一切的操作都是 Java 代码来完成的，XML 和注解只是告诉框架中的 Java 代码如何执行。  
#### 2-4-2-2 扫描理解
Spring 为了知道程序员在哪些地方标记了什么注解，就需要通过扫描的方式，来进行检测。然后根据注解进行后续操作。  
#### 2-4-2-3 准备 Spring 项目和组件
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

#### 2-4-2-4 组件添加标记注解
1. 组件标记注解和区别：  

Spring 提供了以下多个注解，这些注解可以直接标注在 Java 类上，将它们定义成 SpringBean。  

```vtable
{"rows":[[{"t":"注解","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"@Component","rs":1,"cs":1},{"t":"该注解用于描述Spring中的Bean，它是一个泛化的概念，仅仅表示容器中的一个组件（Bean），并且可以作用在引用的任何层次，例如Service层、Dao层等，使用时只需将注解标注在相应类上即可","rs":1,"cs":1}],[{"t":"@Repository","rs":1,"cs":1},{"t":"该注解用于将数据访问层（Dao层）的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}],[{"t":"@Service","rs":1,"cs":1},{"t":"该注解通常作用在业务层（Service层），用于将业务层的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}],[{"t":"@Controller","rs":1,"cs":1},{"t":"该注解通常作用在控制层（Controller层），用于将控制层的类标识为Spring中的Bean，其功能与@Component相同","rs":1,"cs":1}]]}
```

@Controller、@Service、@Repository 这三个注解只是在 @Component 注解的基础上起了三个新的名字。  
对于 Spring 使用 IoC 容器管理这些组件来说没有区别，也就是语法层面没有区别，所以 @Controller、@Service、@Repository 这三个注解只是给开发人员看的，让我们能够便于分辨组件的作用。  

> 注意：虽然他们本质上一样，但是为了代码的可读性，程序结构严谨，不能乱标记。  

#### 2-4-2-5 配置文件确定扫描范围
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

#### 2-4-2-6 组件 BeanName 问题
在我们使用 XML 方式管理 Bean 的时候，每个 Bean 都有一个唯一标识——id 属性的值，便于在其他地方引用，现在使用注解后，每个组件仍然应该有一个唯一标识。  
默认情况：  
类名首字母小写就是 Bean 的 id。例如：SoldierController 类对应的 Bean 的 id 就是 soldierController。  
使用 value 属性指定：  

```java
@Controller(value = "tianDog")
public class SoldierController {}
```

当注解中只设置一个属性时，value 属性的属性名可以省略。  
#### 2-4-2-7 组件（Bean）作用域和周期方法注解
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

#### 2-4-2-8 Bean 属性赋值：引用类型自动装配（DI）
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

#### 2-4-2-9 Bean 属性赋值：基本类型属性赋值（DI）
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

### 2-4-3 基于配置类方法管理 Bean
#### 2-4-3-1 完全注解开发理解
Spring 完全注解配置（Fully Annotation-based Configuration）是指通过 Java 配置类代码来配置 Spring 应用程序，使用注解来替代原本在 XML 配置文件中的配置，相对于 XML 配置，完全注解配置具有更强的类型安全性和更好的可读性。  
#### 2-4-3-2 配置类和扫描注解

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
#### 2-4-3-3 @Bean 定义组件

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

#### 2-4-3-4 高级特性：@Bean 注解细节
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
#### 2-4-3-5 高级特性：@Import 扩展
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
### 2-4-4 三种配置方式总结
#### 2-4-4-1 XML 方式配置总结
1. 所有内容写到 xml 格式配置文件中。  
2. 声明 bean 通过 `<bean>` 标签。  
3. `<bean>` 标签包含基本信息（id、class）和属性信息 `<property name value/ref>`。  
4. 引入外部的 properties 文件可以通过 `<context:property-placeholder>`。  
5. IoC 具体容器实现选择 ClassPathXmlApplicationContext 对象。  

#### 2-4-4-2 XML + 注解方式配置总结
1. 注解负责标记 IoC 的类和进行属性装配。  
2. xml 文件依然需要，需要通过 `<context:component-scan>` 标签指定注解范围。  
3. 标记 IoC 注解：@Component、@Service、@Controller、@Repository。  
4. 标记 DI 注解：@Autowired、@Qualifier、@Resource、@Value。  
5. IoC 具体容器实现选择 ClassPathXmlApplicationContext 对象。  

#### 2-4-4-3 完全注解方式配置总结
1. 完全注解方式指的是去掉 xml 文件，使用配置类 + 注解实现。  
2. xml 文件替换成使用 @Configuration 注解标记的类。  
3. 标记 IoC 注解：@Component、@Service、@Controller、@Repository。  
4. 标记 DI 注解：@Autowired、@Qualifier、@Resource、@Value。  
5. `<context:component-scan>` 标签指定注解范围使用 @ComponentScan(basePackages = {"com.prokyhoof.components"}) 替代。  
6. `<context:property-placeholder>` 引入外部配置文件使用 @PropertySource({"classpath:application.properties", "classpath:jdbc.properties"}) 替代。  
7. `<bean>` 标签使用 @Bean 注解和方法实现。  
8. IoC 具体容器实现选择 AnnotationConfigApplicationContext 对象。  

### 2-4-5 整合 Spring5-Junit5 搭建测试环境
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

## 2-5 Spring AOP 面向切面编程
### 2-5-1 解决技术代理模式
#### 2-5-1-1 代理模式
二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类间接调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——解耦。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。  
#### 2-5-1-2 静态代理
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
#### 2-5-1-3 动态代理
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

### 2-5-2 面向切面编程思维（AOP）
#### 2-5-2-1 面向切面编程思想 AOP
AOP（Aspect Oriented Programming）面向切面编程。  
#### 2-5-2-2 AOP 术语名词介绍
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
### 2-5-3 Spring AOP 框架介绍和关系梳理
1. AOP 一种区别于 OOP 的编程思维，用来完善和解决 OOP 的非核心代码冗余和不方便统一维护问题。  
2. 代理技术（动态代理 | 静态代理）是实现 AOP 思维编程的具体技术，但是自己使用动态代理实现代码比较繁琐。  
3. Spring AOP 框架，基于 AOP 编程思维，封装动态代理技术，简化动态代理技术实现的框架！Spring AOP 内部帮助我们实现动态代理，我们只需写少量的配置，指定生效范围即可，即可完成面向切面思维编程的实现。  

### 2-5-4 Spring AOP 基于注解方式实现和细节
#### 2-5-4-1 Spring AOP 底层技术组成

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%209a44fd5c25773cfb.png)  

1. 动态代理（InvocationHandler）：JDK 原生的实现方式，需要被代理的目标类必须实现接口，因为这个技术要求代理对象和目标对象实现同样的接口。  
2. cglib：通过继承被代理的目标类实现代理，所以不需要目标类实现接口。  
3. AspectJ：早期的 AOP 实现的框架，Spring AOP 借用了 AspectJ 中的 AOP 注解。  

#### 2-5-4-2 初步实现
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

#### 2-5-4-3 获取通知细节信息
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

#### 2-5-4-4 切点表达式语法
1. 切点表达式作用：  

AOP 切点表达式（Pointcut Expression）是一种用于指定切点的语言，它可以通过定义匹配规则，来选择需要被切入的目标对象。  
2. 切点表达式语法：  

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%2094ea0ea4238a20a2.png)  

#### 2-5-4-5 重用（提取）切点表达式

```java
@Pointcut("execution(* com.prokyhoof.service.impl.*.*(..))")
public void pc() {}
```

#### 2-5-4-6 环绕通知

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

#### 2-5-4-7 切面优先级设置
相同目标方法上同时存在多个切面时，切面的优先级控制切面的内外嵌套顺序。  
1. 优先级高的切面：外面。  
2. 优先级低的切面：里面。  

使用 @Order 注解可以控制切面的优先级。  
1. @Order（较小的数）：优先级高。  
2. @Order（较大的数）：优先级低。  

## 2-6 Spring 声明式事务
### 2-6-1 声明式事务概念
#### 2-6-1-1 编程式事务
编程式事务是指手动编写程序来管理事务，即通过编写代码的方式直接控制事务的提交和回滚，在 Java 中，通常使用事务管理器（如 Spring 中的 PlatformTransactionManager）来实现编程式事务。  
编程式事务的主要优点是灵活性高，可以按照自己的需要来控制事务的粒度、模式等等，但是，编写大量的事务控制代码容易出现问题，对代码的可读性和可维护性有一定影响。  
#### 2-6-1-2 声明式事务
声明式事务是指使用注解或 XML 配置的方法来控制事务的提交和回滚。  
开发者只需要添加配置即可，具体事务的实现由第三方框架实现，避免我们直接进行事务操作。  
使用声明式事务可以将事务的控制和业务逻辑分离开来，提高代码的可读性和可维护性。  
区别：  
1. 编程式事务需要手动编写代码来管理事务。  
2. 而声明式事务可以通过配置文件或注解来控制事务。  

#### 2-6-1-3 Spring 事务管理器
1. 声明式事务对应依赖：  
1. spring-tx：包含声明式事务实现的基本规定（事务管理器规范接口和事务增强等等）。  
2. spring-jdbc：包含 DataSource 方法事务管理器实现类 DataSourceTransactionManager。  
3. spring-orm：包含其他持久层框架的事务管理器实现类，例如：Hibernate/Jpa 等。  
2. 事务管理器接口 PlatformTransactionManager：  

Spring 框架中事务管理的核心接口是 PlatformTransactionManager，它定义了事务的开启、提交、回滚等基本操作。  
### 2-6-2 基于注解的声明式事务

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringFramework%20image%20306cf72a75d9fe86.png)  

我们现在使用的事务管理器是 org.springframework.jdbc.datasource.DataSourceTransactionManager，将来整合 JDBC 方式、JdbcTemplate 方式、Mybatis 方式的事务实现。  
DataSourceTransactionManager 类中的主要方法：  
1. doBegin()：开启事务。  
2. doSuspend()：挂起事务。  
3. doResume()：恢复挂起的事务。  
4. doCommit()：提交事务。  
5. doRollback()：回滚事务。  

#### 2-6-2-1 事务实现

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

#### 2-6-2-2 事务属性：只读
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

#### 2-6-2-3 超时时间
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

#### 2-6-2-4 事务异常指定
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

#### 2-6-2-5 事务隔离级别
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

#### 2-6-2-6 事务传播行为
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

# 3 MyBatis
## 3-1 MyBatis 简介
### 3-1-1 简介
MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。  
### 3-1-2 快速入门
1. 依赖导入 pom.xml：  

```xml
<dependencies>
    <!-- mybatis依赖 -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.11</version>
    </dependency>
    <!-- MySQL驱动 MyBatis底层依赖JDBC驱动实现,本次不需要导入连接池,MyBatis自带 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.25</version>
    </dependency>
</dependencies>
```

2. 实体类准备：  

```java
public class Employee {
    private Integer empId;
    private String empName;
    private Double empSalary;
    // getter/setter
}
```

3. 准备 Mapper 接口和 Mapper.xml 文件：  

MyBatis 框架下，SQL 语句编写位置发生改变，从原来的 Java 类，改成 XML 或注解定义。  
推荐在 XML 文件中编写 SQL 语句，让用户能更专注于 SQL 代码，不用关注其他的 JDBC 代码。  
MyBatis 中的 Mapper 接口相当于以前的 Dao，但是区别在于，Mapper 仅仅只是建接口即可，我们不需要提供实现类，具体的 SQL 写到对应的 Mapper 文件。  

```java
public interface EmployeeMapper {
    Employee queryById(Integer id);
}
```

```xml
<!-- namespace = mapper对应接口的全限定名 -->
<mapper namespace="com.prokyhoof.mapper.EmployeeMapper">
    <select id="queryById" resultType="com.prokyhoof.pojo.Employee">
        select emp_id empId, emp_name empName, emp_salary empSalary from t_emp where emp_id = #{id}
    </select>
</mapper>
```

> 注意：  
> 1. 方法名和 SQL 的 id 一致。  
> 2. 方法返回值和 resultType 一致。  
> 3. 方法的参数和 SQL 的参数一致。  
> 4. 接口的全类名和映射配置文件的名称空间（namespace）一致。  

4. 准备 MyBatis 配置文件：  

MyBatis 框架配置文件：数据库连接信息，性能配置，mapper.xml 配置等。  
习惯上命名为 mybatis-config.xml，这个文件名仅仅只是建议，并非强制要求。将来整合 Spring 之后，这个配置文件可以省略。  

```java
public class MyBatisTest {
    @Test
    public void testSelectEmployee() throws IOException {
        // 1 创建SqlSessionFactory对象
        // 声明MyBatis全局配置文件的路径
        String mybatisConfigFilePath = "mybatis-config.xml";
        // 以输入流的形式加载MyBatis配置文件
        InputStream inputStream = Resources.getResourceAsStream(mybatisConfigFilePath);
        // 基于读取mybatis配置文件的输入流创建SqlSessionFactory对象
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        // 2 使用SqlSessionFactory对象开启一个会话
        SqlSession session = sessionFactory.openSession();
        // 3 根据EmployeeMapper接口的Class对象获取Mapper接口类型的对象(动态代理技术)
        // jdk动态代理技术生成的mapper代理对象
        EmployeeMapper employeeMapper = session.getMapper(EmployeeMapper.class);
        // 4 调用代理类方法即可以触发对应的SQL语句
        // 内部拼接接口的全限定名.方法名,去查找SQL语句标签,整合参数传入对应的方法
        Employee employee = employeeMapper.queryById(1);
        System.out.println("employee = " + employee);
        // 5 关闭SqlSession
        session.commit(); // 提交事务,DQL不需要,其他需要
        session.close(); // 关闭会话
    }
}
```

## 3-2 MyBatis 基本使用
### 3-2-1 向 SQL 语句传参
#### 3-2-1-1 MyBatis 日志输出配置
[MyBatis 3 | 配置 - mybatis](https://mybatis.org/mybatis-3/zh_CN/configuration.html)  
#### 3-2-1-2 #{} 形式

```xml
<mapper namespace="com.prokyhoof.mapper.EmployeeMapper">
    <!-- #{key} 占位符+赋值 -->
    <!-- ${key} 字符串拼接 -->
    <select id="queryById" resultType="com.prokyhoof.pojo.Employee">
        SELECT emp_id empId, emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_id = #{id};
    </select>
</mapper>
```

#### 3-2-1-3 ${} 形式
#{} 使用预编译占位符，会为参数自动添加引号，可以防止 SQL 注入，是推荐的使用方式。  
${} 是字符串拼接，直接将参数值拼接到 SQL 语句中，存在 SQL 注入风险。  

> 注意：需要动态传入列名、排序字段等无法使用占位符的场景，才使用 ${}，且必须对传入值做好校验。  

### 3-2-2 数据输入
#### 3-2-2-1 MyBatis 总体机制概括

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/MyBatis%20image%204e7b1b89566d2e5b.png)  
  
#### 3-2-2-2 概念说明
这里数据输入具体是指上层方法（例如 Service 方法）调用 Mapper 接口时，数据传入的形式。  
1. 简单类型：只包含一个值的数据类型。  
   1. 基本数据类型：int、byte、short、double。  
   2. 基本数据类型的包装类型：Integer、Character、Double。  
   3. 字符串类型：String。  
2. 复杂类型：包含多个值的数据类型。  
   1. 实体类类型：Employee、Department。  
   2. 集合类型：List、Set、Map。  
   3. 数组类型：int[]、String[]。  
   4. 复合类型：`List<Employee>`、实体类中包含集合。  

#### 3-2-2-3 单个简单类型参数
Mapper 接口中抽象方法的声明：  

```java
Employee selectEmployee(Integer empId);
```

SQL 语句：  
```xml
<select id="selectEmployee" resultType="com.prokyhoof.pojo.Employee">
    SELECT emp_id empId, emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_id = #{id};
</select>
```

单个简单类型参数，在 #{} 中可以随意命名，但是没有必要，通常还是使用和接口方法参数同名。  
#### 3-2-2-4 实体类类型参数

```java
int insertEmp(Employee employee);
```

```xml
<insert id="insertEmp">
    insert into t_emp(emp_name, emp_salary) value (#{empName}, #{empSalary});
</insert>
```

#### 3-2-2-5 零散的简单类型数据

```java
List<Employee> queryByNameAndSalary(@Param("name")String name, @Param("salary")double salary);
```

```xml
<select id="queryByNameAndSalary" resultType="com.prokyhoof.pojo.Employee">
    SELECT emp_id empId, emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_name = #{name} AND emp_salary = #{salary};
</select>
```

> 注意：当方法参数是多个时，必须使用 @Param 注解为每个参数指定名称，#{} 中才能通过该名称取值。  

#### 3-2-2-6 Map 的简单类型数据

```java
int updateEmployeeByMap(Map<String, Object> paramMap);
```

```xml
<update id="updateEmployeeByMap">
    UPDATE t_emp SET emp_salary = #{empSalaryKey} WHERE emp_id = #{empIdKey}
</update>
```

#{} 中的 key 对应 Map 集合中的键名。  
### 3-2-3 数据输出
#### 3-2-3-1 输出概述
数据输出总体上有两种形式：  
1. 增删改查操作返回的受影响行数，直接使用 int 或 long 类型接收即可。  
2. 查询操作的查询结果。  

#### 3-2-3-2 单个简单类型

``` java
int deleteById(Integer id);
// 指定输出类型,查询语句
// 根据员工的id查询员工的姓名
String queryNameById(Integer id);
// 根据员工的id查询员工的工资
Double querySalaryById(Integer id);
```

```xml
<!-- 返回单个简单类型如何指定
     1 类的全限定名
     2 MyBatis提供了72种默认的别名 -->
<!-- Java的常用数据类型
     1 基本数据类型:int double -> _int _double
     2 包装数据类型:Integer Double -> integer double
     3 集合容器类型:Map List HashMap -> map list hashmap -->
<mapper namespace="com.prokyhoof.mapper.EmployeeMapper">
    <delete id="deleteById" resultType="java.lang.Integer">
        DELETE FROM t_emp WHERE emp_id = #{id};
    </delete>
    <select id="queryNameById" resultType="java.lang.String">
        SELECT emp_name empName FROM t_emp WHERE emp_id = #{id};
    </select>
    <select id="querySalaryById" resultType="java.lang.Double">
        SELECT emp_salary empSalary FROM t_emp WHERE emp_id = #{id};
    </select>
</mapper>
```

定义自己类的别名：  

```xml
<!-- 单独定义 -->
<typeAliases>
    <typeAlias type="com.prokyhoof.pojo.Employee" alias="prokyhoof"/>
</typeAliases>
<!-- 批量定义:批量将包下的类给予别名,别名就是类的首字母小写 -->
<typeAliases>
    <package name="com.prokyhoof.pojo"/>
</typeAliases>
```

```java
// 注释定义
@Alias("prokyhoof")
```

```xml
<!-- 在全局范围内对MyBatis进行配置 -->
<settings>
    <!-- 具体配置
         从org.apache.ibatis.session.Configuration类中可以查看能使用的配置项
         将mapUnderscoreToCamelCase属性配置为true,表示开启自动映射驼峰式命名规则 -->
    <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

#### 3-2-3-3 返回 Map 类型
适用于 SQL 查询返回的各个字段综合起来并不和任何一个现有的实体类对应，没法封装到实体类对象中。能够封装成实体类类型的，就不使用 Map 类型。  
Mapper 接口的抽象方法：  

```java
Map<String, Object> selectEmpNameAndMaxSalary();
```

SQL 语句：  

```xml
<!-- Map<String, Object> selectEmpNameAndMaxSalary();
     返回工资最高的员工的姓名和他的工资 -->
<select id="selectEmpNameAndMaxSalary" resultType="map">
    SELECT emp_name empName, emp_salary empSalary, (SELECT AVG(emp_salary) FROM t_emp) avgSalary FROM t_emp WHERE emp_salary = (SELECT MAX(emp_salary) FROM t_emp)
</select>
```

#### 3-2-3-4 返回 List 类型

```java
List<String> queryNameBySalary(Double salary);
List<Employee> queryAll();
```

```xml
<select id="queryNameBySalary" resultType="string">
    SELECT emp_name empName FROM t_emp WHERE emp_salary > #{salary};
</select>
<select id="queryAll" resultType="employee">
    SELECT * FROM t_emp;
</select>
```

查询多条记录时，resultType 指定集合中元素的类型即可，MyBatis 会自动将结果封装为 List。  
#### 3-2-3-5 返回主键值
1. 自增长类型主键：  

```java
int insertEmployee(Employee employee);
```

```xml
<!-- int insertEmployee(Employee employee);
     useGeneratedKeys属性字面意思就是"使用生成的主键"
     keyProperty属性可以指定主键在实体类对象中对应的属性名,MyBatis会将拿到的主键值存入 -->
<insert id="insertEmployee" useGeneratedKeys="true" keyProperty="empId">
    INSERT INTO t_emp (emp_name, emp_salary) VALUES (#{empName}, #{empSalary});
</insert>
```

> 注意：  
> 1. MyBatis 是将自增主键的值设置到实体类对象中，而不是以 Mapper 接口方法返回值的形式返回。  
> 2. 而对于不支持自增型主键的数据库（例如 Oracle）或者字符串类型主键，则可以使用 selectKey 子元素：selectKey 元素将会首先运行，id 会被设置，然后插入语句会被调用。  

```xml
<insert id="insertUser">
    <selectKey keyProperty="id" resultType="string" order="BEFORE">
        SELECT UUID() AS id;
    </selectKey>
    INSERT INTO user (id, username, password) VALUES (#{id}, #{username}, #{password});
</insert>
```

在上例中，定义了一个 insertUser 的插入语句来将 User 对象插入到 user 表中，使用 selectKey 来查询 UUID 并设置到 id 字段中。  
通过 keyProperty 属性来指定查询到的 UUID 赋值给对象中的 id 属性，而 resultType 属性指定了 UUID 的类型为 java.lang.String。  
需要注意的是，我们将 selectKey 放在了插入语句的前面，这是因为 MySQL 在 insert 语句中只支持一个 select 子句，而 selectKey 中查询 UUID 的语句就是一个 select 子句，因此我们需要将其放在前面。  
最后，再将 User 对象插入到 user 表中时，我们直接使用对象中的 id 属性来插入主键值。  
使用这种方式，我们可以方便地插入 UUID 作为字符串类型主键。当然，还有其他插入方式可以使用，如使用 Java 代码生成 UUID 并在类中显示设置值等，需要根据具体场景和需求选择合适的插入方式。  
#### 3-2-3-6 实体类属性和数据库字段的对应关系
1. 别名对应：将字段的别名设置成和实体类属性一致。  
2. 驼峰命名映射：开启 mapUnderscoreToCamelCase，将数据库下划线字段自动映射为驼峰属性。  
3. resultMap 自定义映射（id、result）：resultType 按照规则自动映射，按照是否开启驼峰式映射，自己映射属性和列名，只能映射一层结构，多表查询的时候结果无法映射。  

### 3-2-4 mapper XML 标签总结
MyBatis 的真正强大在于它的语句映射，这是它的魔力所在。由于它的异常强大，映射器的 XML 文件就显得相对简单。如果拿它跟具有相同功能的 JDBC 代码进行对比，你会立即发现省掉了将近 95% 的代码。MyBatis 致力于减少使用成本，让用户能更专注于 SQL 代码。  
1. insert：映射插入语句。  
2. update：映射更新语句。  
3. delete：映射删除语句。  
4. select：映射查询语句。  

## 3-3 MyBatis 多表映射
### 3-3-1 多表映射概念
对一：属性中包含对方对象。  
对多：属性包含对方对象集合。  
只有真实发生多表查询时，才需要设计和修改实体类，否则不提前设计和修改实体类。  
在查询映射的时候，只需要关注本次查询相关的属性。  
### 3-3-2 对一映射

```xml
<mapper namespace="com.prokyhoof.mapper.OrderMapper">
    <!-- 自定义映射关系,定义嵌套对象的映射关系 -->
    <resultMap id="orderMap" type="order">
        <!-- 第一层属性 order对象 -->
        <!-- order的主键 id标签 -->
        <id column="order_id" property="orderId"/>
        <result column="order_name" property="orderName"/>
        <result column="customer_id" property="customerId"/>
        <!-- 对象属性赋值
             property 对象属性名
             javaType 对象类型 -->
        <association property="customer" javaType="customer">
            <id column="customer_id" property="customerId"/>
            <result column="customer_name" property="customerName"/>
        </association>
    </resultMap>
    <select id="queryById" resultMap="orderMap">
        SELECT * FROM t_order tor JOIN t_customer tur ON tor.customer_id = tur.customer_id WHERE tor.order_id = #{id};
    </select>
</mapper>
```

### 3-3-3 对多映射

```xml
<mapper namespace="com.prokyhoof.mapper.CustomerMapper">
    <resultMap id="customerMap" type="customer">
        <id column="customer_id" property="customerId"/>
        <result column="customer_name" property="customerName"/>
        <collection property="orderList" ofType="order">
            <id column="order_id" property="orderId"/>
            <result column="order_name" property="orderName"/>
            <result column="customer_id" property="customerId"/>
        </collection>
    </resultMap>
    <select id="queryList" resultMap="customerMap">
        SELECT * FROM t_order tor JOIN t_customer tur ON tor.customer_id = tur.customer_id;
    </select>
</mapper>
```

1. `<resultMap>` 是映射的顶层容器，用于定义从 ResultSet 到 Java 对象的映射规则：  

```vtable
{"rows":[[{"t":"属性","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1}],[{"t":"id","rs":1,"cs":1},{"t":"resultMap的唯一标识","rs":1,"cs":1}],[{"t":"type","rs":1,"cs":1},{"t":"映射的目标Java类型（全限定类名或别名）","rs":1,"cs":1}],[{"t":"property","rs":1,"cs":1},{"t":"Java对象的属性名","rs":1,"cs":1}],[{"t":"column","rs":1,"cs":1},{"t":"数据库列名（或别名）","rs":1,"cs":1}]]}
```

2. `<association>` 用于映射单个关联对象：  

```vtable
{"rows":[[{"t":"属性","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1}],[{"t":"property","rs":1,"cs":1},{"t":"Java对象中关联属性的名称","rs":1,"cs":1}],[{"t":"javaType","rs":1,"cs":1},{"t":"关联对象的Java类型","rs":1,"cs":1}],[{"t":"column","rs":1,"cs":1},{"t":"传递给子查询的列名","rs":1,"cs":1}]]}
```

3. `<collection>` 用于映射集合属性：  

```vtable
{"rows":[[{"t":"属性","rs":1,"cs":1},{"t":"含义","rs":1,"cs":1}],[{"t":"property","rs":1,"cs":1},{"t":"Java对象中集合属性的名称","rs":1,"cs":1}],[{"t":"ofType","rs":1,"cs":1},{"t":"集合中元素的类型（即泛型类型）","rs":1,"cs":1}],[{"t":"column","rs":1,"cs":1},{"t":"传递给子查询的列","rs":1,"cs":1}]]}
```

### 3-3-4 多表映射总结

```vtable
{"rows":[[{"t":"关联关系","rs":1,"cs":1},{"t":"配置项关键词","rs":1,"cs":1},{"t":"所在配置文件和具体位置","rs":1,"cs":1}],[{"t":"对一","rs":1,"cs":1},{"t":"association标签/javaType属性/property属性","rs":1,"cs":1},{"t":"Mapper配置文件中的resultMap标签内","rs":1,"cs":1}],[{"t":"对多","rs":1,"cs":1},{"t":"collection标签/ofType属性/property属性","rs":1,"cs":1},{"t":"Mapper配置文件中的resultMap标签内","rs":1,"cs":1}]]}
```

## 3-4 MyBatis 动态语句
### 3-4-1 if 和 where 标签

```xml
<mapper namespace="com.prokyhoof.mapper.EmployeeMapper">
    <!-- where标签的作用有两个:
         1 自动添加where关键字,where内部有任何一个if满足,自动添加where关键字,不满足去掉where
         2 自动去掉多余的and 和 or 关键字 -->
    <select id="query" resultType="employee">
        SELECT * FROM t_emp
        <where>
            <if test="name != null">
                emp_name = #{name}
            </if>
            <if test="salary != null and salary &gt; 100">
                and emp_salary = #{salary};
            </if>
        </where>
    </select>
</mapper>
```

### 3-4-2 set 标签

```xml
<update id="updateEmployeeDynamic">
    UPDATE t_emp
    <!-- set emp_name = #{empName}, emp_salary = #{empSalary}
         使用set标签动态管理set子句,并且动态去掉两端多余的逗号 -->
    <set>
        <if test="empName != null">
            emp_name = #{empName},
        </if>
        <if test="empSalary != null">
            emp_salary = #{empSalary},
        </if>
    </set>
    WHERE emp_id = #{empId}
    <!-- 第一种情况:所有条件都满足 SET emp_name = ?, emp_salary = ?
         第二种情况:部分条件满足 SET emp_salary = ?
         第三种情况:所有条件都不满足 UPDATE t_emp WHERE emp_id = ?
         没有set子句的update语句会导致SQL语法错误 -->
</update>
```

### 3-4-3 trim 标签
使用 trim 标签控制条件部分两端是否包含某些字符。  
1. prefix 属性：指定要动态添加的前缀。  
2. suffix 属性：指定要动态添加的后缀。  
3. prefixOverrides 属性：指定要动态去掉的前缀，使用"|"分隔有可能的多个值。  
4. suffixOverrides 属性：指定要动态去掉的后缀，使用"|"分隔有可能的多个值。  

```xml
<select id="selectEmployeeByConditionByTrim" resultType="com.prokyhoof.mybatis.entity">
    SELECT emp_id, emp_name, emp_age, emp_salary, emp_gender FROM t_emp;
    <trim prefix="where" suffixOverrides="and|or">
        <if test="empName != null">
            emp_name = #{name} and
        </if>
        <if test="empSalary &gt; 3000">
            emp_salary > #{empSalary} and
        </if>
        <if test="empAge &lt;= 20">
            emp_age = #{empAge} or
        </if>
        <if test="empGender == 'male'">
            emp_gender = #{empGender}
        </if>
    </trim>
</select>
```

### 3-4-4 choose/when/otherwise 标签
在多个分支条件中，仅执行一个。  
1. 从上到下依次执行条件判断。  
2. 遇到的第一个满足条件的分支会被采纳。  
3. 被采纳分支后面的分支都将不被考虑。  
4. 如果所有的 when 分支都不满足，那么就执行 otherwise 分支。  

```xml
<select id="selectEmployeeByConditionByChoose" resultType="com.prokyhoof.mybatis.entity">
    SELECT emp_id, emp_name, emp_salary FROM t_emp WHERE
    <choose>
        <when test="empName != null">
            emp_name = #{empName}
        </when>
        <when test="empSalary &lt; 3000">
            emp_salary &lt; 3000
        </when>
        <otherwise>
            1 = 1
        </otherwise>
    </choose>
</select>
```

### 3-4-5 foreach 标签
collection 属性：要遍历的集合对象。MyBatis 会根据传入参数类型自动识别。  
1. 如果是 List，默认用"list"。  
2. 如果是 Array，默认用"array"。  
3. 如果是 Map，可用 key 名。  
4. 如果是自定义参数（@Param），用 @Param("xxx") 指定的名称。  

item 属性：集合中每个元素的别名，在循环体内部通过 #{item} 引用。  
open 属性：循环开始前拼接的字符串。  
close 属性：循环结束后拼接的字符串。  
separator 属性：每次迭代之间的分隔符。  
关于 foreach 标签的 collection 属性：  
如果没有给接口中 List 类型的参数使用 @Param 注解指定一个具体的名字，那么在 collection 属性中默认可以使用 collection 或 list 来引用这个 list 集合，这一点可以通过异常信息看出来。  
在实际开发中，为了避免隐晦的表达造成一定的误会，建议使用 @Param 注解明确声明变量的名称，然后在 foreach 标签的 collection 属性中按照 @Param 注解指定的名称来引用传入的参数。  

```xml
<delete id="deleteBatch">
    DELETE FROM t_emp WHERE id IN
    <foreach collection="ids" open="(" separator="," close=")" item="id">
        #{id}
    </foreach>
</delete>
```

```xml
<insert id="insertBatch">
    INSERT INTO t_emp (emp_name, emp_salary) VALUES
    <foreach collection="list" separator="," item="employee">
        (#{employee.empName}, #{employee.empSalary})
    </foreach>
</insert>
```

### 3-4-6 sql 片段
抽取重复的 SQL 片段：  

```xml
<!-- 使用sql标签抽取重复出现的SQL片段 -->
<sql id="mySelectSql">
    SELECT emp_id, emp_name, emp_age, emp_salary, emp_gender FROM t_emp
</sql>
```

引用已抽取的 SQL 片段：  

```xml
<!-- 使用include标签引用声明的SQL片段 -->
<include refid="mySelectSql"/>
```

## 3-5 MyBatis 高级扩展
### 3-5-1 Mapper 批量映射优化
当 Mapper 接口和 Mapper.xml 文件比较多时，可以在 mybatis-config.xml 中通过 package 标签批量注册 Mapper 映射文件，无需逐个配置。  

```xml
<mappers>
    <package name="com.prokyhoof.mapper"/>
</mappers>
```

批量注册后，要求 Mapper 接口和 Mapper.xml 文件同名且在同一个包（或类路径下的同路径）下。  
### 3-5-2 插件和分页插件 PageHelper
#### 3-5-2-1 插件机制和 PageHelper 插件介绍
MyBatis 的插件机制包括以下三种组件：  
1. Interceptor（拦截器）：定义一个拦截方法 intercept，该方法在执行 SQL 语句、执行查询、查询结果的映射时会被调用。  
2. Invocation（调用）：实际上是对拦截的方法的封装，封装了 Object target、Method method 和 Object[] args 这三个字段。  
3. InterceptorChain（拦截器链）：对所有的拦截器进行管理，包含将所有的 Interceptor 链接成一个链，并在执行 SQL 语句时按顺序调用。  

插件的开发非常简单，只需要实现 Interceptor 接口，并使用注解 @Intercepts 来标注需要拦截的对象和方法，然后在 MyBatis 的配置文件中添加插件即可。  
PageHelper 是 MyBatis 中的分页插件，它提供了多种分页方式（例如 MySQL 和 Oracle 分页方式），支持多种数据库。  
#### 3-5-2-2 PageHelper 插件使用
1. pom.xml 引入依赖：  

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.1.11</version>
</dependency>
```

2. mybatis-config.xml 配置分页插件：  

在 MyBatis 的配置文件中添加 PageHelper 的插件。  

```xml
<plugins>
    <plugin interceptor="com.github.pagehelper.PageInterceptor">
        <property name="helperDialect" value="mysql"/>
    </plugin>
</plugins>
```

其中，com.github.pagehelper.PageInterceptor 是 PageHelper 插件的类名，helperDialect 属性用于指定数据库类型（支持多种数据库）。  
3. 分页插件使用：  

在查询方法中使用分页。  

```java
@Test
public void testTeacherRelationshipToMulti() {
    TeacherMapper teacherMapper = session.getMapper(TeacherMapper.class);
    // 在查询之前调用PageHelper.startPage(页码, 每页条数)
    PageHelper.startPage(1, 2);
    // 查询Customer对象同时将关联的Order集合查询出来
    List<Teacher> allTeachers = teacherMapper.findAllTeachers();
    PageInfo<Teacher> pageInfo = new PageInfo<>(allTeachers);
    System.out.println("pageInfo = " + pageInfo);
    long total = pageInfo.getTotal(); // 获取总记录数
    System.out.println("total = " + total);
    int pages = pageInfo.getPages(); // 获取总页数
    System.out.println("pages = " + pages);
    int pageNum = pageInfo.getPageNum(); // 获取当前页码
    System.out.println("pageNum = " + pageNum);
    int pageSize = pageInfo.getPageSize(); // 获取每页显示记录数
    System.out.println("pageSize = " + pageSize);
    List<Teacher> teachers = pageInfo.getList(); // 获取查询页的数据集合
    System.out.println("teachers = " + teachers);
    teachers.forEach(System.out::println);
}
```

### 3-5-3 逆向工程和 MyBatis 插件
#### 3-5-3-1 ORM 思维介绍
ORM（Object-Relational Mapping，对象-关系映射）是一种将数据库和面向对象编程语言中的对象之间进行转换的技术，它将对象和关系数据库的概念进行映射。使用面向对象思维进行数据库操作。  
ORM 框架通常有半自动和全自动两种方式：  
1. 半自动 ORM 通常需要程序员手动编写 SQL 语句或者配置文件，将实体类和数据表进行映射，还需要手动将查询的结果集转换成实体对象。  
2. 全自动 ORM 则是将实体类和数据表进行自动映射，使用 API 进行数据库操作时，ORM 框架会自动执行 SQL 语句并将查询结果转换成实体对象，程序员无需再手动编写 SQL 语句和转换代码。  

常见的半自动 ORM 框架包括 MyBatis 等；常见的全自动 ORM 框架包含 Hibernate、Spring Data JPA、MyBatis-Plus 等。  
#### 3-5-3-2 逆向工程
MyBatis 的逆向工程是一种自动化生成持久层代码和映射文件的工具，它可以根据数据表结构和设置的参数生成对应的实体类、Mapper.xml 文件、Mapper 接口等代码文件，简化了开发者手动生成的过程。逆向工程使开发者可以快速地构建起 DAO 层，并快速上手进行业务开发。  
MyBatis 的逆向工程有两种方式：  
1. 通过 MyBatis Generator 插件实现。  
2. 通过 Maven 插件实现。  

逆向工程一般需要指定一些配置参数，例如数据库连接 URL、用户名、密码、要生成的表名、生成的文件路径等等。  

> 注意：逆向工程只能生成单表 CRUD 的操作，多表查询依然需要我们自己编写。  

#### 3-5-3-3 逆向工程插件 MyBatisX 使用
MyBatisX 是一个 MyBatis 的代码生成插件，可以通过简单的配置和操作快速生成 MyBatis Mapper、pojo 类和 Mapper.xml 文件。  
在 IDEA 中安装 MyBatisX 插件后，在 Mapper 接口的方法上可以直接跳转到对应的 Mapper.xml 中的 SQL 语句，也可以在数据库表上右键选择 Generate MyBatis 快速生成实体类、Mapper 接口和 Mapper.xml。

# 4 SpringMVC
## 4-1 SpringMVC 简介
### 4-1-1 介绍
Spring Web MVC 是基于 Servlet API 构建的原始 Web 框架，从一开始就包含在 Spring Framework 中。正式名称"Spring Web MVC"来自其源模块的名称（spring-webmvc），但它通常被称为"Spring MVC"。  
### 4-1-2 主要作用
SSM 框架构建起单体项目的技术栈需求！其中的 SpringMVC 负责表述层（控制层）实现简化。  
1. 简化前端参数接收（形参列表）。  
2. 简化后端数据响应（返回值）。  

### 4-1-3 核心组件和调用流程理解

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringMVC%20image%20061ff8cd304a77a6.png)  

SpringMVC 涉及组件理解：  
1. DispatcherServlet：SpringMVC 提供，我们需要使用 web.xml 配置使其生效，它是整个流程处理的核心，所有请求都经过它的处理和分发【CEO】。  
2. HandlerMapping：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效，它内部缓存 handler（controller 方法）和 handler 访问路径数据，被 DispatcherServlet 调用，用于查找路径对应的 handler【秘书】。  
3. HandlerAdapter：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效，它可以处理请求参数和处理响应数据，每次 DispatcherServlet 都是通过 handlerAdapter 间接调用 handler，它是 handler 和 DispatcherServlet 之间的适配器【经理】。  
4. Handler：handler 又称处理器，它是 Controller 内部的方法简称，是由我们自己定义用来接收参数，向后调用业务，最终返回响应结果【打工人】。  
5. ViewResolver：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效。视图解析器主要简化模板视图页面查找的，但是需要注意，前后端分离项目，后端只返回 JSON 数据，不返回页面，那就不需要视图解析器。所以，视图解析器，相对其他的组件不是必须的【财务】。  

## 4-2 SpringMVC 接收数据
### 4-2-1 访问路径设置
@RequestMapping 注解的作用就是将请求的 URL 地址和处理请求的方式（handler 方法）关联起来、建立映射关系。  
SpringMVC 接收到指定的请求，就会来找到映射关系中对应的方法来处理这个请求。  
1. 精准路径匹配：  

在 @RequestMapping 注解指定 URL 地址时，不使用任何通配符，按照请求地址进行精确匹配。  

```java
@Controller
@RequestMapping(value = {"/user"})
public class UserController {

    // 精准设置访问地址 /user/login
    @RequestMapping(value = {"/login"})
    @ResponseBody
    @GetMapping
    public String login() {
        System.out.println("UserController.login");
        return "login success";
    }

    // 精准设置访问地址 /user/register
    @RequestMapping(value = {"/register"}, method = RequestMethod.POST)
    @ResponseBody
    public String register() {
        System.out.println("UserController.register");
        return "register success";
    }
}
```

### 4-2-2 接收参数
#### 4-2-2-1 param 和 json 参数比较
1. 参数编码：param 类型的参数会被编码为 ASCII 码。JSON 类型的参数会被编码为 UTF-8。  
2. 参数顺序：param 类型的参数没有顺序限制。JSON 类型的参数是有序的，JSON 采用键值对的形式进行传递，其中键值对是有序排列的。  
3. 嵌套性：param 类型的参数不支持嵌套。JSON 类型的参数支持嵌套，可以传递更为复杂的数据结构。  
4. 数据类型：param 类型的参数仅支持字符串类型、数据类型和布尔类型等简单数据类型。而 JSON 类型的参数则支持更复杂的数据类型，如数组、对象等。  
5. 可读性：param 类型的参数格式比 JSON 类型的参数更加简单、易读。JSON 格式在传递嵌套数据结构时更加清晰易懂。  

#### 4-2-2-2 param 参数接收
1. 直接接值：  

```java
@Controller
@RequestMapping("/param")
public class ParamController {

    @GetMapping(value = "/value")
    @ResponseBody
    public String setupForm(String name, int age) {
        System.out.println("name = " + name + ", age = " + age);
        return name + age;
    }
}
```

2. @RequestParam 注解：  

可以使用 @RequestParam 注解将 Servlet 请求参数（即查询参数或表单数据）绑定到控制器中的方法参数。  

```java
@GetMapping(value = "/data")
@ResponseBody
public Object paramForm(@RequestParam("name") String name, @RequestParam("stuAge") int age) {
    System.out.println("name = " + name + ", age = " + age);
    return name + age;
}
```

#### 4-2-2-3 路径参数接收
路径传递参数是一种在 URL 路径中传递参数的方式。Spring MVC 框架提供了 @PathVariable 注解来处理路径传递参数。  
@PathVariable 注解允许将 URL 中的占位符映射到控制器方法中的参数。  

```java
@GetMapping("/user/{id}/{name}")
@ResponseBody
public String getUser(@PathVariable Long id, @PathVariable String uname) {
    System.out.println("id = " + id + ", uname = " + uname);
    return "user_detail";
}
```

#### 4-2-2-4 JSON 参数接收
Spring MVC 框架使用 @RequestBody 注解来将 JSON 数据转化为 Java 对象。@RequestBody 注解表示当前方法参数的值应该从请求体中获取。  

```java
@Controller
@EnableWebMvc
public class PersonController {

    @PostMapping("/person")
    @ResponseBody
    public String addPerson(@RequestBody Person person) {
        return "success";
    }
}
```

@EnableWebMvc 注解效果等同于在 XML 配置中，可以使用 `<mvc:annotation-driven>` 元素。  
### 4-2-3 接收 Cookie 数据
可以使用 @CookieValue 注解将 HTTP Cookie 的值绑定到控制器中的方法参数。  

```java
@Controller
@RequestMapping("/cookie")
public class CookieController {

    @RequestMapping("data")
    @ResponseBody
    public String data(@CookieValue(value = "cookieName") String value) {
        System.out.println("value = " + value);
        return value;
    }

    @RequestMapping("save")
    @ResponseBody
    public String save(HttpServletResponse response) {
        Cookie cookie = new Cookie("cookieName", "root");
        response.addCookie(cookie);
        return "ok";
    }
}
```

## 4-3 SpringMVC 响应数据
### 4-3-1 handler 方法分析

```java
// 一个controller的方法是控制层的一个处理器,我们称为handler
// handler需要使用RequestMapping/@GetMapping系列,声明路径,在HandlerMapping中注册
// handler的作用总结
// 1 接收请求参数(param,json,pathVariable,共享域等)
// 2 调用业务逻辑
// 3 响应前端数据(页面(不讲解模板页面跳转),json,转发和重定向等)
// handler如何处理
// 1 接收参数:handler(形参列表:主要的作用就是用来接收参数)
// 2 调用业务:方法体 可以向后调用业务方法 service.xx()
// 3 响应数据:return 返回结果,可以快速响应前端数据
@GetMapping("/xxx")
public Object handler(简化请求参数接收) {
    调用业务方法
    返回的结果
    return 简化响应前端数据;
}
```

总结：请求数据接收，我们都是通过 handler 的形参列表。  
前端数据响应，我们都是通过 handler 的 return 关键字快速处理。  
SpringMVC 简化了参数接收和响应。  
### 4-3-2 页面跳转控制
#### 4-3-2-1 快速返回模板视图
1. 开发模式回顾：  
   1. 前后端分离模式。  
   2. 混合开发模式。  
2. JSP 技术：  

JSP（JavaServer Pages）是一种动态网页开发技术，它是由 Sun 公司提出的一种基于 Java 技术的 Web 页面制作技术，可以在 HTML 文件中嵌入 Java 代码，使得生成动态内容的编写更加简单。  

```xml
<!-- JSP需要依赖jstl -->
<dependency>
    <groupId>jakarta.servlet.jsp.jstl</groupId>
    <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
    <version>3.0.0</version>
</dependency>
```

建议位置：/WEB-INF/ 下。避免外部直接访问。  
位置：/WEB-INF/views/home.jsp。  

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <!-- 可以获取共享域的数据,动态展示。JSP==后台vue -->
    ${msg}
</body>
</html>
```

#### 4-3-2-2 转发和重定向

```java
@GetMapping("forward")
public String forward() {
    System.out.println("JspController.forward");
    return "forward:/jsp/index";
}

@GetMapping("redirect")
public String redirect() {
    System.out.println("JspController.redirect");
    return "redirect:/jsp/index";
}
```

### 4-3-3 返回 JSON 数据
#### 4-3-3-1 前置准备
1. 导入 jackson 依赖：  

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.0</version>
</dependency>
```

2. 添加 JSON 数据转化器 @EnableWebMvc：  

```java
// SpringMVC对应组件的配置类【声明SpringMVC需要的组件信息】
// 导入handlerMapping和HandlerAdapter的三种方式
// 1 自动导入handlerMapping和handlerAdapter
// 2 可以不添加,SpringMVC会检查是否配置handlerMapping和handlerAdapter,没有配置默认加载
// 3 使用@Bean方式配置handlerMapping和handlerAdapter
@EnableWebMvc
@Configuration
@ComponentScan(basePackages = "com.prokyhoof.controller")
// WebMvcConfigurer SpringMVC进行组件配置的规范,配置组件,提供各种方法!前期可以实现
public class SpringMvcConfig implements WebMvcConfigurer {
}
```

#### 4-3-3-2 @ResponseBody
可以在方法上使用 @ResponseBody 注解，用于将方法返回的对象序列化为 JSON 或 XML 格式的数据，并发送给客户端。在前后端分离的项目中使用。  
具体来说，@ResponseBody 注解可以用来表示方法或者方法返回值，表示方法的返回值是要直接返回给客户端的数据，而不是由视图解析器来解析并渲染生成响应体（ViewResolver 没用）。  
#### 4-3-3-3 @RestController
@RestController = @Controller + @ResponseBody。  
### 4-3-4 返回静态资源处理

```java
// 开启静态资源查找
// dispatcherServlet寻找handlerMapping找有没有对应的handler,如果没有,则找有没有静态资源
@Override
public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
    configurer.enable();
}
```

## 4-4 RESTFul 风格设计和实战
### 4-4-1 RESTFul 风格概述
#### 4-4-1-1 RESTFul 风格简介
RESTFul（Representational State Transfer）是一种软件架构风格，用于设计网络应用程序和服务之间的通信。它是一种基于标准 HTTP 方法的简单和轻量级的通信协议，广泛应用于现代的 Web 服务开发。  
RESTFul 是一种基于 HTTP 和标准化的设计原则的软件架构风格，用于设计和实现可靠、可扩展和易于集成的 Web 服务和应用程序。  
#### 4-4-1-2 RESTFul 风格特点
1. 每一个 URI 代表 1 种资源（URI 是名词）。  
2. 客户端使用 GET、POST、PUT、DELETE 4 个表示操作方式的动词对服务端资源进行操作：GET 用来获取资源，POST 用来新建资源（也可以用于更新资源），PUT 用来更新资源、DELETE 用来删除资源。  
3. 资源的表现形式是 XML 或者 JSON。  
4. 客户端与服务器之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必需的信息。  

#### 4-4-1-3 RESTFul 风格设计规范
1. HTTP 协议请求方式要求：  

REST 风格主张在项目设计、开发过程中，具体的操作符合 HTTP 协议定义的请求方式的语义。  

```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"请求方式","rs":1,"cs":1}],[{"t":"查询操作","rs":1,"cs":1},{"t":"GET","rs":1,"cs":1}],[{"t":"保存操作","rs":1,"cs":1},{"t":"POST","rs":1,"cs":1}],[{"t":"删除操作","rs":1,"cs":1},{"t":"DELETE","rs":1,"cs":1}],[{"t":"更新操作","rs":1,"cs":1},{"t":"PUT","rs":1,"cs":1}]]}
```

2. URL 路径风格要求：  

REST 风格下每个资源都应该有一个唯一的标识符，例如一个 URI（统一资源标识符）或者一个 URL（统一资源定位符）。资源的标识符应该能明确地说明该资源的信息，同时也应该是可被理解和解释的。  
使用 URL + 请求方式确定具体的动作，也是一种标准的 HTTP 协议请求。  

```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"传统风格","rs":1,"cs":1},{"t":"REST风格","rs":1,"cs":1}],[{"t":"保存","rs":1,"cs":1},{"t":"/CURD/saveEmp","rs":1,"cs":1},{"t":"URL地址：/CRUD/emp  请求方式：POST","rs":1,"cs":1}],[{"t":"删除","rs":1,"cs":1},{"t":"/CURD/deleteEmp?empId=2","rs":1,"cs":1},{"t":"URL地址：/CRUD/emp/2  请求方式：DELETE","rs":1,"cs":1}],[{"t":"更新","rs":1,"cs":1},{"t":"/CURD/updateEmp","rs":1,"cs":1},{"t":"URL地址：/CURD/emp  请求方式：PUT","rs":1,"cs":1}],[{"t":"查询","rs":1,"cs":1},{"t":"/CURD/editEmp?empId=2","rs":1,"cs":1},{"t":"URL地址：/CURD/emp/2  请求方式：GET","rs":1,"cs":1}]]}
```

总结：  
根据接口的具体动作，选择具体的 HTTP 协议请求方式。  
路径设计从原来携带动标识，改成名词，对应资源的唯一标识即可。  
#### 4-4-1-4 RESTFul 风格好处
1. 含蓄，安全。  
2. 风格统一。  
3. 无状态。  
4. 严谨，规范。  
5. 简洁、优雅。  
6. 丰富的语义。  

## 4-5 SpringMVC 其他扩展
### 4-5-1 全局异常处理机制
#### 4-5-1-1 异常处理两种方式
1. 编程式异常处理。  
2. 声明式异常处理。  

声明式异常处理使用 @RestControllerAdvice（或 @ControllerAdvice）和 @ExceptionHandler：  
1. 声明异常处理控制器类 @RestControllerAdvice。  
2. 创建 Handler @ExceptionHandler。  

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public Result handlerException(Exception e) {
        // 记录日志,统一返回失败结果
        return Result.error(e.getMessage());
    }
}
```

### 4-5-2 拦截器使用
#### 4-5-2-1 拦截器 HandlerInterceptor
1. 重写方法 preHandle：  

执行 handler 之前，调用的拦截方法。  
编码格式设置，登录保护，权限处理。  
参数：request 请求对象、response 响应对象、handler 调用的 handler 方法对象。  
2. 重写方法 postHandle：  

当 Handler 执行完毕后，触发的方法，没有拦截机制。  
参数：request 请求对象、response 响应对象、handler 调用的 handler 方法对象、modelAndView 返回的视图和共享域数据对象。  
3. 重写方法 afterCompletion：  

整体处理完毕，就会调用此方法。  
参数：request 请求对象、response 响应对象、handler 调用的 handler 方法对象、ex handler 报错的异常对象。  
4. 多个拦截器执行顺序：  
   1. preHandle() 方法：SpringMVC 会把所有拦截器收集到一起，然后按照配置顺序调用各个 preHandle() 方法。  
   2. postHandle() 方法：SpringMVC 会把所有拦截器收集到一起，然后按照配置相反的顺序调用各个 postHandle() 方法。  
   3. afterCompletion() 方法：SpringMVC 会把所有拦截器收集到一起，然后按照配置相反的顺序调用各个 afterCompletion() 方法。  

拦截器的注册需要在配置类中实现 WebMvcConfigurer 的 addInterceptors 方法完成。  

```java
@Override
public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(new MyInterceptor())
            .addPathPatterns("/**")
            .excludePathPatterns("/login", "/css/**", "/js/**");
}
```

### 4-5-3 校验参数
1. 校验概述：  

JSR 303 是 Java 为 Bean 数据合法性校验提供的标准框架，它已经包含在 JavaEE 6.0 标准中。  

```vtable
{"rows":[[{"t":"注解","rs":1,"cs":1},{"t":"规则","rs":1,"cs":1}],[{"t":"@Null","rs":1,"cs":1},{"t":"标注值必须为null","rs":1,"cs":1}],[{"t":"@NotNull","rs":1,"cs":1},{"t":"标注值不可为null","rs":1,"cs":1}],[{"t":"@AssertTrue","rs":1,"cs":1},{"t":"标注值必须为true","rs":1,"cs":1}],[{"t":"@AssertFalse","rs":1,"cs":1},{"t":"标注值必须为false","rs":1,"cs":1}],[{"t":"@Min(value)","rs":1,"cs":1},{"t":"标注值必须大于或等于value","rs":1,"cs":1}],[{"t":"@Max(value)","rs":1,"cs":1},{"t":"标注值必须小于或等于value","rs":1,"cs":1}],[{"t":"@DecimalMin(value)","rs":1,"cs":1},{"t":"标注值必须大于或等于value","rs":1,"cs":1}],[{"t":"@DecimalMax(value)","rs":1,"cs":1},{"t":"标注值必须小于或等于value","rs":1,"cs":1}],[{"t":"@Size(max,min)","rs":1,"cs":1},{"t":"标注值大小必须在max和min限定的范围内","rs":1,"cs":1}],[{"t":"@Digits(integer,fraction)","rs":1,"cs":1},{"t":"标注值必须是一个数字，且必须在可接受的范围内","rs":1,"cs":1}],[{"t":"@Past","rs":1,"cs":1},{"t":"标注值只能用于日期型，且必须是过去的日期","rs":1,"cs":1}],[{"t":"@Future","rs":1,"cs":1},{"t":"标注值只能用于日期型，且必须是将来的日期","rs":1,"cs":1}],[{"t":"@Pattern(value)","rs":1,"cs":1},{"t":"标注值必须符合指定的正则表达式","rs":1,"cs":1}]]}
```

2. 易混总结：  
   1. @NotNull（包装类型不为 null）。  
   2. @NotEmpty（集合类型长度大于 0）。  
   3. @NotBlank（字符串，不为 null，且不为""字符串）。  
3. 注意：  

handler 中需要校验的参数都需前置加上 @Validated。  
如果是 JSON 参数，那么还需要加上 @RequestBody。  
捕捉错误绑定信息：  
1. Handler（校验对象，BindingResult result）。  
2. BindingResult 获取绑定错误。  

```java
@PostMapping("/save")
public Result save(@Validated @RequestBody Employee employee, BindingResult result) {
    if (result.hasErrors()) {
        // 处理校验错误
        return Result.error("参数校验失败");
    }
    return Result.success();
}
```

# 5 SpringBoot3
## 5-1 SpringBoot 介绍
SpringBoot 帮我们简单、快速地创建一个独立的、生产级别的 Spring 应用（说明：SpringBoot 底层是 Spring），大多数 SpringBoot 应用只需要编写少量配置即可快速整合 Spring 平台及第三方技术。  
SpringBoot 的核心优势：  
1. 自动配置：根据依赖自动完成大量默认配置，减少繁琐的 XML 配置。  
2. 起步依赖：通过 starter 依赖一键引入相关功能模块及其依赖版本。  
3. 内嵌容器：内嵌 Tomcat、Jetty 等服务器，可以打成 jar 包直接运行。  
4. 生产就绪：提供健康检查、指标监控等生产级能力。  

## 5-2 SpringBoot3 配置文件
### 5-2-1 统一配置管理概述
配置文件应该放置在 Spring Boot 工程的 src/main/resources 目录下，这是因为 src/main/resources 目录是 Spring Boot 默认的类路径（classpath），配置文件会被自动加载并可供应用程序访问。  
SpringBoot 支持三种配置文件格式：application.properties、application.yaml、application.yml，三者配置效果一致，优先级为 application.properties > application.yml > application.yaml。  

> 注意：  
> 1. 如果设置了 spring.profiles.active，并且和 application 有重叠属性，以 active 设置优先。  
> 2. 如果设置了 spring.profiles.active，和 application 无重叠属性，application 设置依然生效。  

## 5-3 SpringBoot3 整合 SpringMVC
### 5-3-1 web 相关配置
1. server.port：指定应用程序的 HTTP 服务器端口号，默认情况下，Spring Boot 使用 8080 作为默认端口，您可以通过配置文件中设置 server.port 来更改端口号。  
2. server.servlet.context-path：设置应用程序的上下文路径。这是应用程序在 URL 中的基本路径，默认情况下，上下文路径为空。  
3. spring.mvc.view.prefix 和 spring.mvc.view.suffix：这两个属性用于配置视图解析器的前缀和后缀。视图解析器用于解析控制器返回的视图名称，并将其映射到实际的视图页面。spring.mvc.view.prefix 定义视图的前缀，spring.mvc.view.suffix 定义视图的后缀。  
4. spring.resources.static.locations：配置静态资源的位置，静态资源可以是 CSS、JavaScript、图像等。默认情况下，Spring Boot 会将静态资源放在 classpath:/static 目录下。您可以通过在配置文件中配置 spring.resources.static.locations 属性来自定义静态资源的位置。  
5. spring.http.encoding.charset 和 spring.http.encoding.enabled：这两个属性用于配置 HTTP 请求和响应的字符编码。spring.http.encoding.charset 定义字符编码的名称（例如 UTF-8），spring.http.encoding.enabled 用于启用或禁用字符编码的自动配置。  

### 5-3-2 静态资源处理
1. 默认路径：classpath:/static、classpath:/public、classpath:/resources 等。  
2. 自定义路径：  

```yaml
spring:
  web:
    resources:
      static-locations:
        - classpath: /custom-static/
        - file: /opt/uploads/
```

## 5-4 SpringBoot3 整合 Druid 数据源
Druid 是阿里开源的高性能数据库连接池，自带监控和 SQL 防注入功能。  
整合步骤：  
1. 引入依赖：druid-spring-boot-3-starter（适配 SpringBoot3）或 druid-spring-boot-starter。  
2. 配置数据源：  

```yaml
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/db?useSSL=false&serverTimezone=Asia/Shanghai
      username: root
      password: 123456
```

3. 开启监控面板：访问 /druid 可以查看 SQL 监控、连接池监控等信息。  

## 5-5 SpringBoot3 整合 MyBatis
整合步骤：  
1. 引入依赖：mybatis-spring-boot-starter（SpringBoot3 对应 mybatis-spring-boot-starter 3.x 版本）。  
2. 配置数据源与 MyBatis：  

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/db?useSSL=false&serverTimezone=Asia/Shanghai
    username: root
    password: 123456
mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.example.pojo
```

3. 在启动类或配置类上使用 @MapperScan 指定 Mapper 接口所在包，或在 Mapper 接口上加 @Mapper 注解，即可自动创建 Mapper 代理对象。

