# MySQL数据库

> 学习信息

**学习地址**：https://www.bilibili.com/video/BV1iq4y1u7vj?from=search&seid=6217142348987500628&spm_id_from=333.337.0.0

**作者**：宋红康

**使用数据库**：atguigudb.sql

## 1. 简介

Mysql是关系型数据库(Relational)，Redis是非关系型数据库(key-value)



### 1.1 关系型数据库(RDBMS)

从排名中我们能看出来，关系型数据库绝对是 DBMS 的主流，其中使用最多的 DBMS 分别是 Oracle、MySQL 和 SQL Server。这些都是关系型数据库（RDBMS）。

#### 1.1.1 实质

- 这种类型的数据库是`最古老`的数据库类型，关系型数据库模型是把复杂的数据结构归结为简单的`二元关系`（即二维表格形式）。
- 关系型数据库以`行(row)`和`列(column)`的形式存储数据，以便于用户理解。这一系列的行和列被称为`表(table)`，一组表组成了一个库(database)。
- 表与表之间的数据记录有关系(relationship)。现实世界中的各种实体以及实体之间的各种联系均用`关系模型`来表示。关系型数据库，就是建立在`关系模型`基础上的数据库。

- SQL 就是关系型数据库的查询语言。

 

#### 1.1.2 优势

- **复杂查询**
  可以用SQL语句方便的在一个表以及多个表之间做非常复杂的数据查询。
- **事务支持**
  使得对于安全性能很高的数据访问要求得以实现。



### 1.2 非关系型数据库(非RDBMS)

#### 1.2.1 介绍

**非关系型数据库**，可看成传统关系型数据库的功能`阉割版本`，基于键值对存储数据，不需要经过SQL层的解析，`性能非常高`。同时，通过减少不常用的功能，进一步提高性能。

目前基本上大部分主流的非关系型数据库都是免费的。

#### 1.2.2 有哪些非关系型数据库

相比于 SQL，NoSQL 泛指非关系型数据库，包括了榜单上的键值型数据库、文档型数据库、搜索引擎和列存储等，除此以外还包括图形数据库。也只有用 NoSQL 一词才能将这些技术囊括进来。

**键值型数据库**

键值型数据库通过 Key-Value 键值的方式来存储数据，其中 Key 和 Value 可以是简单的对象，也可以是复杂的对象。Key 作为唯一的标识符，优点是查找速度快，在这方面明显优于关系型数据库，缺点是无法像关系型数据库一样使用条件过滤（比如 WHERE），如果你不知道去哪里找数据，就要遍历所有的键，这就会消耗大量的计算。

键值型数据库典型的使用场景是作为`内存缓存`。`Redis `是最流行的键值型数据库。

**文档型数据库**

此类数据库可存放并获取文档，可以是XML、JSON等格式。在数据库中文档作为处理信息的基本单位，一个文档就相当于一条记录。文档数据库所存放的文档，就相当于键值数据库所存放的“值”。MongoDB 是最流行的文档型数据库。此外，还有CouchDB等。

**搜索引擎数据库**

虽然关系型数据库采用了索引提升检索效率，但是针对全文索引效率却较低。搜索引擎数据库是应用在搜索引擎领域的数据存储形式，由于搜索引擎会爬取大量的数据，并以特定的格式进行存储，这样在检索的时候才能保证性能最优。核心原理是“倒排索引”。

典型产品：Solr、Elasticsearch、Splunk 等。

**列式数据库**

列式数据库是相对于行式存储的数据库，Oracle、MySQL、SQL Server 等数据库都是采用的行式存储（Row-based），而列式数据库是将数据按照列存储到数据库中，这样做的好处是可以大量降低系统的 I/O，适合于分布式文件系统，不足在于功能相对有限。典型产品：HBase等。

**图形数据库**

图形数据库，利用了图这种数据结构存储了实体（对象）之间的关系。图形数据库最典型的例子就是社交网络中人与人的关系，数据模型主要是以节点和边（关系）来实现，特点在于能高效地解决复杂的关系问题。

图形数据库顾名思义，就是一种存储图形关系的数据库。它利用了图这种数据结构存储了实体（对象）之间的关系。关系型数据用于存储明确关系的数据，但对于复杂关系的数据存储却有些力不从心。如社交网络中人物之间的关系，如果用关系型数据库则非常复杂，用图形数据库将非常简单。典型产品：Neo4J、InfoGrid等。



## 2. 关系型数据库设计规则

- 关系型数据库的典型数据结构就是`数据表`，这些数据表的组成都是结构化的（Structured）。
- 将数据放到表中，表再放到库中。
- 一个数据库中可以有多个表，每个表都有一个名字，用来标识自己。表名具有唯一性。
- 表具有一些特性，这些特性定义了数据在表中如何存储，类似Java和Python中 “类”的设计。



### 2.1 表、记录、字段

- E-R（entity-relationship，实体-联系）模型中有三个主要概念是：`实体集`、`属性`、`联系集`。

- 一个实体集（class）对应于数据库中的一个表（table），一个实体（instance）则对应于数据库表中的一行（row），也称为一条记录（record）。一个属性（attribute）对应于数据库表中的一列（column），也称为一个字段（field）。

![image-20210914235450032](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20210914235450032-1634141235163.png)

```
ORM思想 (Object Relational Mapping)体现：
数据库中的一个表  <---> Java或Python中的一个类
表中的一条数据  <---> 类中的一个对象（或实体）
表中的一个列  <----> 类中的一个字段、属性(field)
```



### 2.2 表的关联关系

- 表与表之间的数据记录有关系(relationship)。现实世界中的各种实体以及实体之间的各种联系均用关系模型来表示。
- 四种：一对一关联、一对多关联、多对多关联、自我引用

#### 2.2.1 一对一关联（one-to-one）

- 在实际的开发中应用不多，因为一对一可以创建成一张表。

- 举例：设计`学生表`：学号、姓名、手机号码、班级、系别、身份证号码、家庭住址、籍贯、紧急联系人、...

  - 拆为两个表：两个表的记录是一一对应关系。

  - `基础信息表`（常用信息）：学号、姓名、手机号码、班级、系别
  - `档案信息表`（不常用信息）：学号、身份证号码、家庭住址、籍贯、紧急联系人、...

- 两种建表原则： 

  - **外键唯一**：主表的主键和从表的外键（唯一），形成主外键关系，外键唯一。 

  - **外键是主键**：主表的主键和从表的主键，形成主外键关系。

    

![image-20211201111923065](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201111923065.png)



#### 2.2.2 一对多关系（one-to-many）

- 常见实例场景：`客户表和订单表`，`分类表和商品表`，`部门表和员工表`。
- 举例：
  - 员工表：编号、姓名、...、所属部门

  - 部门表：编号、名称、简介
