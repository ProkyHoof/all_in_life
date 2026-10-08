---
tags:
  - 知识
类型: 计算机
领域: SSM
来源: "[黑马程序员Java零基础视频教程_上部(Java入门，含斯坦福大学练习题+力扣算法题和大厂java面试题）](https://www.bilibili.com/video/BV17F411T7Ao?vd_source=aae3c81bc41fca87a978ef4700fc0a91)"
日期: 2026-10-08
关联:
---
# 1 简介和入门
## 1.1 Maven 介绍
Maven 就是个款为 Java 项目构建管理、依赖管理的工具（软件），使用 Maven 可以自动化构建、测试、打包和发布项目，大大提高了开发效率和质量。  
## 1.2 Maven 主要作用理解
1. 场景概念：  
   1. 将需要的依赖的信息编写到 Maven 工程的配置文件，Maven 软件就会自动下载并复制这些依赖项到项目中，也会自动下载依赖需要的依赖。确保依赖版本正确无冲突和依赖完整。  
   2. 通过个行构建命令（mvn package）快速项目构建和打包。  
2. 依赖管理：Maven 可以管理项目的依赖，包括自动下载所需依赖库、自动下载依赖需要的依赖并且保证版本没有冲突、依赖版本管理等。  
3. 构建管理：项目构建是指将源代码、配置文件、资源文件等转化为能够运行或部署的应用程序或库的过程。  

Maven 仓库分为本地仓库、中央仓库和私服（远程仓库）三类，依赖的查找顺序是：本地仓库 → 私服 → 中央仓库。  
# 2 基于 IDEA 的 Maven 工程创建
## 2.1 梳理 Maven 工程 GAVP 属性
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

## 2.2 IDEA 构建 Maven

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

# 3 Maven 核心功能依赖和构建管理
## 3.1 依赖管理和配置
通过定义 POM 文件，Maven 能够自动解析项目的依赖关系，并通过 Maven 仓库自动下载和管理依赖，从而避免了手动下载和管理依赖的繁琐工作和可能引发的版本冲突问题。  
## 3.2 依赖传递和冲突
当我们引入一个库或框架时，构建工具（Maven、Gradle）会自动解析和加载其所有的直接和间接依赖，确保这些依赖都可用。  
1. 减少重复依赖。  
2. 自动管理依赖。  
3. 确保依赖版本正确性。  

依赖传递：导入依赖，会自动导入依赖的依赖（compile 依赖），简化依赖的导入，确保依赖的根本无冲突。  
依赖冲突：发现已经存在依赖（重复依赖）会终止依赖传递！避免循环依赖和重复依赖的问题！  
依赖冲突发生场景：重复依赖！  
## 3.3 依赖导入失败场景和解决方案
问题：  
1. 下载依赖时出现网络故障或仓库服务器宕机等原因，导致无法连接至 Maven 仓库，从而无法下载依赖。  
2. 依赖项的版本号或配置文件中的版本号错误，或者依赖项没有正确定义，导致 Maven 下载的依赖项目与实际需要的不个致，从而引发错误。  
3. 本地 Maven 仓库或缓存被污染或损坏，导致 Maven 无法正确地使用现有的依赖项，并且也无法重新下载。  

解决方案：  
1. 检查网络连接和 Maven 仓库服务器状态。  
2. 确保依赖项的版本号与项目对应的版本号匹配，并检查 POM 文件中的依赖项是否正确。  
3. 清除本地 Maven 仓库缓存（lastUpdated 文件），因为只要存在 lastUpdated 缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的 gav 属性依次向下查看文件夹，最终删除内部的文件，刷新重新下载即可。  

## 3.4 扩展构建管理和插件配置
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
# 4 Maven 继承和聚合特性
## 4.1 Maven 工程继承关系
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

## 4.2 Maven 工程聚合关系
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
