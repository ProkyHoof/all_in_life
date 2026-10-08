---
onenote-id: 0-aa987e8c2aef0ba324c4ff81d77ef844!1-DBD29CD2C5C95FE5!se4e140a7c9e643aeac1c77b25db7eb21
---
# 简介

静态资源：无需在程序运行时通过代码运行生成的资源，在程序运行之前就写好的资源。例如html，css，js，img，音频文件和视频文件。  
动态资源：需要在程序运行时通过代码运行生成的资源，在程序运行之前无法确定的数据，运行时动态生成。例如Servlet，Thymeleaf。。。。。。。动态资源指的不是视图上的动画效果或者是简单的人机交互效果。
 
不是所有的Java类都能用于处理客户端请求，能处理客户端请求并做出响应的一套技术标准就是Servlet。  
Servlet是运行在服务端的，所以Servelet必须在Web项目中开发且在Tomcat这样的服务容器中运行。
 
1 Tomcat接收到请求后，会将请求报文的信息转换一个HttpServletRequest对象，该对象中包含了请求中的所有信息（请求行，请求头，请求体）  
2 Tomcat同时创建了一个HttpServletResponse对象，该对象用于承装要响应给客户端的信息，后面，该对象会被转换成响应的报文（响应行，响应头，响应体）  
3 Tomcat根据请求中的资源路径找到对应的servlet，将servlet实例化，调用service方法，同时将HttpServletRequest和HttpServletResponse对象传入  
service方法  
1 从request对象中获取请求的所有信息（参数）  
2 根据参数生成要响应给客户端的数据  
3 将响应的数据放入response对象
 
conf/web.xml 记录了几乎所有的文件类型的对应的MIME类型
 
# Servlet生命周期

应用程序中的对象不仅在空间上有层次结构的关系，在时间上也会因为处于程序运行过程中的不同阶段而表现出不同状态和不同行为——这就是对象的生命周期。  
简单的叙述生命周期，就是对象在容器中从开始创建到销毁的过程。
 
1 实例化 构造器 servletLifeCycle 第一次请求/服务启动 1  
2 初始化 init 构造完毕 1  
3 接收请求，处理需求 服务 service 每次请求 多次  
4 销毁 destory 关闭服务 1
 
Servlet/Tomcat中是单例的  
Servlet的成员变量在多个线程之中是共享的  
不建议在servlet方法中修改成员变量 在并发请求时，会引发线程安全问题

|   |   |
|---|---|
|1|**\<load-on-startup\>****6****\</load-on-startup\>**|

默认值是-1 含义是 Tomcat启动时不会实例化servlet  
其他正整数 15 含义是Tomcat在启动时，实例化该servlet的顺序  
如果序号冲突了，Tomcat会自动协调启动顺序
   

defaultServlet响应静态资源的servlet
 
# Servlet继承结构

1 顶级的Servlet接口

|   |   |
|---|---|
|init()|初始化方法，构造完毕后，由Tomcat自动调用初始化功能的方法|
|getServletConfig()|获得ServletConfig对象的方法|
|service()|接收用户请求，向用于响应信息的方法|
|getServletInfo()|返回Servlet字符串形式描述信息的方法|
|destroy()|Servlet在回收前，由Tomcat调用的销毁方法，往往用于做资源的释放工作|
 
2 抽象的类 GenericsServlet 侧重除了service方法以外的其他方法的基础处理

|   |   |
|---|---|
|destroy()|将抽象方法，重写为普通方法，在方法内部没有任何的实现代码 --- 平庸实现|
|init(参数)|Tomcat在调用init方法时，会读取配置信息进入一个ServletConfig对象并将该对象传入init方法|
|init()|重载的初始化方法，我们重写初始化方法时对应的方法|
|getServletConfig()|返回ServletConfig的方法|
|service()|再次抽象声明service方法|
 
3 HttpServlet 抽象类 侧重service法的处理
 
4 自定义Servlet  
1 部分程序员推荐在servlet中重写do方法处理请求  
2 目前直接重写service方法也没有什么问题  
3 后续使用了SpringMVC框架后，我们无需继承HttpServlet，处理请求的方法也无需是do 或者是service  
4 如果doGet和doPost方法中，我们定义的代码都一样，可以让一个方法直接调用另一个方法  
掌握的技能  
继承HttpServlet后，要么重写service方法，要么重写doGet/doPost方法
 
# ServletConfig

注解方式

|   |
|---|
|@webServlet**{**  <br>urlPatterns **=** ""**,**  <br>initParams **= {**@webInitParam**(**name**=**""**,** value**=**""**)}**  <br>**}**|

# ServletContext

getRealPath()  
getContextPath()
 
1 域对象：一些用于存储数据和传递数据的对象，传递数据不同的范围，我们称为不同的域，不同的域对象代表不同的域，共享数据的范围不同。  
2 ServletContext代表应用，所有ServletContext域也叫作应用域，是webapp中最大的域，可以在本应用内实现数据的共享和传递。  
3 webapp中的三大域对象，分别是应用域，会话域，请求域

![](OneNote/JavaNote/web/JavaWeb/Servlet%20image%206fd3ff51cf6c40b9.png)  