- 一对多建表原则：在从表(多方)创建一个字段，字段作为外键指向主表(一方)的主键

![image-20210915001013524](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20210915001013524.png)

![image-20210914235610597](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20210914235610597.png)

![image-20210915084623432](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20210915084623432.png)



#### 2.2.3 多对多（many-to-many）

要表示多对多关系，必须创建第三个表，该表通常称为`联接表`，它将多对多关系划分为两个一对多关系。将这两个表的主键都插入到第三个表中。

![image-20211201112622306](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201112622306.png)

- **举例1：学生-课程**

  - `学生信息表`：一行代表一个学生的信息（学号、姓名、手机号码、班级、系别...）

  - `课程信息表`：一行代表一个课程的信息（课程编号、授课老师、简介...）

  - `选课信息表`：一个学生可以选多门课，一门课可以被多个学生选择

    ```
    学号     课程编号  
    1        1001
    2        1001
    1        1002
    ```

- **举例2：产品-订单**

  “订单”表和“产品”表有一种多对多的关系，这种关系是通过与“订单明细”表建立两个一对多关系来定义的。一个订单可以有多个产品，每个产品可以出现在多个订单中。

  - `产品表`：“产品”表中的每条记录表示一个产品。
  - `订单表`：“订单”表中的每条记录表示一个订单。
  - `订单明细表`：每个产品可以与“订单”表中的多条记录对应，即出现在多个订单中。一个订单可以与“产品”表中的多条记录对应，即包含多个产品。

![image-20211201112649337](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201112649337.png)

- **举例3：用户-角色**
- 多对多关系建表原则：需要创建第三张表，中间表中至少两个字段，这两个字段分别作为外键指向各自一方的主键。

![image-20211201112702508](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201112702508.png)



#### 2.2.4  自我引用(Self reference)

![image-20211201112745848](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201112745848.png)



## 3. SQL 分类

**SQL语言在功能上主要分为如下3大类**：

- **DDL（Data Definition Languages、数据定义语言）**，这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来创建、删除、修改数据库和数据表的结构。
  - 主要的语句关键字包括`CREATE`、`DROP`、`ALTER`等。

- **DML（Data Manipulation Language、数据操作语言）**，用于添加、删除、更新和查询数据库记录，并检查数据完整性。
  - 主要的语句关键字包括`INSERT`、`DELETE`、`UPDATE`、`SELECT`等。
  - **SELECT是SQL语言的基础，最为重要。**

- **DCL（Data Control Language、数据控制语言）**，用于定义数据库、表、字段、用户的访问权限和安全级别。
  - 主要的语句关键字包括`GRANT`、`REVOKE`、`COMMIT`、`ROLLBACK`、`SAVEPOINT`等。

> 因为查询语句使用的非常的频繁，所以很多人把查询语句单拎出来一类：DQL（数据查询语言）。
>
> 还有单独将`COMMIT`、`ROLLBACK` 取出来称为TCL （Transaction Control Language，事务控制语言）。



## 4. SQL语言的规则与规范

### 4.1 基本规则

- SQL 可以写在一行或者多行。为了提高可读性，各子句分行写，必要时使用缩进

- 每条命令以 ; 或 \g 或 \G 结束
- 关键字不能被缩写也不能分行
- 关于标点符号
  - 必须保证所有的()、单引号、双引号是成对结束的
  - 必须使用英文状态下的半角输入方式
  - 字符串型和日期时间类型的数据可以使用单引号（' '）表示
  - 列的别名，尽量使用双引号（" "），而且不建议省略as

### 4.2 SQL大小写规范 （建议遵守）

- **MySQL 在 Windows 环境下是大小写不敏感的**
- **MySQL 在 Linux 环境下是大小写敏感的**
  - 数据库名、表名、表的别名、变量名是严格区分大小写的
  - 关键字、函数名、列名(或字段名)、列的别名(字段的别名) 是忽略大小写的。
- **推荐采用统一的书写规范：**
  - 数据库名、表名、表别名、字段名、字段别名等都小写
  - SQL 关键字、函数名、绑定变量等都大写

### 4.3 注释

可以使用如下格式的注释结构

```mysql
单行注释：#注释文字(MySQL特有的方式)
单行注释：-- 注释文字(--后面必须包含一个空格。)
多行注释：/* 注释文字  */
```

### 4.4 命名规则

- 数据库、表名不得超过30个字符，变量名限制为29个
- 必须只能包含 A–Z, a–z, 0–9, _共63个字符
- 数据库名、表名、字段名等对象名中间不要包含空格
- 同一个MySQL软件中，数据库不能同名；同一个库中，表不能重名；同一个表中，字段不能重名
- 必须保证你的字段没有和保留字、数据库系统或常用方法冲突。如果坚持使用，请在SQL语句中使用`（着重号）引起来
- 保持字段名和类型的一致性，在命名字段并为其指定数据类型的时候一定要保证一致性。假如数据类型在一个表里是整数，那在另一个表里可就别变成字符型了

举例：

```mysql
#以下两句是一样的，不区分大小写
show databases;
SHOW DATABASES;

#创建表格
#create table student info(...); #表名错误，因为表名有空格
create table student_info(...); 

#其中order使用``飘号，因为order和系统关键字或系统函数名等预定义标识符重名了
CREATE TABLE `order`(
    id INT,
    lname VARCHAR(20)
);

select id as "编号", `name` as "姓名" from t_stu; #起别名时，as都可以省略
select id as 编号, `name` as 姓名 from t_stu; #如果字段别名中没有空格，那么可以省略""
select id as 编 号, `name` as 姓 名 from t_stu; #错误，如果字段别名中有空格，那么不能省略""
```

### 4.5 数据导入指令

在命令行客户端登录mysql，使用`source`指令导入

```mysql
mysql> source d:\mysqldb.sql
```

```mysql
mysql> desc employees;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| employee_id    | int(6)      | NO   | PRI | 0       |       |
| first_name     | varchar(20) | YES  |     | NULL    |       |
| last_name      | varchar(25) | NO   |     | NULL    |       |
| email          | varchar(25) | NO   | UNI | NULL    |       |
| phone_number   | varchar(20) | YES  |     | NULL    |       |
| hire_date      | date        | NO   |     | NULL    |       |
| job_id         | varchar(10) | NO   | MUL | NULL    |       |
| salary         | double(8,2) | YES  |     | NULL    |       |
| commission_pct | double(2,2) | YES  |     | NULL    |       |
| manager_id     | int(6)      | YES  | MUL | NULL    |       |
| department_id  | int(4)      | YES  | MUL | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
11 rows in set (0.00 sec)
```



## 5. 基本的SELECT语句

### 5.1 SELECT...FROM

- **语法**：

   ```sql
   SELECT   标识选择哪些列
   FROM     标识从哪个表中选择
   ```

  > 一般情况下，除非需要使用表中所有的字段数据，最好不要使用通配符‘*’。使用通配符虽然可以节省输入查询语句的时间，但是获取不需要的列数据通常会降低查询和所使用的应用程序的效率。通配符的优势是，当不知道所需要的列的名称时，可以通过它获取它们。
  >
  > 在生产环境下，不推荐你直接使用`SELECT *`进行查询。

### 5.2 列的别名

- 重命名一个列
- 便于计算
- 紧跟列名，也可以**在列名和别名之间加入关键字AS，别名使用双引号**，以便在别名中包含空格或特殊的字符并区分大小写。
- AS 可以省略
- 建议别名简短，见名知意

### 5.3 去除重复行

默认情况下，查询会返回全部行，包括重复行。

```sql
SELECT department_id
FROM   employees;
```

**在SELECT语句中使用关键字DISTINCT去除重复行**

```sql
SELECT DISTINCT department_id
FROM   employees;
```

```mysql
#查询员工表中一共有哪个部门id呢？
#错误的：没有去重的情况
SELECT department_id FROM employees;
#正确的：去重的情况
SELECT DISTINCT department_id FROM employees;

