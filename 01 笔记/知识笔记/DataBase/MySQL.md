---
tags:
  - knowledge
introduction: 数据库基础
start_date: 2026-10-15
---

# 1 基础

## 1-1 MySQL概述

### 1-1-1 数据库相关概念
### 1-1-2 MySQL数据库

#### 1-1-2-1 关系型数据库（RDBMS）

概念：建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

1. 使用表存储数据，统一结构，便于维护。
2. 使用 SQL 语言操作，标准统一，使用方便。

#### 1-1-2-2 MySQL数据模型

MySQL 中的数据按"数据库 → 表 → 数据行"的层次组织：一个数据库中可以有多张表，每张表由行和列组成，数据以记录形式存放在表中。

数据库  
表

#### 1-1-2-3 MySQL启动

特点：

```vtable
{"rows": [[{"t": "项目", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "默认端口", "rs": 1, "cs": 1}, {"t": "3306", "rs": 1, "cs": 1}], [{"t": "默认字符集", "rs": 1, "cs": 1}, {"t": "utf8mb4", "rs": 1, "cs": 1}], [{"t": "配置文件", "rs": 1, "cs": 1}, {"t": "my.ini（Windows）/ my.cnf（Linux）", "rs": 1, "cs": 1}], [{"t": "默认账号", "rs": 1, "cs": 1}, {"t": "root（管理员）", "rs": 1, "cs": 1}], [{"t": "服务名", "rs": 1, "cs": 1}, {"t": "MySQL（Windows 服务）", "rs": 1, "cs": 1}]]}
```

## 1-2 SQL

### 1-2-1 SQL通用语法

- SQL 语句可以单行或多行书写，以分号结尾。
- SQL 语句可以使用空格/缩进增强语句的可读性。
- MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写。
- 注释：

1. 单行注释：-- 注释内容 或 # 注释内容（MySQL 特有）
2. 多行注释：/* 注释内容*/

### 1-2-2 SQL分类

```vtable
{"rows": [[{"t": "分类", "rs": 1, "cs": 1}, {"t": "全称", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "DDL", "rs": 1, "cs": 1}, {"t": "Data Definition Language", "rs": 1, "cs": 1}, {"t": "数据定义语言，定义数据库、表、字段等结构（CREATE/ALTER/DROP）", "rs": 1, "cs": 1}], [{"t": "DML", "rs": 1, "cs": 1}, {"t": "Data Manipulation Language", "rs": 1, "cs": 1}, {"t": "数据操作语言，对表中数据进行增删改（INSERT/UPDATE/DELETE）", "rs": 1, "cs": 1}], [{"t": "DQL", "rs": 1, "cs": 1}, {"t": "Data Query Language", "rs": 1, "cs": 1}, {"t": "数据查询语言，查询表中数据（SELECT）", "rs": 1, "cs": 1}], [{"t": "DCL", "rs": 1, "cs": 1}, {"t": "Data Control Language", "rs": 1, "cs": 1}, {"t": "数据控制语言，设置权限、控制访问（GRANT/REVOKE）", "rs": 1, "cs": 1}]]}
```

### 1-2-3 DDL

#### 1-2-3-1 DDL-数据库操作

查询所有数据库：

```sql
SHOW DATABASES;
```

查询当前数据库：

```sql
SELECT DATABASE();
```

创建数据库：

```sql
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
```

删除数据库：

```sql
DROP DATABASE [IF EXISTS] 数据库名;
```

使用数据库：

```sql
USE 数据库名;
```

#### 1-2-3-2 DDL-表操作-查询

查询当前数据库所有表：

```sql
SHOW TABLES;
```

查询表结构：

```sql
DESC 表名;
```

查询指定表的建表语句：

```sql
SHOW CREATE TABLE 表名;
```

#### 1-2-3-3 DDL-表操作-创建

```sql
CREATE TABLE 表名(
    字段1 字段1类型 [COMMENT 字段1注释],
    字段2 字段2类型 [COMMENT 字段2注释],
    ...
)[COMMENT 表注释];
```

#### 1-2-3-4 DDL-表操作-数据类型

MySQL 中的数据类型有很多，主要分为三类：数值类型、字符串类型、日期时间类型。  
数值类型：

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "大小", "rs": 1, "cs": 1}, {"t": "有符号范围", "rs": 1, "cs": 1}, {"t": "无符号范围", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "TINYINT", "rs": 1, "cs": 1}, {"t": "1 字节", "rs": 1, "cs": 1}, {"t": "-128 ~ 127", "rs": 1, "cs": 1}, {"t": "0 ~ 255", "rs": 1, "cs": 1}, {"t": "小整数", "rs": 1, "cs": 1}], [{"t": "SMALLINT", "rs": 1, "cs": 1}, {"t": "2 字节", "rs": 1, "cs": 1}, {"t": "-32768 ~ 32767", "rs": 1, "cs": 1}, {"t": "0 ~ 65535", "rs": 1, "cs": 1}, {"t": "中等整数", "rs": 1, "cs": 1}], [{"t": "INT", "rs": 1, "cs": 1}, {"t": "4 字节", "rs": 1, "cs": 1}, {"t": "-2^31 ~ 2^31-1", "rs": 1, "cs": 1}, {"t": "0 ~ 2^32-1", "rs": 1, "cs": 1}, {"t": "普通整数", "rs": 1, "cs": 1}], [{"t": "BIGINT", "rs": 1, "cs": 1}, {"t": "8 字节", "rs": 1, "cs": 1}, {"t": "-2^63 ~ 2^63-1", "rs": 1, "cs": 1}, {"t": "0 ~ 2^64-1", "rs": 1, "cs": 1}, {"t": "大整数", "rs": 1, "cs": 1}], [{"t": "FLOAT", "rs": 1, "cs": 1}, {"t": "4 字节", "rs": 1, "cs": 1}, {"t": "单精度浮点", "rs": 1, "cs": 1}, {"t": "—", "rs": 1, "cs": 1}, {"t": "单精度浮点数", "rs": 1, "cs": 1}], [{"t": "DOUBLE", "rs": 1, "cs": 1}, {"t": "8 字节", "rs": 1, "cs": 1}, {"t": "双精度浮点", "rs": 1, "cs": 1}, {"t": "—", "rs": 1, "cs": 1}, {"t": "双精度浮点数", "rs": 1, "cs": 1}], [{"t": "DECIMAL(M,D)", "rs": 1, "cs": 1}, {"t": "M+2 字节", "rs": 1, "cs": 1}, {"t": "定点数", "rs": 1, "cs": 1}, {"t": "—", "rs": 1, "cs": 1}, {"t": "精确小数，M 总位数，D 小数位数", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20333f78f3886ea5a0.png)

字符串类型：

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "描述", "rs": 1, "cs": 1}], [{"t": "CHAR", "rs": 1, "cs": 1}, {"t": "定长字符串", "rs": 1, "cs": 1}], [{"t": "VARCHAR", "rs": 1, "cs": 1}, {"t": "变长字符串", "rs": 1, "cs": 1}], [{"t": "TINYBLOB", "rs": 1, "cs": 1}, {"t": "不超过 255 个字符的二进制数据", "rs": 1, "cs": 1}], [{"t": "TINYTEXT", "rs": 1, "cs": 1}, {"t": "短文本字符串", "rs": 1, "cs": 1}], [{"t": "BLOB", "rs": 1, "cs": 1}, {"t": "二进制形式的长文本数据", "rs": 1, "cs": 1}], [{"t": "TEXT", "rs": 1, "cs": 1}, {"t": "长文本数据", "rs": 1, "cs": 1}], [{"t": "MEDIUMBLOB", "rs": 1, "cs": 1}, {"t": "二进制形式的中等长度文本数据", "rs": 1, "cs": 1}], [{"t": "MEDIUMTEXT", "rs": 1, "cs": 1}, {"t": "中等长度文本数据", "rs": 1, "cs": 1}], [{"t": "LONGBLOB", "rs": 1, "cs": 1}, {"t": "二进制形式的极大文本数据", "rs": 1, "cs": 1}], [{"t": "LONGTEXT", "rs": 1, "cs": 1}, {"t": "极大文本数据", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%208eb2e809976c17f3.png)

日期时间类型：

```vtable
{"rows": [[{"t": "类型", "rs": 1, "cs": 1}, {"t": "大小", "rs": 1, "cs": 1}, {"t": "格式", "rs": 1, "cs": 1}, {"t": "描述", "rs": 1, "cs": 1}], [{"t": "DATE", "rs": 1, "cs": 1}, {"t": "3", "rs": 1, "cs": 1}, {"t": "YYYY-MM-DD", "rs": 1, "cs": 1}, {"t": "日期值", "rs": 1, "cs": 1}], [{"t": "TIME", "rs": 1, "cs": 1}, {"t": "3", "rs": 1, "cs": 1}, {"t": "HH:MM:SS", "rs": 1, "cs": 1}, {"t": "时间值或持续时间", "rs": 1, "cs": 1}], [{"t": "YEAR", "rs": 1, "cs": 1}, {"t": "1", "rs": 1, "cs": 1}, {"t": "YYYY", "rs": 1, "cs": 1}, {"t": "年份值", "rs": 1, "cs": 1}], [{"t": "DATETIME", "rs": 1, "cs": 1}, {"t": "8", "rs": 1, "cs": 1}, {"t": "YYYY-MM-DD HH:MM:SS", "rs": 1, "cs": 1}, {"t": "混合日期和时间值", "rs": 1, "cs": 1}], [{"t": "TIMESTAMP", "rs": 1, "cs": 1}, {"t": "4", "rs": 1, "cs": 1}, {"t": "YYYY-MM-DD HH:MM:SS", "rs": 1, "cs": 1}, {"t": "混合日期和时间值，时间戳", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%203cd4fc115fac3fce.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20200a93e1412dbac6.png)

#### 1-2-3-5 DDL-表操作-修改

添加字段：

```sql
ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
```

修改数据类型：

```sql
ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
```

修改字段和字段类型：

```sql
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
```

删除字段：

```sql
ALTER TABLE 表名 DROP 字段名;
```

修改表名：

```sql
ALTER TABLE 表名 RENAME TO 新表名;
```

#### 1-2-3-6 DDL-表操作-删除

删除表：

```sql
DROP TABLE [IF EXISTS] 表名;
```

删除指定表，并重新创建该表：

```sql
TRUNCATE TABLE 表名;
```

> 注意：在删除表时，表中的全部数据也会被删除。  

## 1-3 事务

### 1-3-1 事务的简介

事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。  
默认 MySQL 的事务是自动提交的，也就是说，当执行一条 DML 语句，MySQL 会立即隐式的提交事务。

### 1-3-2 事务操作

事务的基本操作流程为：开启事务 → 执行 SQL → 提交/回滚。

```sql
-- 开启事务（二选一）
BEGIN;
START TRANSACTION;

-- 执行增删改操作
UPDATE t_emp SET salary = 10000 WHERE emp_id = 1;

-- 提交事务（确认操作生效）
COMMIT;

-- 回滚事务（撤销操作）
ROLLBACK;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20e5e1b2e255fbc8ad.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%207654d12800ff5745.png)

### 1-3-3 事务四大特性（ACID）

- 原子性（Atomicity）：事务是不可分割的最小操作单元，要么全部成功，要么全部失败。
- 一致性（Consistency）：事务完成时，必须使所有的数据都保持一致状态。
- 隔离性（Isolation）：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行。
- 持久性（Durability）：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。

### 1-3-4 并发事务问题

并发事务可能产生脏读、不可重复读、幻读等问题：

