---
title: sql学习
date: 2016-5-10 13:40:0
tags: 
  - Mysql
  - sql
categories: 数据库
---


## 介绍

### 数据库的概念
 一种存取数据的程序
  - 一种 有很多存取数据的程序
  - 存取 
    - 存：能够保持数据避免丢失
    - 取：按照要求取得数据

### DBMS
 >DATABASE MANAGER SYSTEM

 应用程序->DBMS->数据文件
 
### 为什么要使用数据库呢？

 - 较大数据量   数以亿计
 - 网络访问     来自世界各地
 - 并发访问
 - 高性能
 - 事物控制
 - 持久化和数据安全
 - 数据不丢失
 - 查询数据需求逻辑复杂

### 数据库的类型
 - 关系型数据库
     - 支持sql语句
     - 通过外键进行关联
     - 设计的三范式
         - 字段不可在分
         - 有主键，且非主键字段依赖主键
         - 非主键字段不能相互依赖
 - 非关系型数据库
     - 不支持sql语句
     - 分类:
         - Hadoop		大数据数据库
         - mongoDB      文档型数据库
         - redis        键值数据库
         - Cassandra    架构非常先进的分布式数据库
 - NEWSQL 新型的关系型数据库
     - NewSQL是指这样一类新式的关系型数据库管理系统，针对OLTP（读-写）工作负载，追求提供和NoSQL系统相同扩展性能，且仍然保持ACID和SQL等特性（scalable and ACID and (relational and/or sql -access)）

## SQL学习

### 数据库的基本操作

 1. 显示所有数据库

 ``` show databases```

 2. 创建数据库参数

 ``` show create database 数据库名```

 3. 使用数据库

 ``` use 数据库名 ```

 4. 删除数据库

 ``` drop database 数据库名 ```

### 数据库表的基本操作
 > 表是数据库存储数据的基本单位。个一个表包含若干字段或记录；

 1. 创建表
     - 语法
        CREATE TABLE表名(属性名 数据类型 [完整性约束条件],
        属性名 数据类型   [完整性约束条件],
        属性名 数据类型   [完整性约束条件]);
     - 完整性约束条件

         | 约束条件      | 说明          |
         | ------------- |:-------------:| 
         | FOREIGN KEY      | 标识该属性为该表的主键，可以唯一的标识对应的记录 |
         | FOREIGN KEY      | 标识该属性为该表的外键，与某表的主键关联     |
         | NOT NULL | 标识该属性不能为空      |
         | UNIQUE | 标识该属性的值是唯一的 |
         | AUTO_INCREMENT | 标识该属性自动增长 |
         | DEFAULT | 为该属性设置默认值 |
         
     - 实例
     ```
     创建图书类别表：t_bookType
        CREATE TABLE t_booktype(
        id INT PRIMARY KEYAUTO_INCREMENT,
        bookTypeName VARCHAR(20),
        bookTypeDesc VARCHAR(200)
        );
     ```
     ```
     创建图书表：t_book
        CREATE TABLE t_book(
        id INT PRIMARY KEYAUTO_INCREMENT,
        bookName VARCHAR(20),
        author VARCHAR(10),
        price DECIMAL(6,2),
        bookTypeId INT,
        CONSTRAINT `fk` FOREIGN KEY (`bookTypeId`) REFERENCES `t_bookType` (`id`)
        );

     ```
 2. 查看表
     1. 查看所有的表
         ``` show tables; ```
     2. 查看基本表结构
         ``` desc table 表名 ```
     3. 查看详细表结构
         ``` show create table 表名 ```
 3. 修改表
     1. 修改表名
         ``` alter table 旧表名 rename 新表名;```
     2. 修改字段
         ``` alter table 表名 change 旧字段名 新字段名 数据类型 [完整性约束]; ```
     3. 增加字段
         ``` alter table 表名 add 新字段名 数据类型 [完整性约束] after 原表的属性名; ```
         ``` alter table 表名 add 新字段名 数据类型 [完整性约束] first; ``` 
     4. 删除字段
         ``` alter table 表名 drop 字段名; ```

 4. 删除表
     1. 删除表
         ``` drop table 表名; ```

### 查询数据
 1. 单表查询
     1. 查询所有字段
     2. 查询指定字段
     3. where条件查询
     4. 带in的关键字查询
     5. between and 的范围查询
     6. 带like的模糊查询
     7. 空值查询
     8. 带and的多条件查询
     9. 带or的多条件查询
     10. distinct去重复查询
     11. 对查询结果进行排序
     12. group by 分组查询
     13. limit 分页查询

### 使用聚合函数查询
 1. count()函数
 2. sun()函数
 3. avg()函数
 4. max()函数
 5. min()函数

### 连接查询-多表查询
 > 连接查询是将两个或两个以上的表按照某个条件连接起来，从中选取需要的数据

 1. 内连接查询
     - 内连接查询是一种最常用的连接查询。内连接查询可以查询两个或者两个以上的表； 
 2. 外连接查询
     - 外连接可以查出某一张表的所有信息；
     ``` select 属性名列表 FROM表名1 LEFT|RIGHT JOIN 表名2 ON 表名1.属性名1=表名2.属性名2；```
     1. 左连接查询
         - 可以查询出“表名 1”的所有记录，而“表名 2”中，只能查询出匹配的记录；
     2. 右连接查询
         - 可以查询出“表名 2”的所有记录，而“表名 1”中，只能查询出匹配的记录；
 3. 多条件连接查询

### 子查询
 1. 带in关键字的子查询
     - 一个查询语句的条件可能落在另一个 SELECT语句的查询结果中。
 2. 带比较运算符的子查询
     - 子查询可以使用比较运算符。
 3. 带exitsts关键字的子查询
     - 假如子查询查询到记录，则进行外层查询，否则，不执行外层查询；
 4. 带any关键字的子查询
     - ANY关键字表示满足其中任一条件；
 5. 带all关键字的子查询
     - ALL关键字表示满足所有条件；

### 合并查询结果
 1. union
     - 使用 union关键字是，数据库系统会将所有的查询结果合并到一起，然后去除掉相同的记录；
 2. union all
     - 使用 UNION ALL，不会去除掉系统的记录；
### 为表和字段取别名
 1. 为表取别名
     - 格式: ``` 表名 表的别名 ```
 2. 为字段取别名
     - 格式: ``` 属性名 [as] 别名 ```
 

### 插入数据
 1. 给表的所有字段插入数据
     - 格式：``` INSERT INTO 表名 VALUES(值 1，值 2，值 3，...，值 n)；```
 2. 给表的指定字段插入数据
     - 格式：``` INSERT INTO 表名(属性   1，属性 2，...，属性 n) VALUES(值 1，值 2，值 3，...，值 n)；```
 3. 同时插入多条记录
     - ``` INSERT   INTO表名    [(属性列表)] VALUES(取值列表 1)，(取值列表  2)...，(取值列表n)； ```

### 更新数据
 ``` UPDATE表名 SET 属性名1=取值1属性名2=取值2，...，属性名n=取值n WHERE条件表达式；```

### 删除数据
 ``` DELETE FROM表名   [WHERE条件表达式] ```


    






	