#错误的：
SELECT salary, DISTINCT department_id FROM employees;

#仅仅是没有报错，但是没有实际意义（得到74条数据）
SELECT DISTINCT department_id,salary FROM employees;
```



这里有两点需要注意：

1. **DISTINCT** 需要放到所有列名的前面，如果写成`SELECT salary, DISTINCT department_id FROM employees`会报错。
2. **DISTINCT** 其实是对后面所有列名的组合进行去重，你能看到最后的结果是 74 条，因为这 74 个部门id不同，都有 salary 这个属性值。如果你想要看都有哪些不同的部门（department_id），只需要写`DISTINCT department_id`即可，后面不需要再加其他的列名了。

### 5.4 空值参与运算

- 所有运算符或列值遇到null值，运算的结果都为null

  ```mysql
  #4. 空值参与运算
  # 1.空值：NULL
  # 2. NULL不等同于0，''，'NULL' ；
  
  # 3. 空值参与运算：结果也一定为空
  SELECT employee_id,salary "月工资",salary * (1 + commission_pct) * 12 "年工资" ,commission_pct FROM employees;
  
  #实际问题的解决方案：引入IFNULL
  SELECT employee_id,salary "月工资",salary * (1 + IFNULL(commission_pct,0)) * 12 "年工资" ,commission_pct FROM employees;
  ```

  

这里你一定要注意，在 MySQL 里面， 空值不等于空字符串。一个空字符串的长度是 0，而一个空值的长度是空。而且，在 MySQL 里面，空值是占用空间的。

### 5.5 着重号

**着重号**是：`` 。也就是Esc下面的键，Tab键上面的键。

在编写sql语句时，可能某些表或者字段被识别成关键词，比如:“ORDER”，如果想要使用ORDER字段且不会报错，就要使用着重号，将ORDER包裹在里面。

```mysql
#错误写法：因为ORDER是关键词，出现报错；
SELECT * FROM ORDER;

#正确写法：使用着重号``
SELECT * FROM `ORDER`;
```

- 结论

我们需要保证表中的字段、表名等没有和保留字、数据库系统或常用方法冲突。如果真的相同，请在SQL语句中使用一对``（着重号）引起来。

### 5.6 查询常数

SELECT 查询还可以对常数进行查询。对的，就是在 SELECT 查询结果中增加一列固定的常数列。这列的取值是我们指定的，而不是从数据表中动态取出的。

QL 中的 SELECT 语法的确提供了这个功能，一般来说我们只从一个表中查询数据，通常不需要增加一个固定的常数列，但如果我们想整合不同的数据源，用常数列作为这个表的标记，就需要查询常数。

比如说，我们想对 employees 数据表中的员工姓名进行查询，同时增加一列字段`corporation`，这个字段固定值为“尚硅谷”，可以这样写：

```mysql
mysql> SELECT '尚硅谷' as corporation, last_name FROM employees;
+-------------+------------+
| corporation | last_name  |
+-------------+------------+
|  尚硅谷 	    | King   	 |
|  尚硅谷 	  	| Kochhar    |
|  尚硅谷 	  	| De Haan    |
+-------------+------------+
```



### 5.7 显示表结构

```mysql
DESCRIBE employees;
或
DESC employees;
```

```mysql
mysql> desc employees;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| employee_id    | int(6)      | NO   | PRI | 0       |       |
| first_name     | varchar(20) | YES  |     | NULL    |       |
| last_name      | varchar(25) | NO   |     | NULL    |       |
| email          | varchar(25) | NO   | UNI | NULL    |       |
| phone_number   | varchar(20) | YES  |     | NULL    |       |
| hire_date      | date        | NO   |     | NULL    |       |
| job_id         | varchar(10) | NO   | MUL | NULL    |       |
| salary         | double(8,2) | YES  |     | NULL    |       |
| commission_pct | double(2,2) | YES  |     | NULL    |       |
| manager_id     | int(6)      | YES  | MUL | NULL    |       |
| department_id  | int(4)      | YES  | MUL | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
11 rows in set (0.00 sec)
```

其中，各个字段的含义分别解释如下：

- Field：表示字段名称。 
- Type：表示字段类型，这里 barcode、goodsname 是文本型的，price 是整数类型的。
- Null：表示该列是否可以存储NULL值。
- Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一部分；MUL表示在列中某个给定值允许出现多次。
- Default：表示该列是否有默认值，如果有，那么值是多少。
- Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。



### 5.8 章节练习

**【题目】** 

1. 查询员工12个月的工资总和，并起别名为ANNUAL SALARY 
2. 查询employees表中去除重复的job_id以后的数据 
3. 查询工资大于12000的员工姓名和工资 
4. 查询员工号为176的员工的姓名和部门号 
5. 显示表 departments 的结构，并查询其中的全部数据 



```mysql
#1. 查询员工12个月的工资总和，并起别名为ANNUAL SALARY
SELECT last_name ,salary * 12 'ANNUAL SALARY' FROM employees; 
#也可以添加上commission_pct奖金
SELECT last_name ,salary * 12 * (1 + IFNULL(commission_pct,0))'ANNUAL SALARY' FROM employees; 
#2. 查询employees表中去除重复的job_id以后的数据
SELECT DISTINCT job_id FROM employees;

#3. 查询工资大于12000的员工姓名和工资
SELECT employee_id,last_name,salary FROM employees WHERE salary > 12000

#4. 查询员工号为176的员工的姓名和部门号
SELECT last_name, department_id FROM employees WHERE employee_id = 176;