```vtable
{"rows": [[{"t": "问题", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "脏读", "rs": 1, "cs": 1}, {"t": "一个事务读到另一个事务还未提交的数据", "rs": 1, "cs": 1}], [{"t": "不可重复读", "rs": 1, "cs": 1}, {"t": "一个事务前后两次读取的数据不一致（另一事务已提交更新）", "rs": 1, "cs": 1}], [{"t": "幻读", "rs": 1, "cs": 1}, {"t": "一个事务前后两次查询结果行数不一致（另一事务已提交插入）", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2023f423e830e8d8d6.png)

### 1-3-5 事务隔离级别

```vtable
{"rows": [[{"t": "隔离级别", "rs": 1, "cs": 1}, {"t": "脏读", "rs": 1, "cs": 1}, {"t": "不可重复读", "rs": 1, "cs": 1}, {"t": "幻读", "rs": 1, "cs": 1}], [{"t": "读未提交（Read Uncommitted）", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}], [{"t": "读已提交（Read Committed）", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}], [{"t": "可重复读（Repeatable Read）", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}, {"t": "可能", "rs": 1, "cs": 1}], [{"t": "串行化（Serializable）", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}, {"t": "不可能", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20d7060407082aeafb.png)

> 注意：事务隔离级别越高，数据越安全，但是性能越低。  

## 1-4 DML

DML 英文全称是 Data Manipulation Language（数据操作语言），用来对数据库中表的数据记录进行增删改操作。

- 添加数据（INSERT）
- 修改数据（UPDATE）
- 删除数据（DELETE）

添加数据：

```sql
INSERT INTO 表名 (字段1, 字段2, ...) VALUES (值1, 值2, ...);
```

修改数据：

```sql
UPDATE 表名 SET 字段名1 = 值1, 字段名2 = 值2, ... [WHERE 条件];
```

删除数据：

```sql
DELETE FROM 表名 [WHERE 条件];
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2037b6f35657bea438.png)

> 注意：  
> 1. 插入数据时，指定的字段顺序需要与值的顺序是一一对应的。  
> 2. 字符串和日期型数据应该包含在引号中。  
> 3. 插入的数据大小，应该在字段的规定范围内。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%202f20c17d7754dccf.png)

> 注意：修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2068c9a6f79677c34b.png)

> 注意：  
> 1. DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。  
> 2. DELETE 语句不能删除某一个字段的值（可以使用 UPDATE）。  

## 1-5 DQL

DQL 英文全称是 Data Query Language（数据查询语言），用来查询数据库中表的记录。完整查询语法结构如下：

```sql
SELECT 字段列表
FROM 表名列表
WHERE 条件列表
GROUP BY 分组字段列表
HAVING 分组后条件列表
ORDER BY 排序字段列表
LIMIT 分页参数;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%204f3ecf3144d40782.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%202faa8cd06dad33dc.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2039bb2a72807be630.png)

### 1-5-1 聚合函数

聚合函数：将一列数据作为一个整体，进行纵向计算。常见的聚合函数如下：

```vtable
{"rows": [[{"t": "函数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "COUNT", "rs": 1, "cs": 1}, {"t": "统计数量", "rs": 1, "cs": 1}], [{"t": "MAX", "rs": 1, "cs": 1}, {"t": "最大值", "rs": 1, "cs": 1}], [{"t": "MIN", "rs": 1, "cs": 1}, {"t": "最小值", "rs": 1, "cs": 1}], [{"t": "SUM", "rs": 1, "cs": 1}, {"t": "求和", "rs": 1, "cs": 1}], [{"t": "AVG", "rs": 1, "cs": 1}, {"t": "平均值", "rs": 1, "cs": 1}]]}
```

语法：

```sql
SELECT 聚合函数(字段列表) FROM 表名;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20684852ad863ecc10.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2011647c3c43ba92c4.png)

> 注意：null 值不参与所有聚合函数运算。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20d4af4a91c4b31d81.png)

### 1-5-2 分组查询

where 与 having 区别：

- 执行时机不同：where 是分组之前进行过滤，不满足 where 条件，不参与分组，而 having 是分组之后对结果进行过滤。
- 判断条件不同：where 不能对聚合函数进行判断，而 having 可以。

> 注意：  
> 1. 执行顺序：where > 聚合函数 > having。  
> 2. 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20471657dfa2579298.png)

### 1-5-3 排序查询

排序方法：

- ASC：升序（默认值）
- DESC：降序

> 注意：如果是多字段排序，当前一个字段值相同时，才会根据第二个字段进行排序。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20fbc95ddd6a0d40af.png)

### 1-5-4 分页查询

```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;
```

> 注意：  
> 1. 起始索引从 0 开始，起始索引 =（查询页码 - 1）* 每页显示记录数。  
> 2. 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL 中是 LIMIT。  
> 3. 如果查询的是第一页数据，起始索引可以省略，直接简写为 LIMIT 10。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2056d3c53f83600131.png)

### 1-5-5 DQL综合案例

创建员工表并插入数据：

```sql
CREATE TABLE emp(
    id INT COMMENT '编号',
    workno VARCHAR(10) COMMENT '工号',
    name VARCHAR(10) COMMENT '姓名',
    gender CHAR(1) COMMENT '性别',
    age TINYINT UNSIGNED COMMENT '年龄',
    idcard CHAR(18) COMMENT '身份证号',
    entrydate DATE COMMENT '入职时间'
) COMMENT '员工信息表';
```

综合查询：

```sql
SELECT * FROM emp WHERE gender = '女' AND age IN (20, 21, 22, 23);

SELECT * FROM emp WHERE gender = '男' AND (age BETWEEN 20 AND 40) AND name LIKE '___';

SELECT gender, COUNT(*) FROM emp WHERE age < 60 GROUP BY gender;

SELECT name, age FROM emp WHERE age <= 35 ORDER BY age ASC, entrydate DESC;

SELECT * FROM emp WHERE gender = '男' AND (age BETWEEN 20 AND 40) ORDER BY age ASC, entrydate ASC LIMIT 0, 5;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2000e76644f5e836db.png)

## 1-6 DCL

DCL 英文全称是 Data Control Language（数据控制语言），用来管理数据库用户，控制数据库的访问权限。

### 1-6-1 管理用户

查询用户：

```sql
USE mysql;
SELECT * FROM user;
```

创建用户：

```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```

修改用户密码：

```sql
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```

删除用户：

```sql
DROP USER '用户名'@'主机名';
```

> 注意：  
> 1. 主机名可以使用 % 通配。  
> 2. 这类 SQL 开发人员操作的比较少，主要是 DBA（Database Administrator 数据库管理员）使用。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20039405b2e55d6fab.png)

### 1-6-2 权限控制

查询权限：

```sql
SHOW GRANTS FOR '用户名'@'主机名';
```

授予权限：

