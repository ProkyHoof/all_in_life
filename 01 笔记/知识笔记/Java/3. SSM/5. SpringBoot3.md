---
tags:
  - 知识
类型: 计算机
领域: SSM
来源: "[黑马程序员Java零基础视频教程_上部(Java入门，含斯坦福大学练习题+力扣算法题和大厂java面试题）](https://www.bilibili.com/video/BV17F411T7Ao?vd_source=aae3c81bc41fca87a978ef4700fc0a91)"
日期: 2026-10-08
关联:
---
# 1 SpringBoot 介绍
SpringBoot 帮我们简单、快速地创建一个独立的、生产级别的 Spring 应用（说明：SpringBoot 底层是 Spring），大多数 SpringBoot 应用只需要编写少量配置即可快速整合 Spring 平台及第三方技术。  
SpringBoot 的核心优势：  
1. 自动配置：根据依赖自动完成大量默认配置，减少繁琐的 XML 配置。  
2. 起步依赖：通过 starter 依赖一键引入相关功能模块及其依赖版本。  
3. 内嵌容器：内嵌 Tomcat、Jetty 等服务器，可以打成 jar 包直接运行。  
4. 生产就绪：提供健康检查、指标监控等生产级能力。  

# 2 SpringBoot3 配置文件
## 2.1 统一配置管理概述
配置文件应该放置在 Spring Boot 工程的 src/main/resources 目录下，这是因为 src/main/resources 目录是 Spring Boot 默认的类路径（classpath），配置文件会被自动加载并可供应用程序访问。  
SpringBoot 支持三种配置文件格式：application.properties、application.yaml、application.yml，三者配置效果一致，优先级为 application.properties > application.yml > application.yaml。  

> 注意：  
> 1. 如果设置了 spring.profiles.active，并且和 application 有重叠属性，以 active 设置优先。  
> 2. 如果设置了 spring.profiles.active，和 application 无重叠属性，application 设置依然生效。  

# 3 SpringBoot3 整合 SpringMVC
## 3.1 web 相关配置
1. server.port：指定应用程序的 HTTP 服务器端口号，默认情况下，Spring Boot 使用 8080 作为默认端口，您可以通过配置文件中设置 server.port 来更改端口号。  
2. server.servlet.context-path：设置应用程序的上下文路径。这是应用程序在 URL 中的基本路径，默认情况下，上下文路径为空。  
3. spring.mvc.view.prefix 和 spring.mvc.view.suffix：这两个属性用于配置视图解析器的前缀和后缀。视图解析器用于解析控制器返回的视图名称，并将其映射到实际的视图页面。spring.mvc.view.prefix 定义视图的前缀，spring.mvc.view.suffix 定义视图的后缀。  
4. spring.resources.static.locations：配置静态资源的位置，静态资源可以是 CSS、JavaScript、图像等。默认情况下，Spring Boot 会将静态资源放在 classpath:/static 目录下。您可以通过在配置文件中配置 spring.resources.static.locations 属性来自定义静态资源的位置。  
5. spring.http.encoding.charset 和 spring.http.encoding.enabled：这两个属性用于配置 HTTP 请求和响应的字符编码。spring.http.encoding.charset 定义字符编码的名称（例如 UTF-8），spring.http.encoding.enabled 用于启用或禁用字符编码的自动配置。  

## 3.2 静态资源处理
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

# 4 SpringBoot3 整合 Druid 数据源
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

# 5 SpringBoot3 整合 MyBatis
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
