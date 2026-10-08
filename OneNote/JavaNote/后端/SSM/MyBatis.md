---
onenote-id: 0-2f13020702ff4fdf8863710c86afe767!1-DBD29CD2C5C95FE5!s971d26051d5a448e8cec05c95f8a1cc3
---
# MyBatis简介

## 简介

MyBatis是一款优秀的持久层框架，它支持自定义SQL，存储过程以及高级映射。MyBatis免除了几乎所有的JDBC代码以及设置参数和获取结果集的工作。MyBatis可以通过简单的XML或注解来配置和映射原始类型，接口和POJO（Plain Old Java Objects，普通老式Java对象）为数据库中的记录

## 快速入门

1 依赖导入pom.xml

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15|**\<dependencies\>**  <br>        // mybatis依赖  <br>        **\<dependence\>**  <br>                **\<groupId\>**org.mybatis**\</groupId\>**  <br>                **\<artifactId\>**mybatis**\</artifactId\>**  <br>                **\<version\>****3.5.11****\</version\>**  <br>        **\</dependence\>**  <br>          <br>        // MySQL驱动 MyBatis底层依赖JDBC驱动实现，本次不需要导入连接池，MyBatis自带  <br>        **\<dependence\>**  <br>                **\<groupId\>**mysql**\</groupId\>**  <br>                **\<artifactId\>**mysql-connector-java**\</artifactId\>**  <br>                **\<version\>****8.0.25****\</version\>**  <br>        **\</dependence\>**  <br>**\</dependencies\>**|