```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

撤销权限：

```sql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```

> 注意：  
> 1. 多个权限之间，使用逗号分隔。  
> 2. 授权时，数据库名和表名可以使用 * 进行通配，代表所有。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20f9a9c35dd20c8678.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%202df4f5c58dd75ce2.png)

## 1-7 函数

函数是指一段可以直接被另一段程序调用的程序或代码。MySQL 内置函数按功能可分为字符串函数、数值函数、日期函数、流程控制函数等。

### 1-7-1 字符串函数

MySQL 中内置了很多字符串函数，常用的几个如下：

```vtable
{"rows": [[{"t": "函数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "CONCAT(s1,s2,...)", "rs": 1, "cs": 1}, {"t": "字符串拼接", "rs": 1, "cs": 1}], [{"t": "LOWER(str)", "rs": 1, "cs": 1}, {"t": "全部转小写", "rs": 1, "cs": 1}], [{"t": "UPPER(str)", "rs": 1, "cs": 1}, {"t": "全部转大写", "rs": 1, "cs": 1}], [{"t": "LPAD(str,n,pad)", "rs": 1, "cs": 1}, {"t": "左填充，用 pad 对 str 左侧进行填充至 n 个字符", "rs": 1, "cs": 1}], [{"t": "RPAD(str,n,pad)", "rs": 1, "cs": 1}, {"t": "右填充，用 pad 对 str 右侧进行填充至 n 个字符", "rs": 1, "cs": 1}], [{"t": "TRIM(str)", "rs": 1, "cs": 1}, {"t": "去掉字符串头部和尾部的空格", "rs": 1, "cs": 1}], [{"t": "SUBSTRING(str,start,len)", "rs": 1, "cs": 1}, {"t": "返回从 start 位置开始的 len 个长度的子串", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%203ea5a07bf4325492.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20ee0f788bf903f722.png)

示例：将 emp 表中员工的工号统一补齐为 5 位，不足左侧补 0：

```sql
UPDATE emp SET workno = LPAD(workno, 5, '0');
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%202b07d9c2901118f1.png)

### 1-7-2 数值函数

常见的数值函数如下：

```vtable
{"rows": [[{"t": "函数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "CEIL(x)", "rs": 1, "cs": 1}, {"t": "向上取整", "rs": 1, "cs": 1}], [{"t": "FLOOR(x)", "rs": 1, "cs": 1}, {"t": "向下取整", "rs": 1, "cs": 1}], [{"t": "MOD(x,y)", "rs": 1, "cs": 1}, {"t": "返回 x/y 的模", "rs": 1, "cs": 1}], [{"t": "RAND()", "rs": 1, "cs": 1}, {"t": "返回 0~1 内的随机数", "rs": 1, "cs": 1}], [{"t": "ROUND(x,y)", "rs": 1, "cs": 1}, {"t": "求参数 x 的四舍五入的值，保留 y 位小数", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20caf3089c5009be43.png)

示例：生成一个 6 位随机验证码：

```sql
SELECT LPAD(ROUND(RAND() * 1000000, 0), 6, '0');
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20367203e9df3b8436.png)

### 1-7-3 日期函数

常见的日期函数如下：

```vtable
{"rows": [[{"t": "函数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "CURDATE()", "rs": 1, "cs": 1}, {"t": "返回当前日期", "rs": 1, "cs": 1}], [{"t": "CURTIME()", "rs": 1, "cs": 1}, {"t": "返回当前时间", "rs": 1, "cs": 1}], [{"t": "NOW()", "rs": 1, "cs": 1}, {"t": "返回当前日期和时间", "rs": 1, "cs": 1}], [{"t": "YEAR(date)", "rs": 1, "cs": 1}, {"t": "获取指定 date 的年份", "rs": 1, "cs": 1}], [{"t": "MONTH(date)", "rs": 1, "cs": 1}, {"t": "获取指定 date 的月份", "rs": 1, "cs": 1}], [{"t": "DAY(date)", "rs": 1, "cs": 1}, {"t": "获取指定 date 的日期", "rs": 1, "cs": 1}], [{"t": "DATE_ADD(date, INTERVAL expr type)", "rs": 1, "cs": 1}, {"t": "返回一个日期/时间值加上一个时间间隔 expr 后的时间值", "rs": 1, "cs": 1}], [{"t": "DATEDIFF(date1, date2)", "rs": 1, "cs": 1}, {"t": "返回起始时间 date1 和结束时间 date2 之间的天数", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2040a7c079fe97a951.png)

示例：查询员工的入职天数，并按入职天数倒序排序：

```sql
SELECT name, DATEDIFF(CURDATE(), entrydate) FROM emp ORDER BY entrydate DESC;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%203e05d58a2b4a1570.png)

### 1-7-4 流程控制函数

流程控制函数可以在 SQL 语句中实现条件筛选，从而提高语句的效率。

```vtable
{"rows": [[{"t": "函数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "IF(value, t, f)", "rs": 1, "cs": 1}, {"t": "如果 value 为 true，则返回 t，否则返回 f", "rs": 1, "cs": 1}], [{"t": "IFNULL(value1, value2)", "rs": 1, "cs": 1}, {"t": "如果 value1 不为空，返回 value1，否则返回 value2", "rs": 1, "cs": 1}], [{"t": "CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2 ... ELSE 结果n END", "rs": 1, "cs": 1}, {"t": "多条件分支判断", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2006f23314bb0a7197.png)

示例：根据成绩等级评定学生各科成绩：

```sql
SELECT id, name,
(CASE WHEN math >= 85 THEN '优秀' WHEN math >= 60 THEN '及格' ELSE '不及格' END) AS '数学',
(CASE WHEN english >= 85 THEN '优秀' WHEN english >= 60 THEN '及格' ELSE '不及格' END) AS '英语',
(CASE WHEN chinese >= 85 THEN '优秀' WHEN chinese >= 60 THEN '及格' ELSE '不及格' END) AS '语文'
FROM score;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20ec715a90fbff352d.png)

## 1-8 约束

### 1-8-1 概述

1. 概念：约束是作用于表中字段上的规则，用于限制存储在表中的数据。
2. 目的：保证数据库中数据的正确、有效性和完整性。
3. 分类：

```vtable
{"rows": [[{"t": "约束", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "NOT NULL", "rs": 1, "cs": 1}, {"t": "非空约束，限制该字段的数据不能为 null", "rs": 1, "cs": 1}], [{"t": "UNIQUE", "rs": 1, "cs": 1}, {"t": "唯一约束，保证该字段的所有数据都是唯一、不重复的", "rs": 1, "cs": 1}], [{"t": "PRIMARY KEY", "rs": 1, "cs": 1}, {"t": "主键约束，主键是一行数据的唯一标识，要求非空且唯一", "rs": 1, "cs": 1}], [{"t": "DEFAULT", "rs": 1, "cs": 1}, {"t": "默认约束，保存数据时，如果未指定该字段的值，则采用默认值", "rs": 1, "cs": 1}], [{"t": "CHECK", "rs": 1, "cs": 1}, {"t": "检查约束，保证字段值满足某一个条件", "rs": 1, "cs": 1}], [{"t": "FOREIGN KEY", "rs": 1, "cs": 1}, {"t": "外键约束，用来让两张表的数据之间建立连接，保证数据的一致性和完整性", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%205e1fee093740cf7f.png)

> 注意：约束是作用于表中字段上的，可以在创建、修改表的时候添加约束。  

### 1-8-2 约束演示

```sql
CREATE TABLE user(
    id INT PRIMARY KEY AUTO_INCREMENT COMMENT '主键',
    name VARCHAR(10) NOT NULL UNIQUE COMMENT '姓名',
    age INT CHECK (age > 0 AND age <= 120) COMMENT '年龄',
    status CHAR(1) DEFAULT '1' COMMENT '状态',
    gender CHAR(1) COMMENT '性别'
) COMMENT '用户表';
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20c8f461876bb8228d.png)

### 1-8-3 外键约束

概述：外键用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%204f4232c33437d1c4.png)

> 注意：目前上述的两张表，在数据库层面，并未建立外键关联，所以是无法保证数据的一致性和完整性的。  

添加外键：

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (字段名) REFERENCES 主表(列名);
```

删除外键：

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20b93e20d58aef8be7.png)

删除/更新行为：

```vtable
{"rows": [[{"t": "行为", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "NO ACTION", "rs": 1, "cs": 1}, {"t": "当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新（与 RESTRICT 一致）", "rs": 1, "cs": 1}], [{"t": "RESTRICT", "rs": 1, "cs": 1}, {"t": "当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新", "rs": 1, "cs": 1}], [{"t": "CASCADE", "rs": 1, "cs": 1}, {"t": "当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录", "rs": 1, "cs": 1}], [{"t": "SET NULL", "rs": 1, "cs": 1}, {"t": "当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有，则设置子表中该外键值为 null（要求该外键允许取 null）", "rs": 1, "cs": 1}]]}
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20521c9365d735810c.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20ff014a7af97a55cc.png)

## 1-9 多表查询

### 1-9-1 多表关系

项目开发中，在进行数据库表结构设计时，会根据业务需求及业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，基本上分为三种：

- 一对多（多对一）

案例：部门与员工的关系。  
关系：一个部门对应多个员工，一个员工对应一个部门。  
实现：在多对一方建立外键，指向一对一方的主键。

- 多对多

案例：学生与课程的关系。  
关系：一个学生可以选修多门课程，一门课程也可以供多个学生选择。  
实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键。

- 一对一

案例：用户与用户详情的关系。  
关系：一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中，以提升操作效率。  
实现：在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的（UNIQUE）。

### 1-9-2 多表查询概述

1. 概述：指从多张表中查询数据。
2. 笛卡尔积：笛卡尔乘积是指在数学中，两个集合 A 集合和 B 集合的所有组合情况。（在多表查询时，需要消除无效的笛卡尔积）
3. 多表查询分类：

- 连接查询

内连接：相当于查询 A、B 交集部分数据。  
自连接：当前表与自身的连接查询，自连接必须使用表别名。  
外连接：  
左外连接：查询左表所有数据，以及两张表交集部分数据。  
右外连接：查询右表所有数据，以及两张表交集部分数据。

- 子查询

### 1-9-3 连接查询 - 内连接

```sql
-- 隐式内连接
SELECT 字段列表 FROM 表1, 表2 WHERE 条件;

-- 显式内连接
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2073340190adcb8d5a.png)

### 1-9-4 连接查询 - 外连接

```sql
-- 左外连接
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 连接条件;

-- 右外连接
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 连接条件;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%200df1001919a93c77.png)

### 1-9-5 连接查询 - 自连接

```sql
SELECT 字段列表 FROM 表A 别名1 JOIN 表A 别名2 ON 连接条件;
```

> 注意：自连接必须为表起别名，否则无法区分"自身"的两个角色。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20e73ad79ef30565ac.png)

### 1-9-6 联合查询 - union, union all

对于 union 查询，就是把多次查询的结果合并起来，形成一个新的查询结果集。

```sql
SELECT 字段列表 FROM 表A
UNION [ALL]
SELECT 字段列表 FROM 表B;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%20044228c5a30a8068.png)

> 注意：  
> 1. 对于联合查询，多张表的列数必须保持一致，字段类型也需要保持一致。  
> 2. union all 会将全部的数据直接合并在一起，union 会对合并之后的数据去重。  

### 1-9-7 子查询

1. 概念：SQL 语句中嵌套 SELECT 语句，称为嵌套查询，又称子查询。子查询外的语句可以是 INSERT/UPDATE/DELETE/SELECT 的任何一个。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2045022b8160ec3cb3.png)

2. 根据子查询结果不同，分为：

- 标量子查询（子查询结果为单个值）
- 列子查询（子查询结果为一列）
- 行子查询（子查询结果为一行）
- 表子查询（子查询结果为多行多列）

3. 根据子查询位置，分为：WHERE 之后、FROM 之后、SELECT 之后。

#### 1-9-7-1 标量子查询

子查询返回的结果是单个值（数字、字符串、日期等），最简单的形式，这种子查询称为标量子查询。  
常用的操作符：= <> > >= < <=

#### 1-9-7-2 列子查询

子查询返回的结果是一列（可以是多行），这种子查询称为列子查询。  
常用的操作符：IN、NOT IN、ANY、SOME、ALL

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%200711b6380301091f.png)

#### 1-9-7-3 行子查询

子查询返回的结果是一行（可以是多列），这种子查询称为行子查询。  
常见的操作符：=、<>、IN、NOT IN

#### 1-9-7-4 表子查询

子查询返回的结果是多行多列，这种子查询称为表子查询。  
常用的操作符：IN

### 1-9-8 多表查询案例

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/基础%20image%2080d49b9bcffd55dc.png)

```sql
-- 1. 查询员工的姓名、年龄、职位、部门信息（隐式内连接）
SELECT e.name, e.age, e.job, d.name FROM emp e, dept d WHERE e.dept_id = d.id;

-- 2. 查询年龄小于 30 岁的员工姓名、年龄、职位、部门信息（显式内连接）
SELECT e.name, e.age, e.job, d.name FROM emp e INNER JOIN dept d ON e.dept_id = d.id WHERE e.age < 30;

-- 3. 查询拥有员工的部门 id、部门名称（去重）
SELECT DISTINCT d.id, d.name FROM emp e, dept d WHERE e.dept_id = d.id;

-- 4. 查询年龄大于 40 岁的员工及其部门信息（左外连接）
SELECT e.*, d.name FROM emp e LEFT JOIN dept d ON e.dept_id = d.id WHERE e.age > 40;

-- 5. 查询员工及其工资等级（非等值连接）
SELECT e.*, s.grade FROM emp e, salgrade s WHERE e.salary >= s.losal AND e.salary <= s.hisal;

-- 6. 查询研发部所有员工的工资等级
SELECT e.*, s.grade FROM emp e, salgrade s, dept d WHERE e.dept_id = d.id AND (e.salary BETWEEN s.losal AND s.hisal) AND d.name = '研发部';

-- 7. 查询研发部员工的平均工资
SELECT AVG(e.salary) FROM emp e, dept d WHERE e.dept_id = d.id AND d.name = '研发部';

-- 8. 查询工资比灭绝高的员工信息（标量子查询）
SELECT * FROM emp WHERE salary > (SELECT salary FROM emp WHERE name = '灭绝');

-- 9. 查询工资比平均工资高的员工信息
SELECT * FROM emp WHERE salary > (SELECT AVG(salary) FROM emp);

-- 10. 查询每个部门中比本部门平均工资高的员工信息（相关子查询）
SELECT * FROM emp e2 WHERE e2.salary < (SELECT AVG(e1.salary) FROM emp e1 WHERE e1.dept_id = e2.dept_id);

-- 11. 查询部门 id、部门名称以及部门人数（子查询）
SELECT d.id, d.name, (SELECT COUNT(*) FROM emp e WHERE e.dept_id = d.id) '人数' FROM dept d;

-- 12. 查询所有学生的选课情况（多对多三表连接）
SELECT s.name, s.no, c.name FROM student s, student_course sc, course c WHERE s.id = sc.studentid AND sc.courseid = c.id;
```


# 2 进阶

﻿---
tags:
  - 知识
类型: 计算机
领域: MySQL
来源: 黑马程序员MySQL数据库入门到精通课程
日期: 2026-10-08
关联:
---
## 2-1 存储引擎

### 2-1-1 MySQL体系结构

MySQL 整体分为四层：连接层、服务层、引擎层、存储层。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20949a9ee880805fa7.png)

- 连接层

最上层是一些客户端和连接服务，主要完成一些类似于连接处理、授权认证、及相关的安全方案。服务器也会为安全接入的每个客户端验证它所具有的操作权限。

- 服务层

第二层架构主要完成大多数的核心服务功能，如 SQL 接口，并完成缓存的查询，SQL 的分析和优化，部分内置函数的执行。所有跨存储引擎的功能也在这一层实现，如过程、函数等。

- 引擎层

存储引擎真正的负责了 MySQL 中数据的存储和提取，服务器通过 API 和存储引擎进行通信。不同的存储引擎具有不同的功能，这样我们可以根据自己的需求，来选取合适的存储引擎。

- 存储层

主要是将数据存储在文件系统之上，并完成与存储引擎的交互。

### 2-1-2 存储引擎简介

存储引擎就是存储数据、建立索引、更新/查询数据等技术的实现方式。存储引擎是基于表的，而不是基于库的，所以存储引擎也可被称为表类型。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20bd0e878ca64b5cac.png)

### 2-1-3 存储引擎特点

#### 2-1-3-1 InnoDB

介绍：InnoDB 是一种兼顾高可靠性和高性能的通用存储引擎，在 MySQL 5.5 之后，InnoDB 是默认的 MySQL 存储引擎。

特性：

- DML 操作遵循 ACID 模型，支持事务。
- 行级锁，提高并发访问性能。
- 支持外键 FOREIGN KEY 约束，保证数据的完整性和正确性。

文件：xxx.ibd，xxx 代表的是表名，InnoDB 引擎的每张表都会对应一个表空间文件，存储该表的表结构（frm、sdi）、数据和索引。参数：innodb_file_per_table

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2078f84d08867f8263.png)

#### 2-1-3-2 MyISAM

介绍：MyISAM 是 MySQL 早期的默认存储引擎。

特点：

- 不支持事务，不支持外键。
- 支持表锁，不支持行锁。
- 访问速度快。

文件：

- xxx.sdi：存储表结构信息。
- xxx.MYD：存储数据。
- xxx.MYI：存储索引。

#### 2-1-3-3 Memory

介绍：Memory 引擎的表数据是存储在内存中的，由于受到硬件问题、或断电问题的影响，只能将这些表作为临时表缓存使用。

特点：

- 内存存放。
- hash 索引（默认）。

文件：xxx.sdi：存储表结构信息。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2029a8949eb7a9c30c.png)

### 2-1-4 存储引擎选择

在选择存储引擎时，应该根据系统的特点选择合适的存储引擎。对于复杂的应用系统，还可以根据实际情况选择多种存储引擎进行组合。

- InnoDB：是 MySQL 的默认存储引擎，支持事务、外键。如果应用对事务的完整性有比较高的要求，在并发条件下要求数据的一致性，数据操作除了插入和查询之外，还包含很多的更新、删除操作，那么 InnoDB 存储引擎是比较适合的选择。
- MyISAM：如果应用是以读操作和插入操作为主，只有很少的更新和删除操作，并且对事务的完整性、并发性要求不是很高，那么选择这个存储引擎是非常适合的。
- MEMORY：将所有数据保存在内存中，访问速度快，通常用于临时表及缓存。MEMORY 的缺陷就是对表的大小有限制，太大的表无法缓存到内存中，而且无法保障数据的安全性。

## 2-2 索引

### 2-2-1 索引概述

介绍：索引（index）是帮助 MySQL 高效获取数据的数据结构（有序）。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用（指向）数据，这样就可以在这些数据结构上实现高级查找算法，这种数据结构就是索引。

优缺点：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20854a21eed896d096.png)

### 2-2-2 索引结构

MySQL 的索引是在存储引擎层实现的，不同的存储引擎有不同的结构，主要包含以下几种：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20857fbab108e8cabb.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2097d789bf421c5c5a.png)

> 注意：我们平常所说的索引，如果没有特别指名，都是指 B+ 树结构组织的索引。  

#### 2-2-2-1 二叉树

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20e7f49a1df0ab9885.png)

二叉树缺点：顺序插入时，会形成一个链表，查询性能大大降低。大数据量情况下，层级较深，检索速度慢。

#### 2-2-2-2 红黑树

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%204481907000cf370c.png)

红黑树：大数据量情况下，层级较深，检索速度慢。

#### 2-2-2-3 B-Tree（多路平衡查找树）

以一颗最大度数（max-degree）为 5（5 阶）的 b-tree 为例（每个节点最多存储 4 个 key，5 个指针）。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%203220349d9f360b32.png)

树的度数指的是一个节点的子节点个数。

#### 2-2-2-4 B+Tree

以一颗最大度数（max-degree）为 4（4 阶）的 b+tree 为例：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2033647fc895af40e7.png)

1. 所有的数据都会出现在叶子节点。
2. 叶子节点形成一个单向链表。

MySQL 索引数据结构对经典的 B+Tree 进行了优化。在原 B+Tree 的基础上，增加一个指向相邻叶子节点的链表指针，就形成了带有顺序指针的 B+Tree，提高区间访问的性能。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f2cc86026e293d4e.png)

#### 2-2-2-5 Hash

哈希索引就是采用一定的 hash 算法，将键值换算成新的 hash 值，映射到对应的槽位上，然后存储在 hash 表中。

Hash 索引特点：

1. Hash 索引只能用于对等比较（=，in），不支持范围查询（between，>，<，...）。
2. 无法利用索引完成排序操作。
3. 查询效率高，通常只需要一次检索就可以了，效率通常要高于 B+Tree 索引。

存储引擎支持：在 MySQL 中，支持 hash 索引的是 Memory 引擎，而 InnoDB 中具有自适应 hash 功能，hash 索引是存储引擎根据 B+Tree 索引在指定条件下自动构建的。

相对于 B-Tree 区别：  
如果两个（或多个）键值，映射到一个相同的槽位上，他们就产生了 hash 冲突（也称为 hash 碰撞），可以通过链表来解决。

为什么 InnoDB 存储引擎选择使用 B+tree 索引结构？

- 相对于二叉树，层级更少，搜索效率高。
- 对于 B-tree，无论是叶子节点还是非叶子节点，都会保存数据，这样导致一页中存储的键值减少，指针跟着减少，要同样保存大量数据，只能增加树的高度，导致性能降低。
- 相对 Hash 索引，B+tree 支持范围匹配及排序操作。

### 2-2-3 索引分类

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20800edd22305afc27.png)

InnoDB 存储引擎中，根据索引的存储形式，又可以分为以下两种：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b8b8bbb9a62fc9c7.png)