#5. 显示表 departments 的结构，并查询其中的全部数据
DESCRIBE departments;
SELECT * FROM departments;
```



## 6. 过滤数据

- 语法：

  ```mysql
  SELECT 字段1,字段2
  FROM 表名
  WHERE 过滤条件
  ```

  - 使用WHERE 子句，将不满足条件的行过滤掉
  - **WHERE子句紧随 FROM子句**

- 举例

  ```mysql
  SELECT employee_id, last_name, job_id, department_id
  FROM   employees
  WHERE  department_id = 90 ;
  ```

  ![image-20211206142344088](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206142344088.png)

  

``` mysql
#练习：查询90号部门的员工信息
SELECT * FROM employees
#过滤条件
WHERE department_id = 90;

#练习：查询last_name为'King'的员工信息
SELECT * FROM employees WHERE last_name = 'King';
```

![image-20211206143139077](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206143139077.png)



## 7. 算术运算符的使用

### 7.1 算术运算符

#### 7.1.1 加减法运算符

算术运算符主要用于数学运算，其可以连接运算符前后的两个数值或表达式，对数值或表达式进行加（+）、减（-）、乘（*）、除（/）和取模（%）运算。

![image-20211206163841787](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206163841787.png)



```MYSQL
SELECT 100 + 'CES' FROM DUAL;
#此时将'CES'看作0处理
#结果为：
+----------------+
| 100 + 'CES'    |
+----------------+
| 100    		 | 
+----------------+

SELECT 100 + '1' FROM DUAL; 
#在SQL中，“+”没有连接的作用，就表示加法运算。此时，会将字符串转换成数值(隐式转换)
#结果为：
+----------------+
| 100 + '1'    	 |
+----------------+
| 101    		 | 
+----------------+

SELECT 100 + '1' FROM DUAL; 
#NULL值参与运算，结果为(NULL);
#结果为：
+----------------+
| 100 + NULL     |
+----------------+
| (NULL)		 | 
+----------------+

SELECT 100 DIV 0 FROM DUAL; 
#分母如果为0，则结果为(NULL);
#结果为：
+----------------+
| 100 DIV 0      |
+----------------+
| (NULL)		 | 
+----------------+

#练习：查询员工为偶数的员工信息
SELECT employee_id,last_name,salary FROM employees
WHERE employee_id % 2 = 0;
```



![image-20211206170522408](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206170522408.png)

![image-20211206170453044](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206170453044.png)

取模运算：%  mod

取模运算的结果与被取模数有关。被取模数是正数，结果为正数，取模数是负数，结果为负数。

![image-20211206171043458](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211206171043458.png)



由运算结果可以得出如下结论：

> - 一个整数类型的值对整数进行加法和减法操作，结果还是一个整数；
> - 一个整数类型的值对浮点数进行加法和减法操作，结果是一个浮点数；
> - 加法和减法的优先级相同，进行先加后减操作与进行先减后加操作的结果是一样的；
> - 在Java中，+的左右两边如果有字符串，那么表示字符串的拼接。但是在MySQL中+只表示数值相加。如果遇到非数值类型，先尝试转成数值，如果转失败，就按0计算。（补充：MySQL中字符串拼接要使用字符串函数CONCAT()实现）

#### 7.1.2 乘法与除法运算符

```mysql
#计算出员工的年基本工资
SELECT employee_id,salary,salary * 12 annual_sal 
FROM employees;
```

由运算结果可以得出如下结论：

> - 一个数乘以整数1和除以整数1后仍得原数；
> - 一个数乘以浮点数1和除以浮点数1后变成浮点数，数值与原数相等；
> - 一个数除以整数后，不管是否能除尽，结果都为一个浮点数；
> - 一个数除以另一个数，除不尽时，结果为一个浮点数，并保留到小数点后4位；
> - 乘法和除法的优先级相同，进行先乘后除操作与先除后乘操作，得出的结果相同。
> - 在数学运算中，0不能用作除数，在MySQL中，一个数除以0为NULL。

#### 7.1.3 求模（求余）运算符

将t22表中的字段i对3和5进行求模（求余）运算。

```mysql
#筛选出employee_id是偶数的员工
SELECT * FROM employees
WHERE employee_id MOD 2 = 0;
```

可以看到，100对3求模后的结果为3，对5求模后的结果为0。



### 7.2 比较运算符

比较运算符用来对表达式左边的操作数和右边的操作数进行比较，比较的结果为真则返回1，比较的结果为假则返回0，其他情况则返回NULL。

比较运算符经常被用来作为SELECT查询语句的条件来使用，返回符合条件的结果记录。

![image-20211209155956797](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209155956797.png)



#### 7.2.1 等号运算符

- 等号运算符（=）判断等号两边的值、字符串或表达式是否相等，如果相等则返回1，不相等则返回0。
- 在使用等号运算符时，遵循如下规则：
  - 如果等号两边的值、字符串或表达式都为字符串，则MySQL会按照字符串进行比较，其比较的是每个字符串中字符的ANSI编码是否相等。
  - 如果等号两边的值都是整数，则MySQL会按照整数来比较两个值的大小。
  - 如果等号两边的值一个是整数，另一个是字符串，则MySQL会将字符串转化为数字进行比较。
  - 如果等号两边的值、字符串或表达式中有一个为NULL，则比较结果为NULL。
- 对比：SQL中赋值符号使用 := 

```mysql
#比较运算符
# 		=		(等于)
#		<=>		(安全等于)
#		<>、!=	(不等于)
#		<		(小于)
#		<=		(小于等于)
#		>		(大于)
#		>=		(大于等于)
SELECT 1 = 2 , 1 != 2 , 1 = '1', 1 = 'a',0 = 'a'
FROM DUAL;
#结果：
+------+-----------+-------+-------+------+
|1 = 2 |	1 != 2 |1 = '1'|1 = 'a'|0 ='a'|
+------+-----------+-------+-------+------+
|	0  |	1	   |	1  |	0  |   1  |
+------+-----------+-------+-------+------+
#字符串存在隐式转换。如果转换数值不成功，则看作0

SELECT 'a' = 'a','ab' = 'ab' , 'a' = 'b'
FROM DUAL;
#结果
+----------+----------------+-----------+
|'a' = 'a' |	'ab' = 'ab' |'a' = 'b'	|
+----------+----------------+-----------+
|		1  |	 	1       |		0   |
+----------+----------------+-----------+