2 实体类准备

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|**public class** Employee **{**  <br>        **private** Integer empId**;**  <br>        **private** String empName**;**  <br>        **private** Double empSalary**;**  <br>        // getter/setter  <br>**}**|

3 准备Mapper接口和Mapper.XML文件  
MyBatis框架下，SQL语句编写位置发生改变，从原来的Java类，改成XML或注解定义  
推荐在XML文件中编写SQL语句，让用户能更专注于SQL代码，不用关注其他的JDBC代码  
MyBatis中的Mapper接口相当于以前的Dao，但是区别在于，Mapper仅仅只是建接口即可，我们不需要提供实现类，具体的SQL写到对应的Mapper文件

|   |   |
|---|---|
|1  <br>2  <br>3|**public interface** EmployeeMapper **{**  <br>        Employee queryById**(**Integer id**);**  <br>**}**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|// namespace = mapper对应接口的全限定符  <br>**\<mapper** **namespace**="com.prokyhoof.mapper.EmployeeMapper"**\>**  <br>        **\<select** **id**="queryById" **resultType**="com.prokyhoof.pojo.Employee"**\>**  <br>                select emp_id empId, emp_name empName, emp_salary empSalary from t_emp where emp_id = #{id}  <br>        **\</select\>**  <br>**\</mapper\>**|

注意：  
1 方法名和SQL的id一致  
2 方法返回值和resultType一致  
3 方法的参数和SQL的参数一致  
4 接口的全类名和映射配置文件的名称空间一致  
4 准备MyBatis配置文件  
MyBatis框架配置文件：数据库连接信息，性能配置，mapper.xml配置等  
习惯上命名为mybatis-config.xml这个文件名仅仅只是建议，并非强制要求。将来整合Spring之后，这个配置文件可以省略

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18  <br>19  <br>20  <br>21  <br>22  <br>23  <br>24  <br>25|**public class** MyBatisTest **{**  <br>        @Test  <br>        **public void** testSelectEmployee**()** **throws** IOException **{**  <br>                // 1 创建SqlSessionFactory对象  <br>                // 声明NyBatis全局配置文件的路径  <br>                String mybatisConfigFilePath **=** "mybatis-config.xml"**;**  <br>                // 以输入流的形式加载MyBatis配置文件  <br>                InputStream inputStream **=** Resources**.**getResourceAsStream**(**mybatisConfigFilePath**);**  <br>                // 基于读取mybatis配置文件的输入流创建SqlSessionFactory对象  <br>                SqlSessionFactory sessionFactory **=** **new** SqlSessionFactoryBuilder**().**build**(**inputStream**);**  <br>                // 2 使用SqlSessionFactory对象开启一个会话  <br>                SqlSession session **=** sessionFactory**.**openSession**();**  <br>                // 3 根据EmployeeMapper接口的Class对象获取Mapper接口类型的对象（动态代理技术）  <br>                // jdk动态代理技术生成的mapper代理对象  <br>                EmployeeMapper employeeMapper **=** session**.**getMapper**(**EmployeeMapper**.****class****);**  <br>                // 4 调用代理类方法即可以触发对应的SQL语句  <br>                // 内部拼接接口的全限定符号.方法名，去查找SQL语句标签  <br>                // 拼接类的全限定符.方法名，整合参数去iBatis对应的方法传入参数  <br>                Employee employee **=** employeeMapper**.**selectEmployee**(****1****);**  <br>                System**.**out**.**println**(**"employee = " **+** employee**);**  <br>                // 5 关闭SqlSession  <br>                session**.**commit**();** // 提交事务，DQL不需要，其他需要  <br>                session**.**close**();** // 关闭会话  <br>        **}**  <br>**}**|

# MyBatis基本使用

## 向SQL语句传参

### MyBatis日志输出配置

[MyBatis 3 | 配置 – mybatis](https://mybatis.org/mybatis-3/zh_CN/configuration.html)

### #{}形式
 
|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7|**\<mapper** **namespace**="com.prokyhoof.mapper.EmployeeMapper"**\>**  <br>        // #{key} 占位符+赋值  <br>        // ${key} 字符串拼接  <br>        **\<select** **id**="queryById" **resultType**="com.prokyhoof.pojo.Employee"**\>**  <br>                SELECT emp_id empId, emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_id = #{id};  <br>        **\</select\>**  <br>**\</mapper\>**|

### ${}形式

## 数据输入

### MyBatis总体机制概括

![](OneNote/JavaNote/%E5%90%8E%E7%AB%AF/SSM/MyBatis%20image%204e7b1b89566d2e5b.png)

### 概念说明

这里数据输入具体是指上层方法（例如Service方法）调用Mapper接口时，数据传入的形式  
1 简单类型：只包含一个值的数据类型  
1 基本数据类型：int byte short double  
2 基本数据类型的包装类型：Integer Character Double  
3 字符串类型：String  
2 复杂类型：包含多个值的数据类型  
1 实体类类型：Employee Department  
2 集合类型：List Set Map  
3 数组类型：int[] String[]  
4 复合类型：List\<Employee\>、实体类中包含集合

### 单个简单类型参数

Mapper接口中抽象方法的声明

|   |   |
|---|---|
|1|Employee selectEmployee**(**Integer empId**);**|

SQL语句

|   |   |
|---|---|
|1  <br>2  <br>3|**\<select** **id**="selectEmployee" **resultType**="com.prokyhoof.pojo.Employee"**\>**  <br>        SELECT emp_id empId, emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_id = #{id};  <br>**\</select\>**|

单个简单类型参数，在#{}中可以随意命名，但是没有必要，通常还是使用和接口方法参数同名。

### 实体类类型参数
 
|   |   |
|---|---|
|1|**int** insertEmp**(**Employee employee**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|**\<insert** **id**="insertEmp"**\>**  <br>        insert into t_emp(emp_name, emp_salary) value (#{empName}, #{empSalary});  <br>**\</insert\>**|

### 零散的简单类型数据

|   |   |
|---|---|
|1|List**\<**Employee**\>** queryByNameAndSalary**(**@Param**(**"name"**)**String name**,** @Param**(**"salary"**)****double** salary**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|**\<select** **id**="queryByNameAndSalary" **resultType**="com.prokyhoof.pojo.Employee"**\>**  <br>        SELECT emp_id empId. emp_name empName, emp_salary empSalary FROM t_emp WHERE emp_name = #{name} AND emp_salary = #{salary};  <br>**\</select\>**|

### Map的简单类型数据

|   |   |
|---|---|
|1|**int** updateEmployeeByMap**(**Map**\<**String**,** Object**\>** paramMap**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|**\<update** **id**="updateEmployeeByMap"**\>**  <br>        UPDATE t_emp SET emp_salary = #{empSalaryKey} WHERE emp_id = #{empIdKey}  <br>**\</update\>**|

## 数据输出

### 输出概述

数据输出总体上有两种形式：  
1 增删改查操作返回的受影响行数，直接使用int或long类型接收即可  
2 查询操作的查新结果

### 单个简单类型

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|**int** deleteById**(**Integer id**);**  <br>// 指定输出类型，查询语句  <br>// 根据员工的id查询员工的姓名  <br>String queryNameById**(**Integer id**);**  <br>// 根据员工的id查询员工的工资  <br>Double querySalaryById**(**Integer id**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18|// 返回单个简单类型如何指定  <br>// **1** 类的全限定符  <br>// **2** MyBatis提供了**72**种默认的别名  <br>// Java的常用数据类型  <br>// **1** 基本数据类型：int double -**\>** _int _double  <br>// **2** 包装数据类型：Integer Double -**\>** integer double  <br>// **3** 集合容器类型：Map List HashMap -**\>** map list hashmap  <br>**\<mapper** **namespace**="com.prokyhoof.mapper.EmployeeMapper"**\>**  <br>        **\<delete** **id**="deleteById" resultType-"java.lang.Integer"**\>**  <br>                DELETE FROM t_emp WHERE emp_id = #{id};  <br>        **\</delete\>**  <br>        **\<select** **id**="queryNameById" **resultType**="com.lang.String"**\>**  <br>                SELECT emp_name empName FROM t_emp WHERE emp_id = #{id};  <br>        **\</select\>**  <br>        **\<select** **id**="querySalaryById" **resultType**="com.lang.Double"**\>**  <br>                SELECT emp_salary empSalary FROM t_emp WHERE emp_id = #{id};  <br>        **\</select\>**  <br>**\</mapper\>**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12|// 定义自己类的别名  <br>// 单独定义  <br>**\<typeAliases\>**  <br>        **\<typeAlias** **type**="com.prokyhoof.pojo.Employee" **alias**="prokyhoof"**\>**  <br>**\</typeAliases\>**  <br>// 批量定义  <br>**\<typeAliases\>**  <br>        // 批量将包下的类给予别名，别名就是类的首字母小写  <br>        **\<package** **name**="com.prokyhoof.pojo"**\>**  <br>**\</typeAliases\>**  <br>// 注释定义  <br>@Alias("prokyhoof")|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7|// 在全局范围内对MyBatis进行配置  <br>**\<settings\>**  <br>        // 具体配置  <br>        // 从org.apache.ibatis.session.Configuration类中可以查看能使用的配置项  <br>        // 将mapUnderscoreToCamelCase属性配置为true，表示开启自动映射驼峰式命名规则  <br>        **\<setting** **name**="mapUnderscoreToCamelCase" **value**="true"**\>**  <br>**\<settings\>**|

### 返回Map类型

适用于SQL查询返回的各个字段综合起来并不和任何一个现有的实体类对应，没法封装到实体类对象中。能够封装成实体类类型的，就不使用Map类型  
Mapper接口的抽象方法

|   |   |
|---|---|
|1|Map**\<**String**,** Object**\>** selectEmpNameAndMaxSalary**();**|

SQL语句

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|// Map**\<String**, Object**\>** selectEmpNameAndMaxSalary();  <br>// 返回工资最高的员工的姓名和他的工资  <br>**\<select** **id**="selectEmpNameAndMaxSalary" **resultType**="map"**\>**  <br>        SELECT emp_name empName, emp_salary empSalary, (SELECT AVG(emp_salary) FROM t_emp) avgSalary FROM t_emp WHERE emp_salary  <br>        = (SELECT MAX(emp_salary) FROM t_emp)  <br>**\</select\>**|

### 返回List类型

|   |   |
|---|---|
|1  <br>2|List**\<String\>** queryNameBySalary(Double salary);  <br>List**\<Employee\>** queryAll();|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|**\<**select id**=**"queryNameBuSalary" resultType**=**"string"**\>**  <br>        SELECT emp_name empName FROM t_emp WHERE emp_salary **\>** #**{**salary**};**  <br>**\</**select**\>**  <br>**\<**select id**=**"queryAll" resultType**=**"employee"**\>**  <br>        SELECT ***** FROM t_emp**;**  <br>**\</**select**\>**|

### 返回主键值

1 自增长类型主键

|   |   |
|---|---|
|1|**int** insertEmployee**(**Employee employee**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|// int insertEmployee(Employee employee);  <br>// useGeneratedKeys属性字面意思就是“使用生成的主键”  <br>// keyProperty属性可以指定主键在实体类对象中对应的属性名，MyBatis会将拿到的主键值存入  <br>**\<insert** **id**="insertEmployee" **useGeneratedKeys**="true" **keyProperty**="empId"**\>**  <br>        INSERT INTO t_emp (emp_name, emp_salary) VALUES (#{empName}, #{empSalary});  <br>**\</insert\>**|

注意  
MyBatis是将自增主键的值设置到条件类对戏那个中，而不是以Mapper接口方法返回值的形式返回  
2 非自增长类型主键  
而对于不支持自增型主键的数据库（例如Oracle）或者字符串类型主键，则可以使用selectKey子元素：selectKey元素将会首先运行，id会被设置，然后插入语句会被调用

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|**\<insert\>**  <br>        **\<selectKey** **keyProperty**="id" **resultType**="string" **order**="BEFORE"**\>**  <br>                SELECT UUID() AS id;  <br>        **\</selectKey\>**  <br>        INSERT INTO user (id, username, password) VALUES (#{id}, #{username}, #{password});  <br>**\</insert\>**|

在上例中，定义了一个insertUser的插入语句来将User对戏那个插入到user表中，使用selectKey来查询UUID并设置到id字段中  
通过keyProperty属性来指定查询到的UUID赋值给对象中的id属性，而resultType属性指定了UUID的类型为java.lang.String  
需要注意的是，我们将selectKey放在了插入语句的前面，这是因为MySQL在insert语句中只支持一个select字句，而selectKey中查询UUID的语句就是一个select字句，因为我们需要将其放在前面  
最后，再将User对象插入到user表中时，我们直接使用对象中的id属性来插入主键值  
使用这种方式，我们可以方便地插入UUID作为字符串类型主键。当然，还有其他插入方式可以使用，如使用Java代码生成UUID并在类中显示设置值等，需要根据具体场景和需求选择合适的插入方式

### 实体类属性和数据库字段的对应关系

1 别名对应  
将字段的别名设置成和实体类属性一致  
2 驼峰命名映射  
3 resultMap自定义映射（id，result）  
resultType按照规则自动映射，按照是否开启驼峰式映射，自己映射属性和列名，只能映射一层结构，多表查询的时候结果无法映射

## mapperXML标签总结

MyBatis的真正强大在于它的语句映射，这是它的魔力所在。由于它的异常强大，映射器的XML文件就显得相对简单。如果拿它跟具有相同功能的JDBC代码进行对比，你会立即发现省掉了将近95%的代码。MyBatis致力于减少使用成本，让用户能更专注于SQL代码  
1 insert 映射插入语句  
2 update 映射更新语句  
3 delete 映射删除语句  
4 select 映射查询语句
 
# MyBatis多表映射

## 多表映射概念

对一：属性中包含对方对象  
对多：属性包含对方对象集合  
只有真实发生多表查询时，才需要设计和修改实体类，否则不提前设计和修改实体类  
在查询映射的时候，只需要关注本次查询相关的属性

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18  <br>19  <br>20|**\<mapper** **namespace**="com.prokyhoof.pojo.OrderMapper"**\>**  <br>        // 自定义映射关系，定义嵌套对象的映射关系  <br>        **\<resultMap** **id**="orderMap" **type**="order"**\>**  <br>                // 第一层属性 order对象  <br>                // order的主键 id标签  <br>                **\<id** **column**="order_id" **property**="orderId"**\>**  <br>                **\<result** **column**="order_name" **property**="orderName"**\>**  <br>                **\<result** **column**="customer_id" **property**="customerId"**\>**  <br>                // 对象属性赋值  <br>                // property 对象属性名  <br>                // javaType 对象类型  <br>                **\<association** **property**="customer" **javaType**="customer"**\>**  <br>                        **\<id** **column**="customer_id" **property**="customerId"**\>**  <br>                        **\<result** **column**="customer_name" **property**="customerName"**\>**  <br>                **\</association\>**  <br>        **\</resultMap\>**  <br>        **\<select\>**  <br>                SLECT * FROM t_order tor JOIN t_customer tur ON tor.customer_id = tur.customer_id WHERE tor.order_id = #{id};  <br>        **\</select\>**  <br>**\</mapper\>**|

## 对多映射

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14|**\<mapper** **namespace**="com.prokyhoof.pojo.CustomerMapper"**\>**  <br>        **\<resultMap** **id**="customerMap" **type**="customer"**\>**  <br>                **\<id** **column**="customer_id" **property**="customerId"**/\>**  <br>                **\<result** **column**="customer_name" **property**="customerName"**/\>**  <br>                **\<collection** **proeprty**="orderList" **ofType**="order"**\>**  <br>                        **\<id** **column**="order_id" **property**="orderId"**/\>**  <br>                        **\<result** **column**="order_name" **property**="orderName"**/\>**  <br>                        **\<result** **column**="customer_id" **property**="customerId"**/\>**  <br>                **\</collection\>**  <br>        **\</resultMap\>**  <br>        **\<select** **id**="queryList" **resultMap**="customerMap"**\>**  <br>                SELECT * FROM t_order tor JOIN t_customer tur ON tor.customer_id = tur.customer_id;  <br>        **\</select\>**  <br>**\</mapper\>**|

1 \<resultMap\>是映射的顶层容器，用于定义从ResultSet到Java对象的映射规则

|   |   |
|---|---|
|属性|含义|
|id|resultMap的唯一标识|
|type|映射的目标Java类型（全限定类名或别名）|
|property|Java对象的属性名|
|column|数据库列名（或别名）|

2 \<association\>用于映射单个关联对象

|   |   |
|---|---|
|属性|含义|
|property|Java对象中关联属性的名称|
|javaType|关联对象的Java类型|
|column|传递给子查询的列名|

3 \<collection\>用于映射集合属性

|   |   |
|---|---|
|属性|含义|
|property|Java对象中集合属性的名称|
|ofType|集合中元素的类型（即泛型类型）|
|column|传递给子查询的列|

### 多表映射总结

|   |   |   |
|---|---|---|
|关联关系|配置项关键词|所在配置文件和具体位置|
|对一|association标签/javaType属性/property属性|Mapper配置文件中的resultMap标签内|
|对多|collection标签/ofType属性/property属性|Mapper配置文件中的resultMap标签内|
 
# MyBatis动态语句

## if和where标签
 
|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16|**\<mapper** **namespace**="com.prokyhoof.mapper.EmployeeMapper"**\>**  <br>        // where标签的作用有两个：  <br>        // **1** 自动添加where关键字，where内部有任何一个if满足，自动添加where关键字，不满足去掉where  <br>        // **2** 自动去掉多余的and 和 or 关键字  <br>        **\<select** **id**="query" **resultType**="employee"**\>**  <br>                SELECT * FROM t_emp  <br>                **\<where\>**  <br>                        **\<if** **test**="name != null"**\>**  <br>                                emp_name = #{name}  <br>                        **\</if\>**  <br>                        **\<if** **test**="salary != null and salary &gt; 100\>  <br>                                and emp_salary = #{salary};  <br>                        \</if\>  <br>                \</where\>  <br>        \</select\>  <br>\</mapper\>|

## set标签

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18|**\<update** **id**="updateEmployeeDynamic"**\>**  <br>        UPDATE t_emp  <br>        // set emp_name = #{empName}, emp_salary = #{empSalary}  <br>        // 使用set标签动态管理set子句，并且动态去掉两端多余的逗号  <br>        **\<set\>**  <br>                **\<if** **test**="empName != null"**\>**  <br>                        emp_name = #{empName},  <br>                **\</if\>**  <br>                **\<if\>**  <br>                        emp_salary = #{empSalary},  <br>                **\</if\>**  <br>        **\</set\>**  <br>        WHERE emp_id = #{empId}  <br>        // 第一种情况：所有条件都满足 SET emp_name = ?, emp_salary = ?  <br>        // 第二种情况：部分条件满足 SET emp_salary = ?  <br>        // 第三种情况：所有条件都不满足 UPDATE t_emp WHERE emp_id = ?  <br>        // 没有set子句的update语句会导致SQL语法错误  <br>**\</update\>**|

## trim标签

使用trim标签控制条件部分两端是否包含某些字符  
1 prefix属性：指定要动态添加的前缀  
2 suffix属性：指定要动态添加的后缀  
3 prefixOverrides属性：指定要动态去掉的前缀，使用“|”分隔有可能的多个值  
4 suffixOverrides属性：指定要动态去掉的后缀，使用“|”分隔有可能的多个值

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17|**\<select** **id**="selectEmployeeByConditionByTrim" **resultType**="com.prokyhoof.mybatis.entity"**\>**  <br>        SELECT emp_id, emp_name, emp_age, emp_salary, emp_gender FROM t_emp;  <br>        **\<trim** **prefix**="where" **suffixOverrides**="and \| or"**\>**  <br>                **\<if** **test**="empName != null"**\>**  <br>                        emp_name = #{name} and  <br>                **\</if\>**  <br>                **\<if** **test**="empSalary &gt; 3000"**\>**  <br>                        emp_salary **\>** #{empSalary} and  <br>                **\</if\>**  <br>                **\<if** **test**="empAge &lt;= 20"**\>**  <br>                        emp_age = #{empAge} or  <br>                **\</if\>**  <br>                **\<if** **test**="empGender == 'male'"**\>**  <br>                        emp_gender = #{empGender}  <br>                **\</if\>**  <br>        **\</trim\>**  <br>**\</select\>**|

## choose/when/otherwise标签

在多个分支条件中，仅执行一个  
1 从上到下依次执行条件判断  
2 遇到的第一个满足条件的分支会被采纳  
3 被采纳分支后面的分支都将不被考虑  
4 如果所有的when分支都不满足，那么就执行otherwise分支

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14|**\<select** **id**="selectEmployeeByConditionByChoose" **resultType**="com.prokyhoof.mybatis.entity"**\>**  <br>        SELECT emp_id, emp_name, emp_salary FROM t_emp WHERE  <br>        **\<choose\>**  <br>                **\<when** **test**="empName != null" **\>**  <br>                 emp_name = #{empName}  <br>                **\</when\>**  <br>                **\<when** **test**="empSalary &lt; 3000"**\>**  <br>                 emp_salary &lt; **3000**  <br>                **\</when\>**  <br>                **\<otherwise\>**  <br>                 **1** = **1**  <br>                **\</otherwise\>**  <br>        **\</choose\>**  <br>**\</select\>**|

## foreach标签

collection属性：要遍历的集合对象。MyBatis会根据传入参数类型自动识别  
1 如果是List，默认用“list”  
2 如果是Array，默认用"array"  
3 如果是Map，可用key名  
4 如果是自定义参数（@Param），用@Param("xxx")指定的名称  
item属性：集合中每个元素的别名，在循环体内部通过#{item}引用  
open属性：循环开始前拼接的字符串  
close属性：循环结束后拼接的字符串  
separator属性：每次迭代之间的分隔符  
关于foreach标签的collection属性：  
如果没有给接口中List类型的参数使用@Param注解指定一个具体的名字，那么在collection属性中默认可以使用collection或list来引用这个list集合，这一点可以通过异常信息看出来  
在实际开发中，为了避免隐晦的表达造成一定的误会，建议使用@Param注解明确声明变量的名称，然后在foreach标签的collection属性中按照@Param注解指定的名称来引用传入的参数

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13|**\<delete** **id**="deleteBatch"**\>**  <br>DELETE FROM t_emp WHERE id IN  <br>**\<foreach** **collection**="ids" **open**="[" **separator**="," **close**="]" **item**="id"**\>**  <br>#{id}  <br>**\</foreach\>**  <br>**\</delete\>**<br><br>  <br><br>**\<insert** **id**="deleteBatch"**\>**  <br>INSERT INTO t_emp (emp_name, emp_salary) VALUES  <br>**\<foreach** **collection**="list" **separator**="," **item**="employee"**\>**  <br>(#{employee.emp_name}, #{employee.emp_salary})  <br>**\</foreach\>**  <br>**\</insert\>**|

## sql片段

抽取重复的SQL片段

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|// 使用sql标签抽取重复出现的SQL片段  <br>**\<sql** **id**="mySelectSql"**\>**  <br>SELECT emp_id, emp_name, emp_age, emp_salary, emp_gender FROM t_emp  <br>**\</sql\>**|

引用已抽取的SQL片段

|   |   |
|---|---|
|1  <br>2|// 使用include标签引用声明的SQL片段  <br>**\<include** **refid**="mySelectSql"**/\>**|

# MyBatis高级扩展

## Mapper批量映射优化

## 插件和页面插件PageHelper

### 插件机制和PageHelper插件介绍

MyBatis的插件机制包括一下三种组件：￼ 1 Interceptor（拦截器）：定义一个拦截方法intercept，该方法在执行SQL语句，执行查询、查询结果的映射时会被调用  
2 Invocation（调用）：实际上是对拦截的方法对封装，封装了Object target、Method method和Object[] args这三个字段  
3 InterceptorChain（连接器链）：对所有的拦截器进行管理，包含将所有的Interceptor链接成一个链，并在执行SQL语句时按顺序调用  
插件的开发非常简单，只需要实现Interceptor接口，并使用注解@Intercepts来标注需要拦截的对象和发放，然后在MyBatis的配置文件中添加插件即可  
PageHelper是MyBatis中的分页插件，它提供了多重分页方式（例如MySQL和Oracle分页方式），支持多种数据库

### PagerHelper插件使用

1 pom.xml引入依赖

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|**\<dependency\>**  <br>**\<groupId\>**com.github.pagehelper**\</groupId\>**  <br>**\<artifactId\>**pagehelper**\<artifactId\>**  <br>**\<version\>****5.1.11****\</version\>**  <br>**\</dependency\>**|

2 mybatis-config.xml配置分页插件  
在MyBatis的配置文件中添加PageHelper的插件

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|**\<plugins\>**  <br>**\<plugin** **interceptor**="com.guithub.pagehelper.PageInterceptor"**\>**  <br>**\<property** **name**="helperDialect" **value**="mysql"**/\>**  <br>**\</plugin\>**  <br>**\</plugins\>**|

其中，com.github.pagehelper.PageInterceptor是PageHelper插件的名称，dialect属性用于指定数据库类型（支持多重数据库）  
3 页插件使用  
在查询方法中使用分页

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18  <br>19  <br>20  <br>21|@Test  <br>**public void** testTeacherRelationshipToMulti**() {**  <br>TeacherMapper taecherMapper **=** session**.**getMapper**(**TeacherMapper**.****class****);**  <br>PageHelper**.**startPage**(****1****,** **2****);**  <br>// 查询Customer对象同时将关联的Order集合查询出来  <br>List**\<**Teacher**\>** allTeachers **=** teacherMapper**.**findAllTeachers**();**  <br>PageInfo**\<**Teacher**\>** pageInfo **=** **new** PageInfo**\<\>(**allTeachers**);**  <br>  <br>System**.**out**.**println**(**"pageInfo = " **+** pageInfo**);**  <br>**long** total **=** pageInfo**.**getTotal**();** // 获取总记录数  <br>System**.**out**.**println**(**"total = " **+** total**);**  <br>**int** pages **=** pageInfo**.**getPages**();** // 获取总页数  <br>System**.**out**.**println**(**"pages = " **+** pages**);**  <br>**int** pageNum **=** pageInfo**.**getPageNum**();** // 获取当前页码  <br>System**.**out**.**println**(**"pageNum = " **+** paegNum**);**  <br>**int** pageSize **=** pageInfo**.**getPageSize**();** // 获取每页显示记录数  <br>System**.**out**.**println**(**"pageSize = " **+** pageSize**);**  <br>List**\<**Teacher**\>** teachers **=** pageInfo**.**getList**();** // 获取查询页的数据集合  <br>System**.**out**.**println**(**"teachers = " **+** teachers**);**  <br>teachers**.**forEach**(**System**.**out**::**println**);**  <br>**}**|

## 逆向工程和MyBatis插件

### ORM思维介绍

ORM（Object-Relational Mapping，对象-关系映射）是一种将数据库和面向对象编程语言中的对象之间进行转换的计数，他将对象和关系数据库的概念进行映射。使用面向对象思维进行数据库操作  
ORM框架通常有半自动和全自动两种方式：  
1 半自动ORM通常需要程序员手动编写SQL语句或者配置文件，将实体类和数据表进行映射，还需要手动将查询的结果集转换成实体对象  
2 全自动ORM则是将实体类和数据表进行自动映射，使用API进行数据库操作时，ORM框架会自动执行SQL语句并将查询结果转换成实体对象，程序员无需再手动编写SQL语句和转换代码  
常见的半自动ORM框架包括MyBatis等；常见的全自动ORM框架包含Hibernate、Spring Data JPA、MyBatis-Plus等

### 逆向工程

MyBatis的逆行工程是一种自动化生成持久层代码和映射文件的工具，它可以根据数据表结果和设置的参数生成对应的实体类、Mapper.xml文件、Mapper接口等代码文件，简化了开发者手动生成的过程。逆向工程使开发者可以快速地构建起DAO层，并快速上手进行业务开发  
MyBatis的逆向工程有两种方式：  
1 用过MyBatis Generator插件实现  
2 通过Maven插件实现  
逆向工程一般需要指定一些配置参数，例如数据库链接URL、用户名、密码、要生成的表名、生成的文件路径等等  
注意：逆向工程只能生成单表CROD的操作，多表查询依然需要我们自己编写

### 逆向工程插件MyBatisX使用

MyBatisX是一个MyBatis的代码生成插件，可以通过简单的配置和操作快速生成MyBatis Mapper、pojo类和Mapper.xml文件