聚集索引选取规则：

- 如果存在主键，主键索引就是聚集索引。
- 如果不存在主键，将使用第一个唯一（UNIQUE）索引作为聚集索引。
- 如果表没有主键，或没有合适的唯一索引，则 InnoDB 会自动生成一个 rowid 作为隐藏的聚集索引。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%203b4a2cf1f3d89c1b.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2070e5e715bfb6c123.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f82da93d8352ccb3.png)

### 2-2-4 索引语法

创建索引、查看索引、删除索引的语法如下：

```sql
-- 创建索引
CREATE [UNIQUE] INDEX 索引名 ON 表名(字段名1, 字段名2, ...);

-- 查看索引
SHOW INDEX FROM 表名;

-- 删除索引
DROP INDEX 索引名 ON 表名;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%201e4fb1fbc13c7dfb.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20501116352cec6560.png)

示例：

```sql
SHOW INDEX FROM tb_user;
SHOW INDEX FROM tb_user\G

CREATE INDEX idx_user_name ON tb_user(name);
CREATE UNIQUE INDEX idx_user_phone ON tb_user(phone);
CREATE INDEX idx_user_pro_age_sta ON tb_user(profession, age, status);
CREATE INDEX idx_user_email ON tb_user(email);

DROP INDEX idx_user_email ON tb_user;
```## 2.5 SQL性能分析

#### 2-2-5-1 SQL执行频率

MySQL 客户端连接成功后，通过 SHOW [SESSION | GLOBAL] STATUS 命令可以提供服务器状态信息。通过如下指令，可以查看当前数据库的 INSERT、UPDATE、DELETE、SELECT 的访问频次：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%205ff6fd7151bb5b5d.png)

#### 2-2-5-2 慢查询日志

慢查询日志记录了所有执行时间超过指定参数（Long_query_time，单位：秒，默认 10 秒）的所有 SQL 语句的日志。  
MySQL 的慢查询日志默认没有开启，需要在 MySQL 的配置文件（/etc/my.cnf）中配置如下信息：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%205e282ff46e3612cd.png)

配置完毕之后，通过以下指令重新启动 MySQL 服务器进行测试，查看慢日志文件中记录的信息 /var/lib/mysql/localhost-slow.log。

```sql
SHOW VARIABLES LIKE 'slow_query_log';
```

#### 2-2-5-3 profile详情

show profile 能够在做 SQL 优化时帮助我们了解时间都消耗到哪里去了。通过 have_profiling 参数，能够看到当前 MySQL 是否支持 profile 操作：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207ce489187ae3dcd3.png)

默认 profiling 是关闭的，可以通过 set 语句在 session/global 级别开启 profiling：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200f7a26b29e5f8623.png)

执行一系列的业务 SQL 的操作，然后通过如下指令查看指令的执行耗时：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2060de57d8f62359c8.png)

#### 2-2-5-4 explain执行计划

EXPLAIN 或者 DESC 命令获取 MySQL 如何执行 SELECT 语句的信息，包括在 SELECT 语句执行过程中表如何连接和连接的顺序。  
语法：

```sql
EXPLAIN SELECT 字段列表 FROM 表名 WHERE 条件;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20a8c35f47322e24e2.png)

EXPLAIN 执行计划各字段含义：

- Id

select 查询的序列号，表示查询中执行 select 子句或者是操作表的顺序（id 相同，执行顺序从上到下；id 不同，值越大，越先执行）。

- select_type

表示 SELECT 的类型，常见的取值有 SIMPLE（简单表，即不使用表连接或者子查询）、PRIMARY（主查询，即外层的查询）、UNION（UNION 中的第二个或者后面的查询语句）、SUBQUERY（SELECT/WHERE 之后包含了子查询）等。

- type

表示连接类型，性能由好到差的连接类型为 NULL、system、const、eq_ref、range、index、all。

- possible_key

显示可能应用在这张表上的索引，一个或多个。

- Key

实际使用的索引，如果为 NULL，则没有使用索引。

- Key_len

表示索引中使用的字节数，该值为索引字段最大可能长度，并非实际使用长度，在不损失精确性的前提下，长度越短越好。

- filtered

表示返回结果的行数占需读取行数的百分比，filtered 的值越大越好。

### 2-2-6 索引使用

#### 2-2-6-1 验证索引效率

在未建立索引之前，执行如下 SQL 语句，查看 SQL 的耗时。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f4ec4ee77b0dab42.png)

针对字段创建索引。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20cd6fb2d9a8766ceb.png)

然后再次执行相同的 SQL 语句，再次查看 SQL 的耗时。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200045336eaef80cb2.png)

#### 2-2-6-2 最左前缀法则

如果索引了多列（联合索引），要遵守最左前缀法则。最左前缀法则指的是查询从索引的最左列开始，并且不跳过索引中的列。如果跳跃某一列，索引将部分失效（后面的字段索引失效）。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20d1305d8651885169.png)

#### 2-2-6-3 范围查询

联合索引中，出现范围查询（>，<），范围查询右侧的列索引失效。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%206303493f9baf9ea3.png)

#### 2-2-6-4 索引列运算

不要在索引列上进行运算操作，索引将失效。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20ba944683983f4474.png)

#### 2-2-6-5 字符串不加引号

字符串类型字段使用时，不加引号，索引将失效。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b16831b3cf1fca40.png)

#### 2-2-6-6 模糊查询

如果仅仅是尾部模糊匹配，索引不会失效。如果是头部模糊匹配，索引失效。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%204ae308280df88a3d.png)

#### 2-2-6-7 or连接的条件

用 or 分割开的条件，如果 or 前的条件中的列有索引，而后面的列中没有索引，那么涉及的索引都不会被用到。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200a7274a27df79d1a.png)

由于 age 没有索引，所以即使 id、phone 有索引，索引也会失效。所以需要针对于 age 也要创建索引。

#### 2-2-6-8 数据分布影响

如果 MySQL 评估使用索引比全表更慢，则不使用索引。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207e05708a1021cd59.png)

#### 2-2-6-9 SQL提示

SQL 提示，是优化数据库的一个重要手段，简单来说，就是在 SQL 语句中加入一些人为的提示来达到优化操作的目的。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%202d0d77416d1aab14.png)

#### 2-2-6-10 覆盖索引

尽量使用覆盖索引（查询使用了索引，并且需要返回的列，在该索引中已经全部能够找到），减少 select *。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20e23b8638bcd36452.png)

> 注意：  
> 1. using index condition：查询使用了索引，但是需要回表查询数据。  
> 2. using where; using index：查找使用了索引，但是需要的数据都在索引列中能找到，所以不需要回表查询数据。  

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20e165f81549591ba1.png)

对 username 和 password 建立联合索引。

#### 2-2-6-11 前缀索引

语法：

