---
onenote-id: 0-75c7261e5596419abdaa65760aff021f!1-DBD29CD2C5C95FE5!s971d26051d5a448e8cec05c95f8a1cc3
---
# SpringMVC简介

## 介绍

Spring Web MVC是基于Servlet API构建的原始Web框架，从一开始就包含在Spring Framework中。正式名称“Spring Web MVC”来自其源模块的名称（spring-webmvc），但它通常被称为“Spring MVC”

## 主要作用

SSM框架构建起单体项目的技术栈需求！其中的SpringMVC负责表述层（控制层）实现简化  
1 简化前端参数接收（形参列表）  
2 简化后端数据响应（返回值）

## 核心组件和调用流程理解

![](OneNote/JavaNote/%E5%90%8E%E7%AB%AF/SSM/SpringMVC%20image%20061ff8cd304a77a6.png)

SpringMVC涉及组件理解：  
1 DispatcherServlet：SpringMVC提供，我们需要使用web.xml配置使其生效，它是整个流程处理的核心，所有请求都经过他的处理和分发【CEO】  
2 HandlerMapping：SpringMVC提供，我们需要进行IoC配置使其加入IoC容器方可生效，它内部缓存handler（controller方法）和handler访问路径数据，被DispatcherServlet调用，用于查找路径对应的handler【秘书】  
3 HandlerAdapter：SpringMVC提供，我们需要进行IoC容器方可生效，它可以吹请求参数和处理响应数据，每次DispatcherServlet都是通过handlerAdapter间接调用handler，它是handler和DispatcherServlet之间的适配器【经理】  
4 Handler：handler又称处理器，它是Controller内部的方法简称，是由我们自己定义用来接收参数，向后调用业务，最终返回响应结果【打工人】  
5 ViewResovler：SpringMVC提供，我们需要进行IoC配置使其加入IoC容器方可生效。视图解析器主要简化模板视图页面查找的，但是需要注意，前后端分离项目，后端只返回JSON数据，不返回页面，那就不需要视图解析器。所以，视图解析器，相对其他的组件不是必须的【财务】
 
# SpringMVC接收数据

## 访问路径设置