```

![image-20211207102600483](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211207102600483.png)![image-20211207102953293](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211207102953293.png)



#### 7.2.2 安全等于运算符

安全等于运算符（<=>）与等于运算符（=）的作用是相似的，`唯一的区别`是‘<=>’可以用来对NULL进行判断。在两个操作数均为NULL时，其返回值为1，而不为NULL；当一个操作数为NULL时，其返回值为0，而不为NULL。

![image-20211207134702919](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211207134702919.png)

```mysql
#练习：查询表中commission_pct为NULL的数据有哪些
SELECT last_name , salary,commission_pct
FROM employees
WHERE commission_pct <=> NULL;
#也可以写为
SELECT last_name , salary,commission_pct
FROM employees
WHERE commission_pct IS NULL;
```



#### 7.2.3 不等于运算符

不等于运算符（<>和!=）用于判断两边的数字、字符串或者表达式的值是否不相等，如果不相等则返回1，相等则返回0。不等于运算符不能判断NULL值。如果两边的值有任意一个为NULL，或两边都为NULL，则结果为NULL。



此外，还有非符号类型的运算符：

![image-20211207083317340](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211207083317340.png)



```MYSQL
#练习：查询表中commission_pctb不为NULL的数据有哪些
SELECT last_name , salary,commission_pct
FROM employees
WHERE commission_pct IS NOT NULL;
#或


#练习：查询表中commission_pctb为NULL的数据有哪些
SELECT last_name , salary,commission_pct
FROM employees
WHERE ISNULL(commission_pct);
#或
SELECT last_name , salary,commission_pct
FROM employees
WHERE commission_pct IS NULL;
#或
SELECT last_name , salary,commission_pct
FROM employees
WHERE commission_pct <=> NULL;

```



#### 7.2.4 空运算符

空运算符（IS NULL或者ISNULL）判断一个值是否为NULL，如果为NULL则返回1，否则返回0。



#### 7.2.5 非空运算符

非空运算符（IS NOT NULL）判断一个值是否不为NULL，如果不为NULL则返回1，否则返回0。



#### 7.2.6 最小值运算符

语法格式为：LEAST(值1，值2，...，值n)。其中，“值n”表示参数列表中有n个值。在有两个或多个参数的情况下，返回最小值。

#### 7.2.7 最大值运算符

语法格式为：GREATEST(值1，值2，...，值n)。其中，n表示参数列表中有n个值。当有两个或多个参数时，返回值为最大值。假如任意一个自变量为NULL，则GREATEST()的返回值为NULL。

```mysql
SELECT LEAST('g','b','t','m'),GREATEST('g','b','t','m')
FROM DUAL;
#结果
+-----------------------+-----------------------------+
|LEAST('g','b','t','m') |	GREATEST('g','b','t','m') |
+-----------------------+-----------------------------+
|		b 				|		t					  |
+-----------------------+-----------------------------+
```

由结果可以看到，当参数中是整数或者浮点数时，GREATEST将返回其中最大的值；当参数为字符串时，返回字母表中顺序最靠后的字符；当比较值列表中有NULL时，不能判断大小，返回值为NULL。



#### 7.2.8 BETWEEN AND运算符

BETWEEN运算符使用的格式通常为SELECT D FROM TABLE WHERE C BETWEEN A AND B，此时，当C大于或等于A，并且C小于或等于B时，结果为1，否则结果为0。

```mysql
SELECT 1 BETWEEN 0 AND 1, 10 BETWEEN 11 AND 12, 'b' BETWEEN 'a' AND 'c';
+-------------------+----------------------+-------------------------+
| 1 BETWEEN 0 AND 1 | 10 BETWEEN 11 AND 12 | 'b' BETWEEN 'a' AND 'c' |
+-------------------+----------------------+-------------------------+
|                 1 |                    0 |                       1 |
+-------------------+----------------------+-------------------------+

#BETWEEN 条件1(下界) AND 条件2(上界) (查询条件1和条件2范围内的数据，包含条件边界)

#查询工资在6000到8000的员工信息
SELECT employee_id ,last_name,salary
FROM employees
WHERE salary BETWEEN 6000 AND 8000;
#或
SELECT employee_id ,last_name,salary
FROM employees
WHERE salary >= 6000 && salary <=8000 ;
#或
SELECT employee_id ,last_name,salary
FROM employees
WHERE salary >= 6000 AND salary <=8000 ;

#查询工资不在6000到8000的员工信息
SELECT employee_id ,last_name,salary
FROM employees
WHERE salary < 6000 OR salary >8000 ;
#或
SELECT employee_id ,last_name,salary
FROM employees
WHERE salary NOT BETWEEN 6000 AND 8000;
```



#### 7.2.9 IN运算符

IN运算符用于判断给定的值是否是IN列表中的一个值，如果是则返回1，否则返回0。如果给定的值为NULL，或者IN列表中存在NULL，则结果为NULL。

```mysql
#IN (set)
#练习：查询部门为10，20，30部门的员工信息
SELECT department_id,last_name
FROM employees
WHERE department_id = 10 OR department_id = 20 OR department_id = 30;
#或
SELECT department_id,last_name
FROM employees
WHERE department_id IN (10,20,30);
```



#### 7.2.10 NOT IN运算符

NOT IN运算符用于判断给定的值是否不是IN列表中的一个值，如果不是IN列表中的一个值，则返回1，否则返回0。

```mysql
SELECT 'a' NOT IN ('a','b','c'), 1 NOT IN (2,3);
+--------------------------+----------------+
| 'a' NOT IN ('a','b','c') | 1 NOT IN (2,3) |
+--------------------------+----------------+
|                 0        |            1   |
+--------------------------+----------------+

#练习：查询工资不在6000，7000，8000的员工信息
SELECT last_name,salary
FROM employees
WHERE salary !=6000 AND salary !=7000 AND salary !=8000;
#或
SELECT last_name,salary
FROM employees
WHERE salary NOT IN (6000,7000,8000)
```

 

#### 7.2.11 LIKE运算符

LIKE运算符主要用来匹配字符串，通常用于模糊匹配，如果满足条件则返回1，否则返回0。如果给定的值或者匹配条件为NULL，则返回结果为NULL。

LIKE运算符通常使用如下通配符：

```mysql
“%”：匹配0个或多个字符。
“_”：只能匹配一个字符。
```

SQL语句示例如下：

```mysql
SELECT NULL LIKE 'abc', 'abc' LIKE NULL;  
+-----------------+-----------------+
| NULL LIKE 'abc' | 'abc' LIKE NULL |
+-----------------+-----------------+
|          NULL   |          NULL   |
+-----------------+-----------------+

#练习：查询last_name中包含字符'a'的员工信息
# %:代表不确定个数的字符
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '%a%';

#练习：查询last_name中以字符'a'开头的员工信息
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE 'a%';

#练习：查询last_name中包含字符'a'且包含字符'e'的员工信息
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '%a%' AND last_name LIKE '%e%';
#或
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '%a%e%' OR last_name LIKE '%e%a%' ;

#练习：查询last_name中第2个字符是'a'的员工信息
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '_a%' ;