```sql
CREATE INDEX 索引名 ON 表名(字段名(n));
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20c6ab4bac0d847b19.png)

前缀长度：可以根据索引的选择性来决定，而选择性是指不重复的索引值（基数）和数据表的记录总数的比值，索引选择性越高则查询效率越高，唯一索引的选择性是 1，这是最好的索引选择性，性能也是最好的。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2093ae2a940502065a.png)

前缀索引查询流程：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20e2f8c68207c2f7f3.png)

#### 2-2-6-12 单列索引与联合索引

单列索引：即一个索引只包含单个列。  
联合索引：即一个索引包含了多个列。  
在业务场景中，如果存在多个查询条件，查询针对于查询字段建立索引时，建议建立联合索引，而非单列索引。

单列索引情况：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2092e5e854cac4dd1b.png)

> 注意：多条件联合查询时，MySQL 优化器会评估哪个字段的索引效率更高，会选择该索引完成本次查询。  

联合索引情况：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2083b31bbacabf195e.png)

当字段类型为字符串（varchar，text 等）时，有时候需要索引很长的字符串，这会让索引变得很大，查询时，浪费大量的磁盘 IO，影响查询效率。此时可以只将字符串的一部分前缀，建立索引，这样可以大大节约索引空间，从而提高索引效率。

### 2-2-7 索引设计原则

1. 针对于数据量较大，且查询比较频繁的表建立索引。
2. 针对于常作为查询条件（where）、排序（order by）、分组（group by）操作的字段建立索引。
3. 尽量选择区分度高的列作为索引，尽量建立唯一索引，区分度越高，使用索引的效率越高。
4. 如果是字符串类型的字段，字段的长度较长，可以针对于字段的特点，建立前缀索引。
5. 尽量使用联合索引，减少单列索引，查询时，联合索引很多时候可以覆盖索引，节省存储空间，避免回表，提高查询效率。
6. 要控制索引的数量，索引并不是多多益善，索引越多，维护索引结构的代价也会越大，会影响增删改的效率。
7. 如果索引列不能存储 NULL 值，请在创建表时使用 NOT NULL 约束它。当优化器知道每列是否包含 NULL 值时，它可以更好地确定哪个索引最有效地用于查询。# 3 SQL优化

### 2-3-1 插入数据

#### 2-3-1-1 insert优化

- 批量插入

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20d5731fd4479a81e6.png)

- 手动提交事务

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20ba0c396247a57167.png)

- 主键顺序插入

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20c1045bddb01bb01a.png)

#### 2-3-1-2 大批量插入数据

如果一次性需要插入大批量数据，使用 insert 语句插入性能较低，此时可以使用 MySQL 数据库提供的 load 指令进行插入。操作如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20deb0157a125ecb98.png)

> 注意：主键顺序插入性能高于乱序插入。  

### 2-3-2 主键优化

- 数据组织方式

在 InnoDB 存储引擎中，表结构都是根据主键顺序组织存放的，这种存储方式的表称为索引组织表（index organized table IOT）。

- 页分裂

页可以为空，也可以填充一半，也可以填充 100%。每个页包含了 2-N 行数据（如果一行数据过大，会行溢出），根据主键排列。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207fe5a4d62aae5df8.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%201d019bcffabeac61.png)

- 页合并

当删除一行记录时，实际上记录并没有被物理删除，只是记录被标记（flagged）为删除并且它的空间变得允许被其他记录声明使用。  
当页中删除的记录达到 MERGE_THRESHOLD（默认为页的 50%），InnoDB 会开始寻找最靠近的页（前或后）看看是否可以将两个页合并以优化空间使用。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2085bfba213579c8f4.png)

> 注意：MERGE_THRESHOLD 是合并页的阈值，可以自己设置，在创建表或者创建索引时指定。  

- 主键设计原则

1. 满足业务需求的情况下，尽量降低主键的长度。
2. 插入数据时，尽量选择顺序插入，选择使用 AUTO_INCREMENT 自增主键。
3. 尽量不要使用 UUID 做主键或者是其他自然主键，如身份证号。

### 2-3-3 order by优化

1. Using filesort：通过表的索引或全表扫描，读取满足条件的数据行，然后再排序缓冲区 sort buffer 中完成排序操作，所有不是通过索引直接返回排序结果的排序都叫 Filesort 排序。
2. Using index：通过有序索引顺序扫描直接返回有序数据，这种情况即为 using index，不需要额外排序，操作效率高。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20bb202ffb099ac61a.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20156feb8364ce19a7.png)

优化原则：

1. 根据排序字段建立合适的索引，多字段排序时，也遵循最左前缀法则。
2. 尽量使用覆盖索引。
3. 多字段排序，一个升序一个降序，此时需要注意联合索引在创建时的规则（ASC/DESC）。
4. 如果不可避免的出现 filesort，大数据量排序时，可以适当增大排序缓冲区大小 sort_buffer_size（默认 256k）。

### 2-3-4 group by优化

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20aa2e365c179de346.png)

- 在分组操作时，可以通过索引来提高效率。
- 分组操作时，索引的使用也是满足最左前缀法则的。

### 2-3-5 limit优化

一个常见又非常头疼的问题就是 limit 2000000, 10，此时需要 MySQL 排序前 2000010 记录，仅仅返回 2000000 - 2000010 的记录，其他记录丢弃，查询排序的代价非常大。

优化思路：一般分页查询时，通过创建覆盖索引能够比较好地提高性能，可以通过覆盖索引加子查询形式进行优化。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20decc7988016e25ca.png)

### 2-3-6 count优化

- MyISAM 引擎把一个表的总行数存在了磁盘上，因此执行 count(*) 的时候会直接返回这个数，效率高。
- InnoDB 引擎就麻烦了，它执行 count(*) 的时候，需要把数据一行一行地从引擎里面读出来，然后累计计数。

优化思路：自己计数。

count 的几种用法：

1. count() 是一个聚合函数，对于返回的结果集，一行行地判断，如果 count 函数的参数不是 NULL，累计值就加 1，否则不加，最后返回累计值。
2. 用法：count(*)、count(主键)、count(字段)、count(1)。

- count(主键)

InnoDB 引擎会遍历整张表，把每一行的主键 id 值都取出来，返回给服务层。服务层拿到主键后，直接按行进行累加（主键不能为 null）。

- count(字段)

没有 not null 约束：InnoDB 引擎会遍历整张表把每一行的字段值都取出来，返回给服务层，服务层判断是否为 null，不为 null，计数累加。  
有 not null 约束：InnoDB 引擎会遍历整张表把每一行的字段值都取出来，返回给服务层，直接按行进行累加。

- count(1)

InnoDB 引擎遍历整张表，但不取值。服务层对于返回的每一行，放一个数字"1"进去，直接按行进行累加。

- count(*)

InnoDB 引擎并不会把全部字段取出来，而是专门做了优化，不取值，服务层直接按行进行累加。

> 注意：按照效率排序的话，count(字段) < count(主键 id) < count(1) = count(*)，所以尽量使用 count(*)。  

### 2-3-7 update优化

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2034cef5915b4b73e7.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20605c11a672394e93.png)

> 注意：InnoDB 的行锁是针对索引加的锁，不是针对记录加的锁，并且该索引不能失效，否则会行锁升级为表锁。  # 4 视图/存储过程/触发器

### 2-4-1 视图

#### 2-4-1-1 介绍

视图（view）是一种虚拟存在的表。视图中的数据并不在数据库中实际存在，行和列数据来自定义视图的查询中使用的表，并且是在使用视图时动态生成的。  
通俗的讲，视图只保存了查询的 SQL 逻辑，不保存查询结果。所以我们在创建视图的时候，主要的工作就落在创建这条 SQL 查询语句中。

#### 2-4-1-2 语法

创建：

```sql
CREATE [OR REPLACE] VIEW 视图名称 AS SELECT 语句;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20ee4cf6ed75d44abc.png)

查询：

```sql
SHOW CREATE VIEW 视图名称;
SELECT * FROM 视图名称;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20fde9a3992ed503ee.png)

修改：

```sql
CREATE OR REPLACE VIEW 视图名称 AS SELECT 语句;
ALTER VIEW 视图名称 AS SELECT 语句;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2012e843a15a2e6da7.png)

删除：

```sql
DROP VIEW [IF EXISTS] 视图名称;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2008db0ea2c27448e1.png)

示例：

```sql
CREATE VIEW tb_user_view AS SELECT id, name, profession, age, gender, status, createtime FROM tb_user;

CREATE VIEW tb_stu_course_view AS SELECT s.name student_name, s.no student_no, c.name course_name FROM student s, student_course sc, course c WHERE s.id = sc.studentid AND sc.courseid = c.id;
```

#### 2-4-1-3 视图的检查选项

当使用 WITH CHECK OPTION 子句创建视图时，MySQL 会通过视图检查正在更改的每个行，例如插入、更新、删除，以使其符合视图的定义。MySQL 允许基于另一个视图创建视图，它还会检查依赖视图中的规则以保持一致性。为了确保检查的范围，mysql 提供了两个选项：CASCADED 和 LOCAL，默认值 CASCADED。  
CASCADED 需要全部满足。  
LOCAL 只需要当前满足。

```sql
CREATE VIEW 视图名称 AS SELECT 语句 WITH [CASCADED | LOCAL] CHECK OPTION;
```

#### 2-4-1-4 视图的更新

要使视图可更新，视图中的行与基础表中的行之间必须存在一对一的关系。如果视图包括以下任何一项，则该视图不可更新：

1. 聚合函数或窗口函数（SUM()、MIN()、MAX()、COUNT() 等）。
2. DISTINCT
3. GROUP BY
4. HAVING
5. UNION 或者 UNION ALL

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%203605030be02d07c6.png)

#### 2-4-1-5 作用

- 简单

视图不仅可以简化用户对数据的理解，也可以简化他们的操作。那些被经常使用的查询可以被定义为视图，从而使得用户不必为以后的操作每次指定全部的条件。

- 安全

数据库可以授权，但不能授权到数据库特定行和特定的列上。通过视图用户只能查询和修改他们所能见到的数据。

- 数据独立

视图可帮助用户屏蔽真实表结构变化带来的影响。

### 2-4-2 存储过程

#### 2-4-2-1 介绍

存储过程是事先经过编译并存储在数据库中的一段 SQL 语句的集合，调用存储过程可以简化应用开发人员的很多工作，减少数据库和应用服务器之间的传输，对于提高数据处理的效率是有好处的。  
存储过程思想上很简单，就是数据库 SQL 语言层面的代码封装与重用。

特点：

- 封装，复用。
- 可以接受参数，也可以返回数据。
- 减少网络交互，效率提升。

#### 2-4-2-2 语法

创建：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20ddd3d27fe5607660.png)

调用：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b9298168dc2013cf.png)

查看：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20fe78a32c3d9c69ad.png)

删除：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b012d31e78933ee9.png)

> 注意：在命令行，执行创建存储过程的 SQL 时，需要通过关键字 delimiter 指定 SQL 语句的结束符。  

#### 2-4-2-3 变量

系统变量：是 MySQL 服务器提供，不是用户定义的，属于服务器层面。分为全局变量（GLOBAL）、会话变量（SESSION）。

查看系统变量：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b721969f7a766b58.png)

设置系统变量：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2012789e7c14f62b60.png)

> 注意：  
> 1. 如果没有指定 SESSION/GLOBAL，默认是 SESSION，会话变量。  
> 2. mysql 服务重新启动之后，所设置的全局参数会失效，要想不失效，可以在 /etc/my.cnf 中配置。  

用户定义变量：是用户根据需要自己定义的变量，用户变量不用提前声明，在用的时候直接用"@变量名"使用就可以。其作用域为当前连接。

赋值：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20040fc30187da1b80.png)

使用：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2068fcb9d2e8ba3509.png)

> 注意：用户定义的变量无需对其进行声明或初始化，只不过获取到的值为 NULL。  

局部变量：是根据需要定义的在局部生效的变量，访问之前，需要 DECLARE 声明。可用作存储过程内的局部变量和输入参数，局部变量的范围是在其内声明的 BEGIN...END 块。

声明：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20cda8439c52f34e1e.png)

变量类型就是数据库字段类型：INT、BIGINT、CHAR、VARCHAR、DATE、TIME 等。

赋值：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2025806bf302a74865.png)

#### 2-4-2-4 流程控制

if 语法：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2041d9881456d3a5cb.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200d8192c15d067a41.png)

示例：

```sql
CREATE PROCEDURE p()
BEGIN
    DECLARE score INT DEFAULT 58;
    DECLARE result VARCHAR(10);
    IF score >= 85 THEN
        SET result := '优秀';
    ELSEIF score >= 60 THEN
        SET result := '及格';
    ELSE
        SET result := '不及格';
    END IF;
    SELECT result;
END;
CALL p();
```

参数：存储过程的参数有三种类型：IN（输入参数）、OUT（输出参数）、INOUT（输入输出参数）。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200b4e27b294b5a1f3.png)

用法：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20ccebeed1681d6717.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b99af03d578357eb.png)

示例：

```sql
CREATE PROCEDURE p(IN score INT, OUT result VARCHAR(10))
BEGIN
    IF score >= 85 THEN
        SET result := '优秀';
    ELSEIF score >= 60 THEN
        SET result := '及格';
    ELSE
        SET result := '不及格';
    END IF;
END;
CALL p(68, @result);
SELECT @result;
```

```sql
CREATE PROCEDURE p(INOUT score DOUBLE)
BEGIN
    SET score := score * 0.5;
END;
SET @score := 78;
CALL p(@score);
SELECT @score;
```

case 语法：

语法一：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%204ea71d43b6799dcf.png)

语法二：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207cd2c54a69e23a1e.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f9d66cb615395b4f.png)

示例：

```sql
CREATE PROCEDURE p(IN month INT)
BEGIN
    DECLARE result VARCHAR(10);
    CASE
        WHEN month >= 1 AND month <= 3 THEN
            SET result := '第一季度';
        WHEN month >= 4 AND month <= 6 THEN
            SET result := '第二季度';
        WHEN month >= 7 AND month <= 9 THEN
            SET result := '第三季度';
        WHEN month >= 10 AND month <= 12 THEN
            SET result := '第四季度';
        ELSE
            SET result := '非法参数';
    END CASE;
    SELECT CONCAT("您输入的月份为：", month, '，所属的季度为：', result);
END;
CALL p(4);
```

while：while 循环是有条件的循环控制语句。满足条件后，再执行循环体中的 SQL 语句。具体语法为：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%206e0c93f093fa6576.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207ba757f28090a17b.png)

示例：

```sql
CREATE PROCEDURE p(IN n INT)
BEGIN
    DECLARE total INT DEFAULT 0;
    WHILE n > 0 DO
        SET total := total + n;
        SET n := n - 1;
    END WHILE;
    SELECT total;