@RequestMapping注解的作用就是将请求的URL地址和处理请求的方式（handler方法）关联起来、建立映射关系  
SpringMVC接收到指定的请求，就会来找到映射关系中对应的方法来处理这个请求  
1 精准路劲匹配  
在@RequestMapping注解指定URL地址时，不使用任何通配符，按照请求地址进行精确匹配

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18  <br>19|@Controller  <br>@RequestMapping**(**value**={**"/user"**})**  <br>**public class** UserController **{**  <br>        // 精准设置访问地址 /user/login  <br>        @RequestMapping**(**value**={**"/login"**})**  <br>        @ResponseBody  <br>        @GetMapping  <br>        **public** String login**() {**  <br>                System**.**out**.**println**(**"UserController.login"**);**  <br>                **return** "login success"**;**  <br>        **}**  <br>        // 精准设置访问地址 /user/register  <br>        @RequestMapping**(**value**={**"/register"**},** method**=**RequestMethod**.**POST**)**  <br>        @ResponseBody  <br>        **public** String register**() {**  <br>                System**.**out**.**println**(**"UserController.register"**);**  <br>                **return** "register success"  <br>        **}**  <br>**}**|

## 接收参数

### param和json参数比较

1 参数编码  
param类型的参数会被编码为ASCII码。JSON类型的参数会被编码为UTF-8  
2 参数顺序  
param类型的参数没有顺序限制。JSON类型的参数是有序的，JSON采用键值对的形式进行传递，其中键值对是有序排列的  
3 嵌套性  
param类型的参数不支持嵌套。JSON类型的参数支持嵌套，可以传递更为复杂的数据结构  
4 数据类型  
param类型的参数仅支持字符串类型、数据类型和布尔类型等简单数据类型。而JSON类型的参数则支持更复杂的数据类型，如数组、对象等  
5 可读性  
param类型的参数格式比JSON类型的参数更加简单、易读。JSON格式在传递嵌套数据结构时更加清晰易懂

### param参数接收

1 直接接值

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10|@Controller  <br>@RequestMapping**(**"/param"**)**  <br>**public class** ParamController **{**  <br>        @GetMapping**(**value**=**"/value"**)**  <br>        @ResponseBody  <br>        **public** String setupForm**(**String name**,** **int** age**) {**  <br>                System**.**out**.**println**(**"name = " **+** name **+** ", age = " **+** age**);**  <br>                **return** name **+** age**;**  <br>        **}**  <br>**}**|

2 @RequestParam注解  
可以使用@RequestParam注解将Servlet请求参数（即查询参数或表单数据）绑定到控制器中的方法参数

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|@GetMapping**(**value**=**"/data"**)**  <br>@ResponseBody  <br>**public** Object paramForm**(**@RequestParam**(**"name"**)** String name**,** @RequestParam**(**"stuAge"**)** **int** age**) {**  <br>        System**.**out**.**println**(**"name" **=** name **+** ", age = " **+** age**);**  <br>        **return** name **+** age**;**  <br>**}**|

### 路径参数接收

路径传递参数时一种在URL路径中传递参数的方式。Spring MVC框架提供了@PathVariable注解来处理路径传递参数  
@PathVariable注解允许将URL中的占位符映射到控制器方法中的参数

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|@GetMapping**(**"/user/{id}/{name}"**)**  <br>@ResponseBody  <br>**public** String getUser**(**@ParamVariable Long id**,** @ParamVariable String uname**) {**  <br>        System**.**out**.**println**(**"id = " **+** id **+** ", uname = " **+** uname**);**  <br>        **return** "user_detail"**;**  <br>**}**|

### JSON参数接收

Spring MVC框架使用@RequestBody注解来将JSON数据转化为Java对象。@RequestBody注解表示当前方法参数的值应该从请求体中获取，并且需要指定value属性来指定请求体应该映射到哪个参数上

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|@PostMapping**(**"/person"**)**  <br>@ResponseBody  <br>@EnableWebMvc  <br>**public** String addPerson**(**@RequestBody Person person**) {**  <br>        **return** "success"**;**  <br>**}**|

@EnableWebMvc注解效果等同于在XML配置中，可以使用\<mvc:annotation-driven\>元素

## 接收Cookie数据

可以使用@CookieValue注释将HTTP Cookie的值绑定到控制器中的方法参数

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15|@Controller  <br>@RequestMapping**(**"/cookie"**)**  <br>@ResponseBody  <br>**public class** CookieController **{**  <br>@RequestMapping**(**"data"**)**  <br>**public** String data**(**@CookieValue**(**value**=**"cookieName"**)** String value**) {**  <br>System**.**out**.**println**(**"value" **=** value**);**  <br>**}**  <br>@RequestMapping**(**"save"**)**  <br>**public** String save**(**HttpServletResponse response**) {**  <br>Cookie cookie **=** **new** Cookie**(**"cookieName"**,** "root"**);**  <br>response**.**addCookie**(**cookie**);**  <br>**return** "ok"**;**  <br>**}**  <br>**}**|

# SpringMVC响应数据

## handler方法分析

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16|// 一个controller的方法是控制层的一个处理器，我们称为handler  <br>// handler需要使用RequestMapping/@GetMapping系列，声明路径，在HandlerMapping中注册  <br>// handler的作用总结  <br>// 1 接收请求参数（param，json，pathVariable，共享域等）  <br>// 2 调用业务逻辑  <br>// 3 响应前端数据（页面（不讲解模板页面跳转），json，转发和重定向等）  <br>// handler如何处理  <br>// 1 接收参数：handler（形参列表：主要的作用就是用来接收参数）  <br>// 2 调用业务：{方法体 可以向后调用业务方法 service.xx()}  <br>// 3 响应数据：return 返回结果，可以快速响应前端数据  <br>@GetMapping  <br>**public** Objetc handler**(**简化请求参数接收**) {**  <br>调用业务方法  <br>返回的结果  <br>**return** 简化响应前端数据**;**  <br>**}**|

总结：请求数据接收，我们都是通过handler的形参列表  
前端数据响应，我们都是通过handler的return关键字快速处理  
SpringMVC简化了参数接收和响应

## 页面跳转控制

### 快速返回模板视图

1 开发模式回顾  
1 前后端分离模式  
2 混合开发模式  
2 JSP技术  
JSP（JavaServer Pages）是一种动态网页开发技术，它是由Sun公司提出的一种基于Java技术的Web页面制作技术，可以在HTML文件中嵌入了Java代码，使得生成动态内容的编写更加简单

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|// JSP需要依赖。jstl  <br>**\<dependency\>**  <br>**\<groupId\>**jakarta.servlet.jsp.jstl**\</groupId\>**  <br>**\<artifactId\>**jakarta.servlet.jsp.jstl-api**\</artifactId\>**  <br>**\<version\>****3.0.0****\</version\>**  <br>**\</dependency\>**|

建议位置：/WEB-INF/下。避免外部直接访问  
位置：/WEB-INF/views/home.jsp

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10|**\<%**@ page contentType**=**"text/html;charset=UTF-8" language**=**"java" **%\>**  <br>**\<**html**\>**  <br>**\<**head**\>**  <br>**\<**title**\>**Title**\</**title**\>**  <br>**\</**head**\>**  <br>**\<**body**\>**  <br>// 可以获取共享域的数据，动态展示。JSP==后台vue  <br>$**{**msg**}**  <br>**\</**body**\>**  <br>**\</**html**\>**|

### 转发和重定向

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11|@GetMapping**(**"forward"**)**  <br>**public** String forward**() {**  <br>System**.**out**.**println**(**"JspController.forward"**);**  <br>**return** "forward:/jsp/index"  <br>**}**<br><br>  <br><br>@GetMapping**(**"redirect"**)**  <br>**public** String redirect**() {**  <br>System**.**out**.**println**(**"JspController.redirect"**);**  <br>**return** "redirect:/jsp/index"  <br>**}**|

## 返回JSON数据

### 前置准备

1 导入jackson依赖

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|**\<dependency\>**  <br>**\<groupId\>**com.fasterxml.jackson.core**\</groupId\>**  <br>**\<artifactId\>**jackson-databind**\</artifactId\>**  <br>**\<version\>****2.15.0****\</version\>**  <br>**\</dependency\>**|

添加JSON数据转化器@EnableWebMvc

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10|// SpringMVC对应组件的配置类【声明SpringMVC需要的组件信息】  <br>// 导入handlerMapping和HandlerAdapter的三种方式  <br>// 1 自动导入handlerMapping和handlerAdapter  <br>// 2 可以不添加,SpringMVC会检查是否配置handlerMapping和handlerAdapter，没有配置默认加载  <br>// 3 使用@Bean方式配置handlerMapping和handlerAdapter  <br>@EnableWebMvc  <br>@Configuration  <br>@ComponentScan**(**basePackage**=**"com.prokyhoof.controller"**)**  <br>// WebMvcConfigurer SpringMVC进行组件配置的的规范，配置组件，提供各种方法！前期可以实现  <br>**public class** SpringMvcConfig **implements** WebMvcConfugurer **{}**|

### @ResponseBody

1 方法上使用@ResponseBody  
可以在方法上使用@ResponseBody注解，用于将方法返回的对象序列化为JSON或XML格式的数据，并发送给客户端。在前后端分离的项目中使用  
具体来说，@ResponseBody注解可以用来表示方法或者方法返回值，表示方法的返回值是要直接返回给客户端的数据，而不是由视图解析器来解析并渲染生成响应体（ViewResolver没用）

### @RestController

@RestController = @Controller + @ResponseBody

## 返回静态资源处理
 
|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|// 开启静态资源查找  <br>// dispatcherServlet寻找handlerMapping找有没有对应的handler，如果没有，则找有没有静态资源  <br>@Override  <br>**public void** configureDefaultServletHandling**(**DefaultServletHandlerConfigurer configurer**) {**  <br>configurer**.**enable**();**  <br>**}**|

# RESTFul风格设计和实战

## RESTFul风格概述

### RESTFul风格简介

RESTFul（Representational State Transfer）是一种软件架构风格，用于设计网络应用程序和服务之间的通信。它是一种基于标准HTTP方法的简单和轻量级的通信协议，广泛应用于现代的Web服务开发  
RESTFul是一种基于HTTP和标准化的设计原则的软件架构风格，用于设计和实现可靠、可扩展和易于集成的Web服务和应用程序

### RESTFul风格特点

1 每一个URI代表1种资源（URI是名词）  
2 客户端使用GET、POST、PUT、DELETE 4个表示操作方式的动词对服务端资源进行操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源、DELETE用来删除资源  
3 资源的表现形式是XML或者JSON  
4 客户端与服务器之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必需的信息

### RESTFul风格设计规范

1 HTTP协议请求方式要求  
REST风格主张在项目设计、开发过程中，具体的操作复合HTTP协议定义的请求方式的语义

|   |   |
|---|---|
|操作|请求方式|
|查询操作|GET|
|保存操作|POST|
|删除操作|DELETE|
|更新操作|PUT|

2 URL路径风格要求  
REST风格下每个资源都应该有一个唯一的标识符，例如一个URI（统一资源标识符）或者一个URL（统一资源定位符）。资源的标识符应该能明确地说明该资源的信息，同时也应该是可被理解和解释的  
使用URL + 请求方式确定具体的动作，也是一种标准的HTTP协议请求

|   |   |   |
|---|---|---|
|操作|传统风格|REST风格|
|保存|/CURD/saveEmp|URL地址：/CRUD/emp￼ 请求方式：POST|
|删除|/CURD/deleteEmp?empId=2|URL地址：/CRUD/emp/2￼ 请求方式：DELETE|
|更新|/CURD/updateEmp|URL地址：/CURD/emp￼ 请求方式：PUT|
|查询|/CURD/editEmp?empId=2|URL地址：/CURD/emp/2￼ 请求方式：GET|

总结：  
根据接口的具体动作，选择具体的HTTP协议请求方式  
路径设计从原来携带动标识，改成名词，对应资源的唯一标识即可

### RESTFul风格好处

1 含蓄，安全  
2 风格统一  
3 无状态  
4 严谨，规范  
5 简洁、优雅  
6 丰富的语义
 
# SpringMVC其他扩展

## 全局异常处理机制

### 异常处理两种方式

1 编程式异常处理  
2 声明式异常处理  
@Throws 和 @ExceptionHandler  
1 声明异常处理控制器类 @RestControllerAdvice  
2 创建Handler @ExceptionHandler

## 拦截器使用

### 拦截器HandlerInterceptor

1 重写方法preHandle  
执行handler之间，调用的拦截方法  
编码格式设置，登录保护，权限处理  
request 请求对象  
response 响应对象  
handler 调用的handler方法对象  
2 重写方法postHandle  
当Handler执行完毕后，触发的方法，没有拦截机制  
request 请求对象  
response 响应对象  
handler 调用的handler方法对象  
modeAndView 返回的视图和共享域数据对象  
3 重写方法afterCompletion  
整体处理完毕，就会调用此方法  
request 请求对象  
response 响应对象  
handler 调用的handler方法对象  
ex handler报错的异常对象  
4 多个拦截器执行顺序  
1 preHandle()方法：SpringMVC会把所有拦截器收集到一起，然后按照配置顺序调用各个preHandle()方法  
2 postHandle()方法：SpringMVC会把所有拦截器收集到一起，然后按照配置相反的顺序调用各个postHandle()方法  
3 afterCompletion()方法：SpringMVC会把所有拦截器收集到一起，然后按照配置相反的顺序调用各个afterCompletion()方法

## 校验参数

1 校验概述  
JSR 303 是Java为Bean数据合法性校验提供的标准框架，它已经包含在JavaEE 6.0标准中

|   |   |
|---|---|
|注解|规则|
|@Null|标注值必须为null|
|@NotNull|标注值不可为null|
|@AssertTrue|标注值必须为true|
|@AssertFalse|标注值必须为false|
|@Min(value)|标注值必须大于或等于value|
|@Max(value)|标注值必须小于或等于value|
|@DecimalMin(value)|标注值必须大于或等于value|
|@DecimalMax(value)|标注值必须小于或等于value|
|@Size(max,min)|标注值大小必须在max和min限定的范围内|
|@Digits(integer,fratction)|标注值必须是一个数字，且必须在可接受的范围内|
|@Past|标注值只能用于日期型，且必须是过去的日期|
|@Future|标注值只能用于日期型，且必须是将来的日期|
|@Pattern(value)|标注值必须复合指定的正则表达式|

2 易混总结  
1 @NotNull（包装类型不为null）  
2 @NotEmpty（集合类型长度大于0）  
3 @NotBlank（字符串，不为null，切不为“”字符串）  
3 注意：  
handler中需要校验的参数都需前置加上@Validated  
如果是JSON参数，那么还需要加上@RequestBody  
捕捉错误绑定信息：  
1 Handler（校验对象，BindingResult result）  
2 BindingResult获取绑定错误