```



**ESCAPE**

- 回避特殊符号的：**使用转义符**。例如：将[%]转为[$%]、[]转为[$]，然后再加上[ESCAPE‘$’]即可。

  ```mysql
  SELECT job_id
  FROM   jobs
  WHERE  job_id LIKE ‘IT\_%‘;
  ```

- 如果使用\表示转义，要省略ESCAPE。如果不是\，则要加上ESCAPE。

  ```mysql
  SELECT job_id
  FROM   jobs
  WHERE  job_id LIKE ‘IT$_%‘ escape ‘$‘;
  ```

```mysql
#练习：查询last_name中第二个字符是'_'且第3个字符是'a'的员工信息
#需要使用转义字符：\
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '_\_a%' ;
#或
SELECT employee_id , last_name 
FROM employees
WHERE last_name LIKE '_$_a%' ESCAPE '$';
```



#### 7.2.12 REGEXP运算符

REGEXP运算符用来匹配字符串，语法格式为：`expr REGEXP 匹配条件`。如果expr满足匹配条件，返回1；如果不满足，则返回0。若expr或匹配条件任意一个为NULL，则结果为NULL。

REGEXP运算符在进行匹配时，常用的有下面几种通配符：

```
（1）‘^’匹配以该字符后面的字符开头的字符串。
（2）‘$’匹配以该字符前面的字符结尾的字符串。
（3）‘.’匹配任何一个单字符。
（4）“[...]”匹配在方括号内的任何字符。例如，“[abc]”匹配“a”或“b”或“c”。为了命名字符的范围，使用一个‘-’。“[a-z]”匹配任何字母，而“[0-9]”匹配任何数字。
（5）‘*’匹配零个或多个在它前面的字符。例如，“x*”匹配任何数量的‘x’字符，“[0-9]*”匹配任何数量的数字，而“*”匹配任何数量的任何字符。

```



```MYSQL
mysql> SELECT 'shkstart' REGEXP '^s', 'shkstart' REGEXP 't$', 'shkstart' REGEXP 'hk';
+------------------------+------------------------+-------------------------+
| 'shkstart' REGEXP '^s' | 'shkstart' REGEXP 't$' | 'shkstart' REGEXP 'hk'  |
+------------------------+------------------------+-------------------------+
|                      1 |                      1 |                       1 |
+------------------------+------------------------+-------------------------+
1 row in set (0.01 sec)
```



```mysql
mysql> SELECT 'atguigu' REGEXP 'gu.gu', 'atguigu' REGEXP '[ab]';
+--------------------------+-------------------------+
| 'atguigu' REGEXP 'gu.gu' | 'atguigu' REGEXP '[ab]' |
+--------------------------+-------------------------+
|                        1 |                       1 |
+--------------------------+-------------------------+
1 row in set (0.00 sec)
```



### 7.3 逻辑运算符

逻辑运算符主要用来判断表达式的真假，在MySQL中，逻辑运算符的返回结果为1、0或者NULL。

MySQL中支持4种逻辑运算符如下：

![image-20211208150626175](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211208150626175.png)



#### 7.3.1 逻辑非运算符

逻辑非（NOT或!）运算符表示当给定的值为0时返回1；当给定的值为非0值时返回0；当给定的值为NULL时，返回NULL。

```mysql
SELECT NOT 1, NOT 0, NOT(1+1), NOT !1, NOT NULL;    
+-------+-------+----------+--------+----------+
| NOT 1 | NOT 0 | NOT(1+1) | NOT !1 | NOT NULL |
+-------+-------+----------+--------+----------+
|     0 |     1 |        0 |      1 |     NULL |
+-------+-------+----------+--------+----------+
```



#### 7.3.2 逻辑与运算符

逻辑与（AND或&&）运算符是当给定的所有值均为非0值，并且都不为NULL时，返回1；当给定的一个值或者多个值为0时则返回0；否则返回NULL。

```mysql
SELECT 1 AND -1, 0 AND 1, 0 AND NULL, 1 AND NULL;
+----------+---------+------------+------------+
| 1 AND -1 | 0 AND 1 | 0 AND NULL | 1 AND NULL |
+----------+---------+------------+------------+
|        1 |       0 |          0 |       NULL |
+----------+---------+------------+------------+
```



#### 7.3.3 逻辑或运算符

逻辑或（OR或||）运算符是当给定的值都不为NULL，并且任何一个值为非0值时，则返回1，否则返回0；当一个值为NULL，并且另一个值为非0值时，返回1，否则返回NULL；当两个值都为NULL时，返回NULL。

```mysql
SELECT 1 OR -1, 1 OR 0, 1 OR NULL, 0 || NULL, NULL || NULL;     
+---------+--------+-----------+-----------+--------------+
| 1 OR -1 | 1 OR 0 | 1 OR NULL | 0 || NULL | NULL || NULL |
+---------+--------+-----------+-----------+--------------+
|       1 |      1 |         1 |    NULL   |       NULL   |
+---------+--------+-----------+-----------+--------------+
```



> 注意：
>
> OR可以和AND一起使用，但是在使用时要注意两者的优先级，由于**AND的优先级高于OR**，因此先对AND两边的操作数进行操作，再与OR中的操作数结合。



#### 7.3.4 逻辑异或运算符

逻辑异或（XOR）运算符是当给定的值中任意一个值为NULL时，则返回NULL；如果两个非NULL的值都是0或者都不等于0时，则返回0；如果一个值为0，另一个值不为0时，则返回1。

```mysql
SELECT 1 XOR -1, 1 XOR 0, 0 XOR 0, 1 XOR NULL, 1 XOR 1 XOR 1, 0 XOR 0 XOR 0;
+----------+---------+---------+------------+---------------+---------------+
| 1 XOR -1 | 1 XOR 0 | 0 XOR 0 | 1 XOR NULL | 1 XOR 1 XOR 1 | 0 XOR 0 XOR 0 |
+----------+---------+---------+------------+---------------+---------------+
|        0 |       1 |       0 |       NULL |             1 |             0 |
+----------+---------+---------+------------+---------------+---------------+
```

```mysql
#XOR：追求的异,
#XOR：只能满足一个条件，满足条件1就不能满足条件2。反之如此；
SELECT last_name,salary,department_id
FROM employees
WHERE department_id = 50 XOR salary > 6000;
```



### 7.4 位运算符

位运算符是在二进制数上进行计算的运算符。位运算符会先将操作数变成二进制数，然后进行位运算，最后将计算结果从二进制变回十进制数。

MySQL支持的位运算符如下：

![image-20211209105702945](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209105702945.png)



#### 7.4.1 按位与运算符

按位与（&）运算符将给定值对应的二进制数逐位进行逻辑与运算。当给定值对应的二进制位的数值都为1时，则该位返回1，否则返回0。

```mysql
SELECT 1 & 10, 20 & 30;
+--------+---------+
| 1 & 10 | 20 & 30 |
+--------+---------+
|      0 |      20 |
+--------+---------+
```

1的二进制数为0001，10的二进制数为1010，所以1 & 10的结果为0000，对应的十进制数为0。20的二进制数为10100，30的二进制数为11110，所以20 & 30的结果为10100，对应的十进制数为20。

#### 7.4.2 按位或运算符

按位或（|）运算符将给定的值对应的二进制数逐位进行逻辑或运算。当给定值对应的二进制位的数值有一个或两个为1时，则该位返回1，否则返回0。

```mysql
SELECT 1 | 10, 20 | 30; 
+--------+---------+
| 1 | 10 | 20 | 30 |
+--------+---------+
|     11 |      30 |
+--------+---------+
```

1的二进制数为0001，10的二进制数为1010，所以1 | 10的结果为1011，对应的十进制数为11。20的二进制数为10100，30的二进制数为11110，所以20 | 30的结果为11110，对应的十进制数为30。

#### 7.4.3 按位异或运算符

按位异或（^）运算符将给定的值对应的二进制数逐位进行逻辑异或运算。当给定值对应的二进制位的数值不同时，则该位返回1，否则返回0。

```mysql
SELECT 1 ^ 10, 20 ^ 30; 
+--------+---------+
| 1 ^ 10 | 20 ^ 30 |
+--------+---------+
|     11 |      10 |
+--------+---------+
```

1的二进制数为0001，10的二进制数为1010，所以1 ^ 10的结果为1011，对应的十进制数为11。20的二进制数为10100，30的二进制数为11110，所以20 ^ 30的结果为01010，对应的十进制数为10。

再举例：

```mysql
SELECT 12 & 5, 12 | 5,12 ^ 5 FROM DUAL;
+--------+--------+--------+
| 12 & 5 | 12 | 5 | 12 ^ 5 |
+--------+--------+--------+
|      4 |     13 |      9 |
+--------+--------+--------+
```



![image-20211209110026105](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209110026105.png)



#### 7.4.4 按位取反运算符

按位取反（~）运算符将给定的值的二进制数逐位进行取反操作，即将1变为0，将0变为1。

```mysql
SELECT 10 & ~1;
+---------+
| 10 & ~1 |
+---------+
|      10 |
+---------+
```



![](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209111653462.png)

由于按位取反（~）运算符的优先级高于按位与（&）运算符的优先级，所以10 & ~1，首先，对数字1进行按位取反操作，结果除了最低位为0，其他位都为1，然后与10进行按位与操作，结果为10。



#### 7.4.5 按位右移运算符

按位右移（>>）运算符将给定的值的二进制数的所有位右移指定的位数。右移指定的位数后，右边低位的数值被移出并丢弃，左边高位空出的位置用0补齐。

```mysql
SELECT 1 >> 2, 4 >> 2;
+--------+--------+
| 1 >> 2 | 4 >> 2 |
+--------+--------+
|      0 |      1 |
+--------+--------+
```



1的二进制数为0000 0001，右移2位为0000 0000，对应的十进制数为0。4的二进制数为0000 0100，右移2位为0000 0001，对应的十进制数为1。

#### 7.4.6 按位左移运算符

按位左移（<<）运算符将给定的值的二进制数的所有位左移指定的位数。左移指定的位数后，左边高位的数值被移出并丢弃，右边低位空出的位置用0补齐。

```mysql
SELECT 1 << 2, 4 << 2;  
+--------+--------+
| 1 << 2 | 4 << 2 |
+--------+--------+
|      4 |     16 |
+--------+--------+
```

1的二进制数为0000 0001，左移两位为0000 0100，对应的十进制数为4。4的二进制数为0000 0100，左移两位为0001 0000，对应的十进制数为16。

**在一定范围内满足：每向左移动1位，相当于乘以2；每向右移动一位，相当于除于2。**



#### 7.4.7 运算符练习题

```mysql
# 1.查询工资不在5000到12000的员工的姓名和工资
SELECT last_name,salary
FROM employees
WHERE salary NOT BETWEEN 5000 AND 12000;
#或
SELECT last_name,salary
FROM employees
WHERE salary < 5000 OR salary > 12000;