# HttpServletRequest

URI 统一资源标识符 interface URI() 资源定位的要求和规范  
URL 统一资源定位符 class URL implements URI() 一个具体的资源路径
 
form 表单标签提交GET请求时，参数以键值对形式放在url后，不放在请求体里，GET方式的请求也是可以有请求体的。
   

# 请求转发和响应重定向

1 请求转发和响应重定向是web应用中间接访问项目资源的两种手段，也是Servlet控制页面跳转到两种手段。  
2 请求转发通过HttpServletRequest实现，响应重定向通过HttpServletResponse实现。

## 特性

1 请求转发时，请求和响应对象会继续传递给下一个资源  
2 请求中的参数可以继续向下传递  
3 请求转发时服务器内部的行为，客户端是不知道的  
4 客户端只产生了一次请求
 
1 请求转发是通过HttpServletRequest对象实现的。  
2 请求转发是服务器内部行为，对客户端是屏蔽的。  
3 客户端只产生了一次请求 服务器只产生了一对request和response对象。  
4 客户端的地址栏是不变的。  
5 请求的参数是可以继续传递到  
6 目标资源可以是servlet动态资源 也可以是html静态资源  
7 目标资源可以是WEB-INF下的受保护的资源，该方法也是WEB-INF下的资源的唯一访问方式  
8 目标资源不可以是外部的资源

## 响应重定向

![](OneNote/JavaNote/web/JavaWeb/Servlet%20image%20ab909d44de2e8e72.png)  

特点：￼1 重定向是通过HttpResponse对象实现的。  
2 响应重定向是在服务器提示下的，客户端行为。  
3 客户端的地址栏是变化的 客户端至少发送了两次请求 客户端产生了多次请求  
4 请求产生了多次 后端就会有多个request对象 此时请求中的参数不能继续自动传递  
5 目标资源可以是视图资源  
6 目标资源不可以是WEB-INF下的资源  
7 目标资源可以是外部资源
 
重点：同样能够实现页面跳转，优先使用响应重定向。
   

# web乱码和路径问题

## 请求乱码问题

乱码产生的根本原因：￼1 数据的编码和解码使用的不是同一个字符集  
2 使用了不支持某个语言文字的字符集
 
tomcat10 默认以UTF-8为请求体的解码字符解码  
客户端提交数据时，要是以其他字符集对请求体中的数据进行编码则会出现乱码

|   |   |
|---|---|
|1|req**.**setCharacterEncoding**(**"GBK"**);**|

GET乱码问题  
GET方式时，form表单提交的参数会放在uri后面，编码受到charset的影响  
server.xml connector URIEncoding="";  
POST乱码问题  
POST方式时，form表单提交的参数会放在请求体中，编码受到charset影响  
req.setCharacterEncoding("");

## 响应乱码问题

tomcat10中，响应体默认的编码字符集使用的是UTF-8  
解决思路：  
1 可以设置响应体的编码字符集和客户端的保持一致  
不推荐 客户端解析的字符集是无法预测的  
2 可以告诉客户端使用指定的字符集进行解码 通过设置Content-Type响应头

|   |   |
|---|---|
|1|resp**.**getContentType**(**"text/html;charset=UTF-8"**);**|

注意：明确响应体的编码，然后再设置Content-Type

## 路径问题

1 相对路径  
以当前资源的所在路径为出发点去找目标资源  
缺点：目标资源路径受到当前资源路径的影响，不同的位置，相对路径写法不同。  
2 绝对路径  
始终以固定的路径作为出发点去找目标资源 和当前资源的所在路径没有关系。  
优点：目标资源路径的写法不会受到当前资源路径的影响，不同的位置，绝对路径写法一致。  
缺点：绝对路径要补充项目的上下文 项目上下文是可以改变的  
通过head\>base\>href属性，定义相对路径公共前缀，通过公共前缀把一个相对路径转换为绝对路径

## 重定向中的路径问题

1 相对路径  
和前端的相对路劲规则一致。  
2 绝对路径  
[http://localhost:8080/](http://localhost:8080/)

## 请求转发到路径问题

1 相对路径写法一致  
2 绝对路径  
请求转发到绝对路径是不需要添加项目上下文的  
请求转发的/ 代表的路径是 [http://localhost:8080/d05/](http://localhost:8080/d05/)
 
# MVC架构模式

MVC（Model View Controller）是软件工程中的一种软件架构模式，他把软件系统分为模型、视图和控制器三个基本部分。用一种业务逻辑、数据、界面显示分离的方法阻止代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。  
1 Model模型层，具体功能如下  
存放和数据库对象的实体类以及一些用于存储非数据库表完整相关的VO对象。  
存放一些对数据进行逻辑运算操作的一些业务处理代码。  
2 View视图层，具体功能如下  
存放一些视图文件相关的代码 html css js等。  
在前后端分离的项目中，后端已经没有视图文件，该层次已经衍化成独立的前端项目。  
3 Controller控制层，具体功能如下  
接收客户端请求，获得请求数据。  
将准备好的数据响应给客户端。

![](OneNote/JavaNote/web/JavaWeb/Servlet%20image%2003a7a4f584510c19.png)