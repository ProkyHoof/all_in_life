---
tags:
  - 知识
类型: 计算机
领域: SSM
来源: "[黑马程序员Java零基础视频教程_上部(Java入门，含斯坦福大学练习题+力扣算法题和大厂java面试题）](https://www.bilibili.com/video/BV17F411T7Ao?vd_source=aae3c81bc41fca87a978ef4700fc0a91)"
日期: 2026-10-08
关联:
---
# 1 SpringMVC 简介
## 1.1 介绍
Spring Web MVC 是基于 Servlet API 构建的原始 Web 框架，从一开始就包含在 Spring Framework 中。正式名称"Spring Web MVC"来自其源模块的名称（spring-webmvc），但它通常被称为"Spring MVC"。  
## 1.2 主要作用
SSM 框架构建起单体项目的技术栈需求！其中的 SpringMVC 负责表述层（控制层）实现简化。  
1. 简化前端参数接收（形参列表）。  
2. 简化后端数据响应（返回值）。  

## 1.3 核心组件和调用流程理解

![](../../../../03%20附件/attachments/知识附件/Java/3.%20SSM/SpringMVC%20image%20061ff8cd304a77a6.png)  

SpringMVC 涉及组件理解：  
1. DispatcherServlet：SpringMVC 提供，我们需要使用 web.xml 配置使其生效，它是整个流程处理的核心，所有请求都经过它的处理和分发【CEO】。  
2. HandlerMapping：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效，它内部缓存 handler（controller 方法）和 handler 访问路径数据，被 DispatcherServlet 调用，用于查找路径对应的 handler【秘书】。  
3. HandlerAdapter：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效，它可以处理请求参数和处理响应数据，每次 DispatcherServlet 都是通过 handlerAdapter 间接调用 handler，它是 handler 和 DispatcherServlet 之间的适配器【经理】。  
4. Handler：handler 又称处理器，它是 Controller 内部的方法简称，是由我们自己定义用来接收参数，向后调用业务，最终返回响应结果【打工人】。  
5. ViewResolver：SpringMVC 提供，我们需要进行 IoC 配置使其加入 IoC 容器方可生效。视图解析器主要简化模板视图页面查找的，但是需要注意，前后端分离项目，后端只返回 JSON 数据，不返回页面，那就不需要视图解析器。所以，视图解析器，相对其他的组件不是必须的【财务】。  

# 2 SpringMVC 接收数据
## 2.1 访问路径设置
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

## 2.2 接收参数
### 2.2.1 param 和 json 参数比较
1. 参数编码：param 类型的参数会被编码为 ASCII 码。JSON 类型的参数会被编码为 UTF-8。  
2. 参数顺序：param 类型的参数没有顺序限制。JSON 类型的参数是有序的，JSON 采用键值对的形式进行传递，其中键值对是有序排列的。  
3. 嵌套性：param 类型的参数不支持嵌套。JSON 类型的参数支持嵌套，可以传递更为复杂的数据结构。  
4. 数据类型：param 类型的参数仅支持字符串类型、数据类型和布尔类型等简单数据类型。而 JSON 类型的参数则支持更复杂的数据类型，如数组、对象等。  
5. 可读性：param 类型的参数格式比 JSON 类型的参数更加简单、易读。JSON 格式在传递嵌套数据结构时更加清晰易懂。  

### 2.2.2 param 参数接收
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

### 2.2.3 路径参数接收
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

### 2.2.4 JSON 参数接收
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
## 2.3 接收 Cookie 数据
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

# 3 SpringMVC 响应数据
## 3.1 handler 方法分析

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
## 3.2 页面跳转控制
### 3.2.1 快速返回模板视图
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

### 3.2.2 转发和重定向

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

## 3.3 返回 JSON 数据
### 3.3.1 前置准备
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

### 3.3.2 @ResponseBody
可以在方法上使用 @ResponseBody 注解，用于将方法返回的对象序列化为 JSON 或 XML 格式的数据，并发送给客户端。在前后端分离的项目中使用。  
具体来说，@ResponseBody 注解可以用来表示方法或者方法返回值，表示方法的返回值是要直接返回给客户端的数据，而不是由视图解析器来解析并渲染生成响应体（ViewResolver 没用）。  
### 3.3.3 @RestController
@RestController = @Controller + @ResponseBody。  
## 3.4 返回静态资源处理

```java
// 开启静态资源查找
// dispatcherServlet寻找handlerMapping找有没有对应的handler,如果没有,则找有没有静态资源
@Override
public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
    configurer.enable();
}
```

# 4 RESTFul 风格设计和实战
## 4.1 RESTFul 风格概述
### 4.1.1 RESTFul 风格简介
RESTFul（Representational State Transfer）是一种软件架构风格，用于设计网络应用程序和服务之间的通信。它是一种基于标准 HTTP 方法的简单和轻量级的通信协议，广泛应用于现代的 Web 服务开发。  
RESTFul 是一种基于 HTTP 和标准化的设计原则的软件架构风格，用于设计和实现可靠、可扩展和易于集成的 Web 服务和应用程序。  
### 4.1.2 RESTFul 风格特点
1. 每一个 URI 代表 1 种资源（URI 是名词）。  
2. 客户端使用 GET、POST、PUT、DELETE 4 个表示操作方式的动词对服务端资源进行操作：GET 用来获取资源，POST 用来新建资源（也可以用于更新资源），PUT 用来更新资源、DELETE 用来删除资源。  
3. 资源的表现形式是 XML 或者 JSON。  
4. 客户端与服务器之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必需的信息。  

### 4.1.3 RESTFul 风格设计规范
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
### 4.1.4 RESTFul 风格好处
1. 含蓄，安全。  
2. 风格统一。  
3. 无状态。  
4. 严谨，规范。  
5. 简洁、优雅。  
6. 丰富的语义。  

# 5 SpringMVC 其他扩展
## 5.1 全局异常处理机制
### 5.1.1 异常处理两种方式
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

## 5.2 拦截器使用
### 5.2.1 拦截器 HandlerInterceptor
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

## 5.3 校验参数
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
