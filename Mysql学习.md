# Mysql学习笔记

# 1. 数据库简介

## 1.1 什么是数据库

数据库（DB DataBase）

概念：数据仓库，软件，安装在操作系统（window、linux、mac、...）之上

作用：存储数据，管理数据



## 1.2  数据库分类

关系型数据库：（SQL）

- Mysql、Oracle、SqlServer、DB2、SQLlite
- 通过表和表之间，行和列之间的关系进行数据存储。

非关系型数据库：（NOSQL）

- Redis、MongDB
- 非关系型数据库。对象存储，通过对象的自身的属性来决定。



**==DBMS（数据库管理系统）==**

- 数据库的管理软件，维护和获取数据；



## 1.3 Mysql简介

Mysql**是一个关系型数据库**

开源的数据库软件，体积小，速度快。



## 1.4 安装

推荐安装压缩包，下载.exe的会导致卸载很麻烦。

安装教程忽略自行百度。



## 1.5连接数据库

命令行连接

```sql
-- 连接数据库
mysql -u账号 -p密码

-- 修改用户密码
update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';

-- 刷新权限
flush privileges; 

------------------------------------
-- 查看所有数据库
show databases;

-- 进入使用某库
use 库名;

-- 查看数据库中的所有表
show tables;

-- 显示表中所有的信息
describe 表名;

-- 创建一个数据库
create database 库名;

-- 删除数据库
drop database 库名;

-- 显示表结构
desc 表名;

-- 退出连接
exit;
```



**数据库语言** CRUD 增删改查

DDL	定义语言

DML	操作语言

DQL	查询语言

DCL	控制语言



# 2. 操作数据库

操作数据库 > 操作数据库中的表 > 操作数据库中的数据

==mysql关键字不区分大小写==

## 2.1 数据库的列(数据)类型



> 数值（从小到大）

- tinyint		 十分小的数据		1个字节 

- smallint      较小的数据            2个字节

- int                标准的整数            4个字节（常用的）
- bigint           较大的数据            8个字节
- float             单精度浮点数        4个字节

- double        双精度浮点数        8个字节
- decimal      字符串形式的浮点数（**金融计算的时候一般使用decimal**）

> 字符串

- char			字符串固定大小的 	0~255

- varchar       可变字符串                0~65535
-  tinytext      微型文本                    2^8-1
- text              文本串                        2^16-1

> 时间日期

- date			YYYY-MM-DD		日期格式		
- time            HH:mm:ss             时间格式
- datetime    YYYY-MM-DD HH:mm:ss
- timestamp 时间戳
- year             年份表示

> NULL

- 没有值，未知
- ==注意，不要使用NULL进行运算，结果为NULL==



## 2.2 数据库的字段属性

- Unsigned
  1. 无符号的整数
  2. 不能声明为负数
- zerofill
  1. 0填充
  2. 不足的位数，使用0来填充。例如是int(3)类型，值是5，则变成005
- 自增
  1. 通常在上一条记录的基础上进行加1
  2. 通常用来设计为唯一的主键
  3. 可以自定义设计自增的起始值和步长
- 非空 NULL not NULL
  1. 设置为not NULL，插入数据或者修改数据，该字段不能为NULL，否则报错
  2. 设置为NULL，如果不填写值，默认就是NULL
- 默认
  1. 设置默认值后，不填写数据，该字段的值就是设置的默认值



## 2.3 修改表删除表

> 修改

```sql
-- 修改表名
ALTER TABLE 旧表名 RENAME AS 新表名;

-- 增加表的字段
-- 例如：ALTER TABLE 表名 ADD age INt(11);
ALTER TABLE 表名 ADD 字段名 列属性;

-- 修改表的字段（1.重命名；2.修改约束，把列的属性改变）
-- 例如：把age字段从int类型修改为varchar类型，如下
-- ALTER TABLE 表名 MODIFY age VARCHAR(100);
ALTER TABLE 表名 MODIFY 字段名 列属性;              -- 修改约束
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 INT(11);   -- 重命名且修改成INT类型

```

> 删除

```sql
-- 删除表字段
ALTER TABLE 表名 DROP 字段;

-- 删除表
DROP TABLE 表名;
```

==创建删除操作尽量加上判断IF EXISTS，以免报错==



# 3. MYSQL数据管理

## 3.1 外键

**==删除有外键关系的表的时候，必须要先删除引用别人的表（从表），再删除被引用的表（主表）==**



## 3.2 DML语言





## 3.3 添加







## 3.4 修改







## 3.5 删除