# 2.查询在20或50号部门工作的员工姓名和部门号
SELECT last_name,department_id
FROM employees
WHERE department_id IN (20,50);
#或
SELECT last_name,department_id
FROM employees
WHERE department_id = 20 OR department_id = 50;

#3.查询公司中没有管理者的员工姓名及job_id
SELECT last_name,job_id,manager_id
FROM employees
WHERE  ISNULL(manager_id);
#或
SELECT last_name,job_id,manager_id
FROM employees
WHERE  manager_id IS NULL;

# 4.查询公司中有奖金的员工姓名，工资和奖金级别
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct IS NOT NULL;
#或
SELECT last_name,salary,commission_pct
FROM employees
WHERE NOT commission_pct <=> NULL;

# 5.查询员工姓名的第三个字母是a的员工姓名
SELECT last_name
FROM employees
WHERE last_name LIKE "__a%";

# 6.查询姓名中有字母a和k的员工姓名
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%k%' OR last_name LIKE '%k%a%';
#或
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%' AND last_name LIKE'%K%';

# 7.查询出表 employees 表中 first_name 以 'e'结尾的员工信息
# 7.查询出表 employees 表中 first_name 以 'e'结尾的员工信息
SELECT first_name
FROM employees
WHERE first_name LIKE '%e';
#或
SELECT first_name
FROM employees
WHERE first_name REGEXP 'e$';

# 8.查询出表 employees 部门编号在 80-100 之间的姓名、工种
SELECT last_name,department_id,job_id
FROM employees
WHERE department_id BETWEEN 80 AND 100;
#或
SELECT last_name,department_id,job_id
FROM employees
WHERE department_id >= 80 AND department_id <= 100;

# 9.查询出表 employees 的 manager_id 是 100,101,110 的员工姓名、工资、管理者id
SELECT manager_id,last_name,salary
FROM employees
WHERE manager_id IN (100,101,110);
```





## 8. 运算符的优先级



![image-20211209110322144](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209110322144.png)

数字编号越大，优先级越高，优先级高的运算符先进行计算。可以看到，赋值运算符的优先级最低，使用“()”括起来的表达式的优先级最高。

## 9. 使用正则表达式查询

正则表达式通常被用来检索或替换那些符合某个模式的文本内容，根据指定的匹配模式匹配文本中符合要求的特殊字符串。例如，从一个文本文件中提取电话号码，查找一篇文章中重复的单词或者替换用户输入的某些敏感词语等，这些地方都可以使用正则表达式。正则表达式强大而且灵活，可以应用于非常复杂的查询。

MySQL中使用REGEXP关键字指定正则表达式的字符匹配模式。下表列出了REGEXP操作符中常用字符匹配列表。

![image-20211209110422253](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211209110422253.png)



**1. 查询以特定字符或字符串开头的记录**
字符‘^’匹配以特定字符或者字符串开头的文本。

在fruits表中，查询f_name字段以字母‘b’开头的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP '^b';
```