END;
CALL p(10);
```

repeat：repeat 是有条件的循环控制语句，当满足条件的时候退出循环。具体语法为：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20a4d4b296dcdf08cd.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2050714695501d9981.png)

示例：

```sql
CREATE PROCEDURE p(IN n INT)
BEGIN
    DECLARE total INT DEFAULT 0;
    REPEAT
        SET total := total + n;
        SET n := n - 1;
    UNTIL n <= 0
    END REPEAT;
    SELECT total;
END;
CALL p(10);
```

loop：LOOP 实现简单的循环，如果不在 SQL 逻辑中增加退出循环的条件，可以用其来实现简单的死循环。LOOP 可以配合以下两个语句使用：

- LEAVE：配合循环使用，退出循环。
- ITERATE：必须用在循环中，作用是跳过当前循环剩下的语句，直接进入下一个循环。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%209f5310dc02cca869.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20be6407e0fa2e69ec.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b1b33ba9e2ed0848.png)

示例（LEAVE 退出循环）：

```sql
CREATE PROCEDURE p(IN n INT)
BEGIN
    DECLARE total INT DEFAULT 0;
    sum:LOOP
        IF n <= 0 THEN
            LEAVE sum;
        END IF;
        SET total := total + n;
        SET n := n - 1;
    END LOOP sum;
    SELECT total;
END;
CALL p(10);
```

示例（ITERATE 跳过循环）：

```sql
CREATE PROCEDURE p(IN n INT)
BEGIN
    DECLARE total INT DEFAULT 0;
    sum:LOOP
        IF n <= 0 THEN
            LEAVE sum;
        END IF;
        IF n % 2 = 1 THEN
            SET n := n - 1;
            ITERATE sum;
        END IF;
        SET total := total + n;
        SET n := n - 1;
    END LOOP sum;
    SELECT total;
END;
CALL p(10);
```

#### 2-4-2-5 游标

游标（CURSOR）是用来存储查询结果集的数据类型，在存储过程和函数中可以使用游标对结果集进行循环的处理。游标的使用包括游标的声明、OPEN、FETCH 和 CLOSE，其语法分别如下。

声明游标：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207512df67617e86d9.png)

打开游标：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20efcb1444c073e8e5.png)

获取游标记录：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2013c5fdb8f554dabb.png)

关闭游标：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20030f1e6438d4eb25.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%201afc968d596432c7.png)

示例：

```sql
CREATE PROCEDURE p(IN uage INT)
BEGIN
    DECLARE uname VARCHAR(100);
    DECLARE upro VARCHAR(100);
    DECLARE u_cursor CURSOR FOR SELECT name, profession FROM tb_user WHERE age <= uage;
    DECLARE exit HANDLER FOR SQLSTATE '02000' CLOSE u_cursor;

    DROP TABLE IF EXISTS tb_user_pro;
    CREATE TABLE IF NOT EXISTS tb_user_pro(
        id INT PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(100),
        profession VARCHAR(100)
    );

    OPEN u_cursor;
    WHILE TRUE DO
        FETCH u_cursor INTO uname, upro;
        INSERT INTO tb_user_pro VALUES (NULL, uname, upro);
    END WHILE;
    CLOSE u_cursor;
END;
```

#### 2-4-2-6 条件处理程序

条件处理程序（Handler）可以用来定义在流程控制结构执行中遇到问题时相应的处理步骤。具体语法为：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20c70bf6aec7960a49.png)

### 2-4-3 存储函数

存储函数是有返回值的存储过程，存储函数的参数只能是 IN 类型。具体语法如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f33dc2499f5d828b.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20003cca8b1e101989.png)

示例：

```sql
CREATE FUNCTION fun(n INT)
RETURNS INT DETERMINISTIC
BEGIN
    DECLARE total INT DEFAULT 0;

    WHILE n > 0 DO
        SET total := total + n;
        SET n := n - 1;
    END WHILE;

    RETURN total;
END;
```

### 2-4-4 触发器

介绍：触发器是与表有关的数据库对象，指在 insert/update/delete 之前或之后，触发并执行触发器中定义的 SQL 语句集合。触发器的这种特性可以协助应用在数据库端确保数据的完整性，日志记录，数据校验等操作。  
使用别名 OLD 和 NEW 来引用触发器中发生变化的记录内容，这与其他的数据库是相似的。现在触发器还只支持行级触发，不支持语句级触发。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f5d9a0214f0ed348.png)

语法：

创建：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%208389bd0922e47a8b.png)

查看：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f9904f546a6de94c.png)

删除：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%205c9e5f5f72150a2d.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20a7fc6337b589f01f.png)

示例：

```sql
CREATE TRIGGER tb_user_insert_trigger
AFTER INSERT ON tb_user FOR EACH ROW
BEGIN
    INSERT INTO user_logs(id, operation, operate_time, operate_id, operate_params) VALUES
    (NULL, 'insert', NOW(), new.id, CONCAT('插入的数据内容为：id = ', new.id, 'name = ', new.name, 'phone = ', new.phone, 'email = ', new.email, 'profession = ', new.profession));
END;
```# 5 锁

### 2-5-1 概述

介绍：锁是计算机协调多个进程或线程并发访问某一资源的机制。在数据库中，除传统的计算资源（CPU、RAM、I/O）的争用以外，数据也是一种供许多用户共享的资源。如何保证数据并发访问的一致性、有效性是所有数据库必须解决的一个问题，锁冲突是影响数据库并发访问性能的一个重要因素。从这个角度来说，锁对数据库而言显得尤其重要，也更加复杂。

MySQL 中的锁，按照锁的粒度分，分为以下三类：

1. 全局锁：锁定数据库中的所有表。
2. 表级锁：每次操作锁住整张表。
3. 行级锁：每次操作锁住对应的行数据。

### 2-5-2 全局锁

介绍：全局锁就是对整个数据库实例加锁，加锁后整个实例就处于只读状态，后续的 DML 的写语句，DDL 语句，以及更新操作的事务提交语句都将被阻塞。  
其典型的使用场景是做全库的逻辑备份，对所有的表进行锁定，从而获取一致性视图，保证数据的完整性。

演示：

加锁：

```sql
FLUSH TABLES WITH READ LOCK;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%209b5d9b94c532e776.png)

备份：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%201ef2e49a763985d8.png)

解锁：

