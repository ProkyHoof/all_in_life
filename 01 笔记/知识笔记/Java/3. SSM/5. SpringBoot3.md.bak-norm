---
onenote-id: 0-7a58114f16b743558450283011bd1fbe!1-DBD29CD2C5C95FE5!s971d26051d5a448e8cec05c95f8a1cc3
---
# SpringBoot介绍

SpringBoot帮我们简单、快速地创建一个独立的、生产级别的Spring应用（说明：SpringBoot底层是Spring），大多数SpringBoot应用值需要编写少量配置即可快速整合Spring平台及第三方技术

# SpringBoot3配置文件

## 统一配置管理概述

配置文件应该放置在Spring Boot工程的src/main/resources目录下，这是因为src/main/resources目录是Spring Boot默认的类路径（classpath），配置文件会被自动加载并可供应用程序访问  
application.properties / application.yaml / application.yml  
注意：  
1 如果设置了spring.profiles.active，并且和application有重叠属性，以active设置优先  
2 如果设置了spring.profiles.active，和application无重叠属性，application设置依然生效

# SpringBoot3整合SpringMVC

## web相关配置

1 server.port：指定应用程序的HTTP服务器端口号，默认情况下，Spring Boot使用8080作为默认端口，您可以通过配置文件中设置server.port来更改端口号  
2 server,servlet.context.path：设置应用程序的上下文路径。这是应用程序在URL中的基本路径，默认情况下，上下文路径为空。您可以通过在配置文件中设置  
3 spring.mvc.view.prefix和spring.mvc.view.suffix：这两个属性用于配置视图解析器的前缀和后缀。视图解析器用于解析控制器返回的视图名称，并将其映射到实际的视图页面。spring.mvc.view.prefix定义视图的前缀，spring.mvc.view.suffix定义视图的后缀  
4 spring.resources.static.locations：配置静态资源的位置，静态资源可以是CSS、JavaScript、图像等。默认情况下，Spring Boot会将静态资源放在classpath:/static目录下。您可以通过在配置文件中配置spring.resources.static.locations属性来自定义静态资源的位置  
5 spring.http.encoding.charset和spring.http.encoding.enabled：这两个属性用于配置HTTP请求和响应的字符编码。spring.http.encoding.charset定义字符编码的名称（例如UTF-8），spring.http.encoding.enabled用于启用或禁用字符编码的自动配置

## 静态资源处理

1 默认路径

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|spring:  <br>web:  <br>resources:  <br>static-locations:  <br>- classpath: /custom-static/  <br>- file: /opt/uploads/|

# SpringBoot3整合Druid数据源

# SpringBoot3整合MyBatis