**2. 查询以特定字符或字符串结尾的记录**
字符‘$’匹配以特定字符或者字符串结尾的文本。

在fruits表中，查询f_name字段以字母‘y’结尾的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'y$';
```

**3. 用符号"."来替代字符串中的任意一个字符**
字符‘.’匹配任意一个字符。
在fruits表中，查询f_name字段值包含字母‘a’与‘g’且两个字母之间只有一个字母的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'a.g';
```

**4. 使用"*"和"+"来匹配多个字符**
星号‘*’匹配前面的字符任意多次，包括0次。加号‘+’匹配前面的字符至少一次。

在fruits表中，查询f_name字段值以字母‘b’开头且‘b’后面出现字母‘a’的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP '^ba*';
```

在fruits表中，查询f_name字段值以字母‘b’开头且‘b’后面出现字母‘a’至少一次的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP '^ba+';
```

**5. 匹配指定字符串**
正则表达式可以匹配指定字符串，只要这个字符串在查询文本中即可，如要匹配多个字符串，多个字符串之间使用分隔符‘|’隔开。

在fruits表中，查询f_name字段值包含字符串“on”的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'on';
```

在fruits表中，查询f_name字段值包含字符串“on”或者“ap”的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'on|ap';
```

之前介绍过，LIKE运算符也可以匹配指定的字符串，但与REGEXP不同，LIKE匹配的字符串如果在文本中间出现，则找不到它，相应的行也不会返回。REGEXP在文本内进行匹配，如果被匹配的字符串在文本中出现，REGEXP将会找到它，相应的行也会被返回。对比结果如下所示。

在fruits表中，使用LIKE运算符查询f_name字段值为“on”的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name like 'on';
Empty set(0.00 sec)
```

**6. 匹配指定字符中的任意一个**
方括号“[]”指定一个字符集合，只匹配其中任何一个字符，即为所查找的文本。

在fruits表中，查找f_name字段中包含字母‘o’或者‘t’的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP '[ot]';
```

在fruits表中，查询s_id字段中包含4、5或者6的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE s_id REGEXP '[456]';
```

**7. 匹配指定字符以外的字符**
`“[^字符集合]”`匹配不在指定集合中的任何字符。

在fruits表中，查询f_id字段中包含字母a~e和数字1~2以外字符的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_id REGEXP '[^a-e1-2]';
```

**8. 使用{n,}或者{n,m}来指定字符串连续出现的次数**
“字符串{n,}”表示至少匹配n次前面的字符；“字符串{n,m}”表示匹配前面的字符串不少于n次，不多于m次。例如，a{2,}表示字母a连续出现至少2次，也可以大于2次；a{2,4}表示字母a连续出现最少2次，最多不能超过4次。

在fruits表中，查询f_name字段值出现字母‘x’至少2次的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'x{2,}';
```

在fruits表中，查询f_name字段值出现字符串“ba”最少1次、最多3次的记录，SQL语句如下：

```mysql
mysql> SELECT * FROM fruits WHERE f_name REGEXP 'ba{1,3}';
```



## 10. 排序与分页

### 10.1 排序数据

- 使用 ORDER BY 子句排序
  - **ASC（ascend）: 升序**
  - **DESC（descend）:降序**
- **ORDER BY 子句在SELECT语句的结尾。**



**排序分为：**

- 单列排序
- 多列排序

在对多列进行排序的时候，首先排序的第一列必须有相同的列值，才会对第二列进行排序。如果第一列数据中所有值都是唯一的，将不再对第二列进行排序。

```mysql
#1. 排序
# 如果没有使用排序操作，默认情况下查询返回的数据是按照添加数据的顺序显示的
SELECT * FROM employees;

#使用ORDER BY 对查询到的数据进行排序操作。
#升序：ASC（ascend）
#降序：DESC（descend）
#练习：按照salary从高到低的顺序显示员工信息
SELECT employee_id,last_name,salary
FROM employees
ORDER BY salary DESC;

#练习：按照salary从低到高的顺序显示员工信息
#如果在ORDER BY 后没有显示指定的排序方式，则默认按照升序排列。
SELECT employee_id,last_name,salary
FROM employees
ORDER BY salary ASC;

#2. 可以使用列的别名，进行排序
SELECT employee_id,salary,salary * 12 annual_sal
FROM employees
ORDER BY annual_sal;

#列的别名只能在ORDER BY 中使用，不能在WHERE中使用。
#如下操作报错！找不到annual_sal
SELECT employee_id,salary,salary * 12 AS annual_sal
FROM employees
WHERE annual_sal > 81600;

#3. 强调格式：WHERE 需要声明在FROM后，ORDER BY之前。
SELECT employee_id,salary,department_id
FROM employees
WHERE department_id IN (50,60,70)
ORDER BY department_id DESC;

#4. 二级排序

#练习：显示员工信息，按照department_id的降序排列，salary的升序排列
SELECT employee_id,salary,department_id
FROM employees
ORDER BY department_id DESC,salary ASC;
```



### 10.2 分页

**格式：**

```mysql
LIMIT [位置偏移量,] 行数
```

第一个“位置偏移量”参数指示MySQL从哪一行开始显示，是一个可选参数，如果不指定“位置偏移量”，将会从表中的第一条记录开始（第一条记录的位置偏移量是0，第二条记录的位置偏移量是1，以此类推）；第二个参数“行数”指示返回的记录条数。

**举例：**

```mysql
--前10条记录：
SELECT * FROM 表名 LIMIT 0,10;
或者
SELECT * FROM 表名 LIMIT 10;

--第11至20条记录：
SELECT * FROM 表名 LIMIT 10,10;

--第21至30条记录： 
SELECT * FROM 表名 LIMIT 20,10;
```

> MySQL 8.0中可以使用“LIMIT 3 OFFSET 4”，意思是获取从第5条记录开始后面的3条记录，和“LIMIT 4,3;”返回的结果相同。

- 分页显式公式**：（当前页数-1）*每页条数，每页条数**

  ```mysql
  SELECT * FROM table 
  LIMIT(PageNo - 1)*PageSize,PageSize;**注意：LIMIT 子句必须放在整个SELECT语句的最后！**
  ```

- **注意：LIMIT 子句必须放在整个SELECT语句的最后！**

- 使用 LIMIT 的好处

  约束返回结果的数量可以`减少数据表的网络传输量`，也可以`提升查询效率`。如果我们知道返回结果只有 1 条，就可以使用`LIMIT 1`，告诉 SELECT 语句只需要返回一条记录即可。这样的好处就是 SELECT 不需要扫描完整的表，只需要检索到一条符合条件的记录即可返回。

  