```sql
UNLOCK TABLES;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20d6b25ff35ec6d5c2.png)

特点：数据库中加全局锁，是一个比较重的操作，存在以下问题：

1. 如果在主库上备份，那么在备份期间都不能执行更新，业务基本上就得停摆。
2. 如果在从库上备份，那么在备份期间从库不能执行主库同步过来的二进制日志（binlog），会导致主从延迟。

在 InnoDB 引擎中，我们可以在备份时加上参数 --single-transaction 参数来完成不加锁的一致性数据备份。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f8037c9fc5c1ac32.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%208136b8ef8a13f7c0.png)

### 2-5-3 表级锁

介绍：表级锁，每次操作锁住整张表。锁定粒度大，发生锁冲突的概率最高，并发度最低。应用在 MyISAM、InnoDB、BDB 等存储引擎中。

对于表级锁，主要分为以下三类：

1. 表锁。
2. 元数据锁（meta data lock，MDL）。
3. 意向锁。

#### 2-5-3-1 表锁

对于表锁，分为两类：

1. 表共享读锁（read lock）
2. 表独占写锁（write lock）

语法：

```sql
LOCK TABLES 表名 READ / WRITE;
UNLOCK TABLES;
```

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207457a497507f0656.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%209bcabbfb8fb3a00e.png)

> 注意：读锁不会阻塞其他客户端的读，但是会阻塞写。写锁既会阻塞其他客户端的读，又会阻塞其他客户端的写。  

#### 2-5-3-2 元数据锁

MDL 加锁过程是系统自动控制，无需显式使用，在访问一张表的时候会自动加上。MDL 锁主要作用是维护表元数据的数据一致性，在表上有活动事务的时候，不可以对元数据进行写入操作。为了避免 DML 与 DDL 冲突，保证读写的正确性。

在 MySQL 5.5 中引入了 MDL，当对一张表进行增删改查的时候，加 MDL 读锁（共享）；当对表结构进行变更操作的时候，加 MDL 写锁（排他）。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20476156dd0d7b29d0.png)

查看元数据锁：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20a2f22021c0434ff0.png)

#### 2-5-3-3 意向锁

为了避免 DML 在执行时，加的行锁与表锁的冲突，在 InnoDB 中引入了意向锁，使得表锁不用检查每行数据是否加锁，使用意向锁来减少表锁的检查。

1. 意向共享锁（IS）：由语句 select ... lock in share mode 添加。与表锁共享锁（read）兼容，与表锁排他锁（write）互斥。
2. 意向排他锁（IX）：由 insert、update、delete、select ... for update 添加。与表锁共享锁（read）及排他锁（write）都互斥。意向锁之间不会互斥。

可以通过以下 SQL，查看意向锁及行锁的加锁情况：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2073f8fe58c55cb979.png)

### 2-5-4 行级锁

介绍：行级锁，每次操作锁住对应的行数据。锁定粒度最小，发生锁冲突的概率最低，并发度最高。应用在 InnoDB 存储引擎中。

InnoDB 的数据是基于索引组织的，行锁是通过对索引上的索引项加锁来实现的，而不是对记录加的锁。对于行级锁，主要分为以下三类：

1. 行锁（Record Lock）：锁定单个行记录的锁，防止其他事务对此行进行 update 和 delete。在 RC、RR 隔离级别下都支持。
2. 间隙锁（Gap Lock）：锁定索引记录间隙（不含该记录），确保索引记录间隙不变，防止其他事务在这个间隙进行 insert，产生幻读。在 RR 隔离级别下支持。
3. 临键锁（Next-Key Lock）：行锁和间隙锁组合，同时锁住数据，并锁住数据前面的间隙 Gap。在 RR 隔离级别下支持。

#### 2-5-4-1 行锁

InnoDB 实现了以下两种类型的行锁：

1. 共享锁（S）：允许一个事务去读一行，阻止其他事务获得相同数据集的排他锁。
2. 排他锁（X）：允许获取排他锁的事务更新数据，阻止其他事务获得相同数据集的共享锁和排他锁。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2021aad34c07607637.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20e439da3e24092831.png)

演示：

1. 针对唯一索引进行检索时，对已存在的记录进行等值匹配，将会自动优化为行锁。
2. InnoDB 的行锁是针对索引加的锁，不通过索引条件检索数据，那么 InnoDB 将对表中的所有记录加锁，此时将会升级为表锁。

可以通过以下 SQL，查看意向锁及行锁的加锁情况：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2081e0567c5962b7af.png)

#### 2-5-4-2 间隙锁/临键锁

演示：

1. 索引上的等值查询（唯一索引），给不存在的记录加锁时，优化为间隙锁。
2. 索引上的等值查询（普通索引），向右遍历时最后一个值不满足查询需求时，next-key lock 退化为间隙锁。
3. 索引上的范围查询（唯一索引）--会访问到不满足条件的第一个值为止。

> 注意：间隙锁唯一目的是防止其他事务插入间隙。间隙锁可以共存，一个事务采用的间隙锁不会阻止另一个事务在同一间隙上采用的间隙锁。  

默认情况下，InnoDB 在 REPEATABLE READ 事务隔离级别运行，InnoDB 使用 next-key 锁进行搜索和索引扫描，以防止幻读。

## 2-6 InnoDB核心

### 2-6-1 逻辑存储结构

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2035188274ca8855ed.png)

InnoDB 的逻辑存储结构从大到小依次为：表空间、段、区、页、行。

- 表空间（ibd 文件）：一个 mysql 实例可以对应多个表空间，用于存储记录、索引等数据。

- 段：分为数据段（Leaf node segment）、索引段（Non-leaf node segment）、回滚段（Rollback segment），InnoDB 是索引组织表，数据段就是 B+ 树的叶子节点，索引段即为 B+ 树的非叶子节点。段用来管理多个 Extent（区）。

- 区：表空间的单元结构，每个区大小都为 1M。默认情况下，InnoDB 存储引擎页大小为 16K，即一个区中一共有 64 个连续的页。

- 页：是 InnoDB 存储引擎磁盘管理的最小单元，每个页的大小默认为 16KB。为了保证页的连续性，InnoDB 存储引擎每次从磁盘申请 4-5 个区。

- 行：InnoDB 存储引擎数据是按行进行存放的。  
Trx_id：每次对某条记录进行改动时，都会把对应的事务 id 赋值给 trx_id 隐藏列。  
Roll_pointer：每次对某条记录进行改动时，都会把旧的版本写入到 undo 日志中，然后这个隐藏列就相当于一个指针，可以通过它来找到该记录修改前的信息。

### 2-6-2 架构

MySQL 5.5 版本开始，默认使用 InnoDB 存储引擎，它擅长事务处理，具有崩溃恢复特性，在日常开发中使用非常广泛。下面是 InnoDB 架构图，左侧为内存结构，右侧为磁盘结构。

#### 2-6-2-1 内存结构

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20cfb3355b9ef46f63.png)

Buffer Pool：缓冲池是主内存中的一个区域，里面可以缓存磁盘上经常操作的真实数据，在执行增删改查操作时，先操作缓冲池中的数据（若缓冲池没有数据，则从磁盘加载并缓存），然后再以一定频率刷新到磁盘，从而减少磁盘 IO，加快处理速度。

缓冲池以 Page 页为单位，底层采用链表数据结构管理 Page。根据状态，将 Page 分为三种类型：

1. free page：空闲 page，未被使用。
2. clean page：被使用 page，数据没有被修改过。
3. dirty page：脏页，被使用 page，数据被修改过，页中数据与磁盘的数据产生了不一致。

Change Buffer：更改缓冲区（针对于非唯一二级索引页），在执行 DML 语句时，如果这些数据 Page 没有在 Buffer Pool 中，不会直接操作磁盘，而会将数据变更存在更改缓冲区 Change Buffer 中，在未来数据被读取时，再将数据合并恢复到 Buffer Pool 中，再将合并后的数据刷新到磁盘中。

Change Buffer 的意义是什么？  
与聚集索引不同，二级索引通常是非唯一的，并且以相对随机的顺序插入二级索引。同样，删除和更新可能会影响索引树中不相邻的二级索引页，如果每一次都操作磁盘，会造成大量的磁盘 IO。有了 ChangeBuffer 之后，我们可以在缓冲池中进行合并处理，减少磁盘 IO。

Adaptive Hash Index：自适应 hash 索引，用于优化对 Buffer Pool 数据的查询。InnoDB 存储引擎会监控对表上索引页的查询，如果观察到 hash 索引可以提升速度，则建立 hash 索引，称之为自适应 hash 索引。  
自适应哈希索引，无需人工干预，是系统根据情况自动完成。  
参数：adaptive_hash_index

Log Buffer：日志缓冲区，用来保存要写入到磁盘中的 log 日志数据（redo log、undo log），默认大小为 16MB，日志缓冲区的日志会定期刷新到磁盘中。如果需要更新、插入或删除许多行的事务，增加日志缓冲区的大小可以节省磁盘 I/O。  
参数：

- innodb_log_buffer_size：缓冲区大小
- innodb_flush_log_at_trx_commit：日志刷新到磁盘时机

1：日志在每次事务提交时写入并刷新到磁盘。  
0：每秒将日志写入并刷新到磁盘一次。  
2：日志在每次事务提交后写入，并每秒刷新到磁盘一次。

#### 2-6-2-2 磁盘结构

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%203e86677390db65da.png)

System Tablespace：系统表空间是更改缓冲区的存储区域。如果表是在系统表空间而不是每个表文件或通用表空间中创建的，它也可能包含表和索引数据。（在 MySQL 5.x 版本中还包含 InnoDB 数据字典、undolog 等）  
参数：innodb_data_file_path

File-Per-Table Tablespaces：每个表的文件表空间包含单个 InnoDB 表的数据和索引，并存储在文件系统上的单个数据文件中。  
参数：innodb_file_per_table

General Tablespace：通用表空间，需要通过 CREATE TABLESPACE 语法创建通用表空间，在创建表时，可以指定该表空间。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20c4c4193734b48c9f.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20f3e3f5c6a61c0f20.png)

Undo Tablespaces：撤销表空间，MySQL 实例在初始化时会自动创建两个默认的 undo 表空间（初始大小 16M），用于存储 undo log 日志。

Temporary Tablespaces：InnoDB 使用会话临时表空间和全局临时表空间。存储用户创建的临时表等数据。

Doublewrite Buffer Files：双写缓冲区，InnoDB 引擎将数据页从 Buffer Pool 刷新到磁盘前，先将数据页写入双写缓冲区文件中，便于系统异常时恢复数据。

Redo Log：重做日志，是用来实现事务的持久性。该日志文件由两部分组成：重做日志缓冲（redo log buffer）以及重做日志文件（redo log），前者在内存中，后者在磁盘中。当事务提交之后会把所有修改信息都会存到该日志中，用于在刷新脏页到磁盘时，发生错误时，进行数据恢复使用。

#### 2-6-2-3 后台线程

1. Master Thread

核心后台线程、负责调度其他线程，还负责将缓冲池中的数据异步刷新到磁盘中，保持数据的一致性，还包括脏页的刷新、合并插入缓存、undo 页的回收。

2. IO Thread

在 InnoDB 存储引擎中大量使用了 AIO 来处理 IO 请求，这样可以极大地提高数据库的性能，而 IO Thread 主要负责这些 IO 请求的回调。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20d46f6c6941672ece.png)

### 2-6-3 事务原理

- 事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。
- 特性：

1. 原子性（Atomicity）：事务是不可分割的最小操作单元，要么全部成功，要么全部失败。
2. 一致性（Consistency）：事务完成时，必须使所有的数据都保持一致状态。
3. 隔离性（Isolation）：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行。
4. 持久性（Durability）：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2051ae558581b6b5ff.png)

#### 2-6-3-1 redo log

重做日志，记录的是事务提交时数据页的物理修改，是用来实现事务的持久性。  
该日志文件由两部分组成：重做日志缓冲（redo log buffer）以及重做日志文件（redo log file），前者是在内存中，后者在磁盘中。当事务提交之后会把所有修改信息都存到该日志文件中，用于在刷新脏页到磁盘，发生错误时，进行数据恢复使用。

#### 2-6-3-2 undo log

回滚日志，用于记录数据被修改前的信息，作用包含两个：提供回滚和 MVCC（多版本并发控制）。  
undo log 和 redo log 记录的物理日志不一样，它是逻辑日志。可以认为当 delete 一条记录时，undo log 中会记录一条对应的 insert 记录，反之亦然，当 update 一条记录时，它记录一条对应相反的 update 记录。当执行 rollback 时，就可以从 undo log 中的逻辑记录读取到相应的内容并进行回滚。  
Undo log 销毁：undo log 在事务执行时产生，事务提交时，并不是立即删除 undo log，因为这些日志可能还用于 MVCC。  
Undo log 存储：undo log 采用段的方式进行管理和记录，存放在前面介绍的 rollback segment 回滚段中，内部包含 1024 个 undo log segment。

### 2-6-4 MVCC

#### 2-6-4-1 基本概念

当前读：读取的是记录的最新版本，读取时还要保证其他并发事务不能修改记录，会对读取的记录进行加锁。对于我们日常的操作，如：select ... lock in share mode（共享锁），select ... for update、update、insert、delete（排他锁）都是一种当前读。

快照读：简单的 select（不加锁）就是快照读，快照读，读取的是记录数据的可见版本，有可能是历史数据，不加锁，是非阻塞读。

- Read Committed：每次 select，都生成一个快照。
- Repeatable Read：开启事务后第一个 select 语句才是快照读的地方。
- Serializable：快照读会退化为当前读。

MVCC：全称 Multi-Version Concurrency Control，多版本并发控制。指维护一个数据的多个版本，使得读写操作没有冲突，快照读为 MySQL 实现 MVCC 提供了一个非阻塞读功能。MVCC 的具体实现，还需要依赖于数据库记录中的三个隐式字段、undo log 日志、readView。

#### 2-6-4-2 实现原理

记录中的隐藏字段：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2074d865531013c6b9.png)

undo log：回滚日志，在 insert、update、delete 的时候产生的便于数据回滚的日志。  
当 insert 的时候，产生的 undo log 日志只在回滚时需要，在事务提交后，可被立即删除。  
而 update、delete 的时候，产生的 undo log 日志不仅在回滚时需要，在快照读时也需要，不会立即被删除。

undo log 版本链：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20eba939fbbe3e0f38.png)

不同事务或相同事务对同一条记录进行修改，会导致该记录的 undo log 生成一条记录版本链表、链表的头部是最新的旧记录，链表尾部是最早的旧记录。

readview：ReadView（读视图）是快照读 SQL 执行时 MVCC 提取数据的依据，记录并维护系统当前的事务（未提交的）id。  
ReadView 中包含了四个核心字段：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200f2ca08f72f264ea.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%205badd72e96ecadf5.png)

> 注意：不同的隔离级别，生成 ReadView 的时机不同：  
> 1. READ COMMITTED：在事务中每一次执行快照读时生成 ReadView。  
> 2. REPEATABLE READ：仅在事务中第一次执行快照读时生成 ReadView，后续复用该 ReadView。  

## 2-7 MySQL管理

### 2-7-1 系统数据库

MySQL 数据库安装完成后，自带了以下四个数据库，具体作用如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20dcf18c4a1e2d8f1c.png)

### 2-7-2 常用工具

- mysql

mysql 不是指 mysql 服务，而是指 mysql 的客户端工具。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2015d9ae1dcb76a67f.png)

- mysqladmin

mysqladmin 是一个执行管理操作的客户端程序。可以用它来检查服务器的配置和当前状态、创建并删除数据库等。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%207586ee7bff50cbc4.png)

- mysqlbinlog

由于服务器生成的二进制日志文件以二进制格式保存，所以如果想要检查这些日志的文本格式，就会使用到 mysqlbinlog 日志管理工具。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%200338b0ed2844c2cc.png)

- mysqlshow

mysqlshow 客户端对象查找工具，用来很快地查找存在哪些数据库、数据库中的表、表中的列或者索引。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20be76726731790d9a.png)

- mysqldump

mysqldump 客户端工具用来备份数据库或在不同数据库之间进行数据迁移。备份内容包括创建表，及插入表的 SQL 语句。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%2037380183b0ee822a.png)

- mysqlimport/source

mysqlimport 是客户端数据导入工具，用来导入 mysqldump 加 -T 参数后导出的文本文件。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20fa40e31db2a4a1d7.png)

如果需要导入 sql 文件，可以使用 mysql 中的 source 指令：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/进阶%20image%20b0ec0222ff2bf07a.png)


# 3 运维

﻿---
tags:
  - 知识
类型: 计算机
领域: MySQL
来源: 黑马程序员MySQL数据库入门到精通课程
日期: 2026-10-08
关联:
---
## 3-1 日志

### 3-1-1 错误日志

错误日志是 MySQL 中最重要的日志之一，它记录了当 mysqld 启动和停止时，以及服务器在运行过程中发生任何严重错误时的相关信息。当数据库出现任何故障导致无法正常使用时，建议首先查看此日志。  
该日志是默认开启的，默认存放目录为 /var/log/，默认的日志文件名为 mysqld.log。查看日志位置：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20fe8ee7f159b25a28.png)

### 3-1-2 二进制日志

二进制日志（BINLOG）记录了所有的 DDL（数据定义语言）语句和 DML（数据操纵语言）语句，但不包括数据查询（SELECT、SHOW）语句。二进制日志主要有两个作用：

1. 灾难时的数据恢复。
2. MySQL 的主从复制。

在 MySQL 8 版本中，默认二进制日志是开启着的，涉及到的参数如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%2013542c4f835fd367.png)

#### 3-1-2-1 日志格式

MySQL 服务器中提供了多种格式来记录二进制日志，具体格式及特点如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20555de072935548a6.png)

#### 3-1-2-2 日志查看

由于日志是以二进制方式存储的，不能直接读取，需要通过二进制日志查询工具 mysqlbinlog 来查看，具体语法：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%209a23e8da7635da1e.png)

#### 3-1-2-3 日志删除

对于比较繁忙的业务系统，每天生成的 binlog 数据巨大，如果长时间不清理，将会占用大量磁盘空间，可以通过以下几种方式清理日志：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20fe0f8276321411b4.png)

也可以在 mysql 的配置文件中配置二进制日志的过期时间，设置了之后，二进制日志过期会自动删除。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20deb0bf353305998d.png)

### 3-1-3 查询日志

查询日志中记录了客户端的所有操作语句，而二进制日志不包含查询数据的 SQL 语句。默认情况下，查询日志是未开启的。如果需要开启查询日志，可以设置以下配置：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%208d02092793a6587c.png)

修改 MySQL 的配置文件 /etc/my.cnf 文件，添加如下内容：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%208a53ca816c9546c6.png)

### 3-1-4 慢查询日志

慢查询日志记录了所有执行时间超过参数 long_query_time 设置值并且扫描记录数不小于 min_examined_row_limit 的所有的 SQL 语句的日志，默认未开启。long_query_time 默认为 10 秒，最小为 0，精度可以到微秒。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20ad1029d3be81f63f.png)

默认情况下，不会记录管理语句，也不会记录不使用索引进行查找的查询。可以使用 log_slow_admin_statements 和 log_queries_not_using_indexes 更改此行为，如下所示。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20266e1f7acee85f94.png)

## 3-2 主从复制

### 3-2-1 概述

主从复制是指将数据库的 DDL 和 DML 操作通过二进制日志传到从库服务器中，然后再从库上对这些日志重新执行（也叫重做），从而使得从库和主库的数据保持同步。  
MySQL 支持一台主库同时向多台从库进行复制，从库同时也可以作为其他从服务器的主库，实现链状复制。

MySQL 复制的优点主要包含以下三个方面：

1. 主库出现问题，可以快速切换到从库提供服务。
2. 实现读写分离，降低主库的访问压力。
3. 可以在从库中执行备份，以避免备份期间影响主库服务。

### 3-2-2 原理（基于二进制日志）

MySQL 的主从复制原理如下。

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%200b652757b15c5be0.png)

从上图来看，复制分成三步：

1. Master 主库在事务提交时，会把数据变更记录在二进制日志文件 Binlog 中。
2. 从库读取主库的二进制日志文件 Binlog，写入到从库的中继日志 Relay Log。
3. Slave 重做中继日志中的事件，将改变反映到它自己的数据。

### 3-2-3 搭建

#### 3-2-3-1 服务器准备

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20fc3f0071e7fc6d52.png)

准备好两台服务器之后，在上述的两台服务器中分别安装好 MySQL，并且完成基础的初始化准备工作。

#### 3-2-3-2 主库配置

1. 修改配置文件 /etc/my.cnf

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%2058c523991aa8f04c.png)

2. 重启 MySQL 服务器

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20b6207cca60c9bdc7.png)

3. 登录 mysql，创建远程连接的账号，并授予主从复制权限

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20fc202fd98d86c1e4.png)

4. 通过指令，查看二进制日志坐标

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20c1eed6f082bc042c.png)

字段含义说明：

```vtable
{"rows": [[{"t": "字段", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "file", "rs": 1, "cs": 1}, {"t": "从哪个日志文件开始推送日志文件", "rs": 1, "cs": 1}], [{"t": "position", "rs": 1, "cs": 1}, {"t": "从哪个位置开始推送日志", "rs": 1, "cs": 1}], [{"t": "binlog_ignore_db", "rs": 1, "cs": 1}, {"t": "指定不需要同步的数据库", "rs": 1, "cs": 1}]]}
```

#### 3-2-3-3 从库配置

1. 修改配置文件 /etc/my.cnf

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20b7a69f7dd4855db7.png)

2. 重新启动 MySQL 服务

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20ba859572b7fd5222.png)

3. 登录 mysql，设置主库配置

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20154ee8a1eb2eb003.png)

> 注意：上述是 8.0.23 中的语法。如果 mysql 是 8.0.23 之前的版本，执行如下 SQL：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%205f5dbce631edbebf.png)

4. 开启同步操作

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20b94cda8d5df914eb.png)

5. 查看主从同步状态

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%2067297f05ec951aad.png)

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%20704de3484528e916.png)

## 3-3 分库分表

### 3-3-1 介绍

随着互联网及移动互联网的发展，应用系统的数据量也是成指数增长，若采用单数据库进行数据存储，存在以下性能瓶颈：

1. IO 瓶颈：热点数据太多，数据库缓存不足，产生大量磁盘 IO，效率较低。请求数据太多，带宽不够，网络 IO 瓶颈。
2. CPU 瓶颈：排序、分组、连接查询、聚合统计等 SQL 会耗费大量的 CPU 资源，请求数太多，CPU 出现瓶颈。

分库分表的中心思想都是将数据分散存储，使得单一数据库/表的数据量变小来缓解单一数据库的性能问题，从而达到提升数据库性能的目的。

### 3-3-2 垂直拆分

垂直分库：以表为结构，根据业务将不同表拆分到不同库中。

1. 每个库的表结构都不一样。
2. 每个库的数据也不一样。
3. 所有库的并集是全量数据。

垂直分表：以字段为依据，根据字段属性将不同字段拆分到不同表中。

1. 每个表的结构都不一样。
2. 每个表的数据也不一样，一般通过一列（主键/外键）关联。
3. 所有表的并集是全量数据。

### 3-3-3 水平拆分

水平分库：以字段为依据，按照一定策略，将一个表的数据拆分到多个库中。

1. 每个库的表结构都一样。
2. 每个库的数据都不一样。
3. 所有库的并集是全量数据。

水平分表：以字段为依据，按照一定策略，将一个表的数据拆分到多张表中。

1. 每张表的表结构都一样。
2. 每张表的数据都不一样。
3. 所有表的并集是全量数据。

### 3-3-4 实现技术

- shardingJDBC：基于 AOP 原理，在应用程序中对本地执行的 SQL 进行拦截、解析、改写、路由处理。需要自行编码配置实现，只支持 java 语言，性能较高。
- MyCat：数据库分库分表中间件，不用调整代码即可实现分库分表，支持多种语言，性能不及前者。

### 3-3-5 MyCat概述

#### 3-3-5-1 介绍

MyCat 是开源的、活跃的、基于 Java 语言编写的 MySQL 数据库中间件。可以像使用 MySQL 一样使用 mycat，对于开发人员来说根本感觉不到 mycat 的存在。

#### 3-3-5-2 优势

- 性能可靠稳定。
- 强大的技术团队。
- 体系完善。
- 社区活跃。

## 3-4 读写分离

### 3-4-1 介绍

读写分离，简单地说是对数据库的读和写操作分开，以对应不同的数据库服务器。主数据库提供写操作，从数据库提供读操作，这样能有效地减轻单台数据库的压力。  
通过 MyCat 即可轻易实现上述功能，不仅可以支持 MySQL，也可以支持 Oracle 和 SQL Server。

### 3-4-2 双主双从

一个主机 Master1 用于处理所有写请求，它的从机 Slave1 和另一台主机 Master2 还有它的从机 Slave2 负责所有读请求。当 Master1 主机宕机后，Master2 主机负责写请求，Master1、Master2 互为备机。框架图如下：

![](../../../../03%20附件/attachments/知识附件/数据库/1.%20MySQL/运维%20image%2096e3e162776fa2fb.png)


# 4 JDBC

﻿---
tags:
  - 知识
类型: 计算机
领域: MySQL
来源: 黑马程序员MySQL数据库入门到精通课程
日期: 2026-10-08
关联:
---
## 4-1 JDBC

### 4-1-1 JDBC概述

JDBC：Java DataBase Connectivity，意为 Java 数据库连接。  
JDBC 是 Java 提供的一组独立于任何数据库管理系统的 API，它统一了 Java 程序访问关系型数据库的方式。  

> 注意：JDBC 只负责建立连接与执行 SQL，具体的数据读写仍由各个数据库厂商提供的驱动（Driver）实现。  

JDBC 中常用的核心接口与类如下：

```vtable
{"rows": [[{"t": "名称", "rs": 1, "cs": 1}, {"t": "作用", "rs": 1, "cs": 1}], [{"t": "DriverManager", "rs": 1, "cs": 1}, {"t": "驱动管理器，负责加载驱动并获取数据库连接", "rs": 1, "cs": 1}], [{"t": "Connection", "rs": 1, "cs": 1}, {"t": "数据库连接对象，代表与数据库建立的会话", "rs": 1, "cs": 1}], [{"t": "Statement", "rs": 1, "cs": 1}, {"t": "执行 SQL 语句的对象（存在 SQL 注入风险）", "rs": 1, "cs": 1}], [{"t": "PreparedStatement", "rs": 1, "cs": 1}, {"t": "预编译的 SQL 执行对象，可防止 SQL 注入，推荐使用", "rs": 1, "cs": 1}], [{"t": "ResultSet", "rs": 1, "cs": 1}, {"t": "结果集对象，封装查询返回的数据", "rs": 1, "cs": 1}]]}
```

### 4-1-2 JDBC开发步骤

JDBC 操作数据库的完整流程分为六步：注册驱动 → 获取连接对象 → 获取执行 SQL 的对象 → 执行 SQL 并接收结果集 → 处理结果 → 释放资源。

#### 4-1-2-1 注册驱动（注释驱动）

注册驱动的作用是让 JVM 加载数据库厂商提供的驱动类。MySQL 8 之后的版本可以省略该步骤，驱动会自动注册。

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

#### 4-1-2-2 获取连接对象

通过 DriverManager 获取 Connection 连接对象，需要指定连接地址、用户名和密码。

```java
String url = "jdbc:mysql://localhost:3306/prokyhoof";
String username = "root";
String password = "200466";
Connection connection = DriverManager.getConnection(url, username, password);
```

连接地址 url 的格式说明：

```vtable
{"rows": [[{"t": "参数", "rs": 1, "cs": 1}, {"t": "说明", "rs": 1, "cs": 1}], [{"t": "jdbc:mysql", "rs": 1, "cs": 1}, {"t": "协议名称，表示使用 JDBC 访问 MySQL 数据库", "rs": 1, "cs": 1}], [{"t": "//localhost:3306", "rs": 1, "cs": 1}, {"t": "数据库所在主机与端口，本机默认端口为 3306", "rs": 1, "cs": 1}], [{"t": "prokyhoof", "rs": 1, "cs": 1}, {"t": "要连接的数据库名称", "rs": 1, "cs": 1}], [{"t": "useSSL=false", "rs": 1, "cs": 1}, {"t": "关闭 SSL 连接（可选，避免本地连接警告）", "rs": 1, "cs": 1}], [{"t": "serverTimezone=Asia/Shanghai", "rs": 1, "cs": 1}, {"t": "指定服务器时区（可选，解决时区报错）", "rs": 1, "cs": 1}]]}
```

#### 4-1-2-3 获取执行SQL语句的对象

```java
Statement statement = connection.createStatement();
```

#### 4-1-2-4 编写SQL语句，并执行，接收返回的结果集

```java
String sql = "SELECT emp_id, emp_name, emp_salary, emp_age FROM t_emp";
ResultSet resultSet = statement.executeQuery(sql);
```

> 注意：查询操作使用 executeQuery 方法；增删改操作使用 executeUpdate 方法，返回受影响的行数。  

#### 4-1-2-5 处理结果：遍历resultSet结果集

```java
while (resultSet.next()) {
    int empId = resultSet.getInt("emp_id");
    String empName = resultSet.getString("emp_name");
    double empSalary = resultSet.getDouble("emp_salary");
    int age = resultSet.getInt("emp_age");
    System.out.println(empId + "\t" + empName + "\t" + empSalary + "\t" + age);
}
```

#### 4-1-2-6 释放资源（先开后关原则）

```java
resultSet.close();
statement.close();
connection.close();
```

> 注意：释放资源遵循"先开后关"原则，即后创建的对象先关闭；连接属于稀缺资源，用完必须关闭，实际开发中通常放在 finally 块或使用 try-with-resources 自动关闭。  

### 4-1-3 PreparedStatement 防注入

Statement 在执行 SQL 时直接拼接字符串，容易被恶意输入构造出非预期的 SQL，产生 SQL 注入问题。PreparedStatement 使用 `?` 占位符预编译 SQL，参数以绑定方式传入，可有效防止 SQL 注入，且执行效率更高。

```java
String sql = "SELECT * FROM t_emp WHERE emp_name = ?";
PreparedStatement ps = connection.prepareStatement(sql);
ps.setString(1, empName);
ResultSet resultSet = ps.executeQuery();
```

