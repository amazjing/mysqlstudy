MySQL数据库

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

![image11](https://gitee.com/Amazjing/markdown-img/raw/master/img/image11.png)

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

    

![image-20211201111923](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211201111923.png)



#### 2.2.2 一对多关系（one-to-many）

- 常见实例场景：`客户表和订单表`，`分类表和商品表`，`部门表和员工表`。
- 举例：
  - 员工表：编号、姓名、...、所属部门

  - 部门表：编号、名称、简介
- 一对多建表原则：在从表(多方)创建一个字段，字段作为外键指向主表(一方)的主键

![微信截图_20211221155826](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155826.png)



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

![微信截图_20211221155016](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155016.png)

- **举例3：用户-角色**
- 多对多关系建表原则：需要创建第三张表，中间表中至少两个字段，这两个字段分别作为外键指向各自一方的主键。

![image-202112011127025](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-202112011127025.png)



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

![image-202112061431390](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-202112061431390.png)



## 7. 算术运算符的使用

### 7.1 算术运算符

#### 7.1.1 加减法运算符

算术运算符主要用于数学运算，其可以连接运算符前后的两个数值或表达式，对数值或表达式进行加（+）、减（-）、乘（*）、除（/）和取模（%）运算。

![image-202112061638417](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-202112061638417.png)



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



![image-202112061705224](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-202112061705224.png)

![image-202112061704530](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-202112061704530.png)

取模运算：%  mod

取模运算的结果与被取模数有关。被取模数是正数，结果为正数，取模数是负数，结果为负数。

![微信截图_20211221155120](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155120.png)



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

![微信截图_20211221155225](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155225.png)



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

![微信截图_20211221155303](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155303.png)





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



![微信截图_20211221155353](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155353.png)

数字编号越大，优先级越高，优先级高的运算符先进行计算。可以看到，赋值运算符的优先级最低，使用“()”括起来的表达式的优先级最高。

## 9. 使用正则表达式查询

正则表达式通常被用来检索或替换那些符合某个模式的文本内容，根据指定的匹配模式匹配文本中符合要求的特殊字符串。例如，从一个文本文件中提取电话号码，查找一篇文章中重复的单词或者替换用户输入的某些敏感词语等，这些地方都可以使用正则表达式。正则表达式强大而且灵活，可以应用于非常复杂的查询。

MySQL中使用REGEXP关键字指定正则表达式的字符匹配模式。下表列出了REGEXP操作符中常用字符匹配列表。

![微信截图_20211221155428](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155428.png)



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

```mysql
# 分页
# mysql使用limit实现数据分页显示

#需求1：每页显示20条记录，此时显示第一页
SELECT employee_id,last_name
FROM employees
LIMIT 0,20;

#需求2：每页显示20条记录，此时显示第二页
SELECT employee_id,last_name
FROM employees
LIMIT 20,20;

#需求3：每页显示20条记录，此时显示第三页
SELECT employee_id,last_name
FROM employees
LIMIT 40,20;

#需求：每页显示pageSize条记录，此时显示第pageNo页
#公式：LIMIT (pageNo-1) * pageSize , pageSize;

# WHERE ... ORDER BY ... LIMIT 声明顺序如下：
SELECT employee_id,last_name,salary
FROM employees
WHERE salary > 6000
ORDER BY salary DESC
LIMIT 0,10;

#练习：表中有107条数据，我们只想要显示第32、33条数据
SELECT employee_id,last_name
FROM employees
LIMIT 31,2;

#MySQL8.0 新特性：LIMIT ... OFFSET ...
#练习：表中有107条数据，我们只想要显示第32、33条数据
SELECT employee_id,last_name
FROM employees
LIMIT 2 OFFSET 31;

```



### 10.3 排序与分页练习

```mysql
#1. 查询员工的姓名和部门号和年薪，按年薪降序,按姓名升序显示 
SELECT last_name,department_id,salary * 12 annual_salary
FROM employees
ORDER BY annual_salary DESC,last_name ASC;

#2. 查询工资不在 8000 到 17000 的员工的姓名和工资，按工资降序，显示第21到40位置的数据 
SELECT last_name,salary
FROM employees
WHERE salary > 17000 OR salary < 8000
ORDER BY salary DESC
LIMIT 20,20;
#或使用BETWEEN ... AND ...
SELECT last_name,salary
FROM employees
WHERE salary NOT BETWEEN 8000 AND 17000
ORDER BY salary DESC
LIMIT 20,20;
#或 MySQL8.0
SELECT last_name,salary
FROM employees
WHERE salary NOT BETWEEN 8000 AND 17000
ORDER BY salary DESC
LIMIT 20 OFFSET 20;

#3. 查询邮箱中包含 e 的员工信息，并先按邮箱的字节数降序，再按部门号升序
SELECT employee_id,last_name,email,department_id
FROM employees
WHERE email LIKE '%e%'
ORDER BY LENGTH(email) DESC , department_id ASC
#或使用表达式
SELECT employee_id,last_name,email,department_id
FROM employees
WHERE email REGEXP '[e]'
ORDER BY LENGTH(email) DESC , department_id ASC
```



## 11. 多表查询

多表查询，也称为关联查询，指两个或更多个表一起完成查询操作。

前提条件：这些一起查询的表之间是有关系的（一对一、一对多），它们之间一定是有关联字段，这个关联字段可能建立了外键，也可能没有建立外键。比如：员工表和部门表，这两个表依靠“部门编号”进行关联。



### 11.1 出现笛卡尔积的错误

```mysql
#错误的原因：缺少了多表的连接条件

#需求：查询每个员工的部门名称

#错误的实现方式：每个员工都与每个部门匹配了一遍。
SELECT employee_id,department_name
FROM employees,departments;		#查询出2889条记录
#错误的实现方式：
SELECT employee_id,department_name
FROM employees CROSS JOIN departments;	#查询出2889条记录

#为什么会出现2889条数据

SELECT * FROM employees;	#结果：107

SELECT * FROM departments;	#结果：27
#人员与部门相乘就是2889条记录

#多表查询的正确方式：需要有连接条件
SELECT employee_id,department_name
FROM employees,departments
#两个表的连接条件
WHERE employees.department_id = departments.department_id;

#如果查询语句中出现了多个表中都存在的字段，则必须陟明此字段所在的表。

#建议：从sql优化的角度，建议多表查询时，每个字段都指明其所在的表。

#可以给表起别名，在SELECT和WHERE中使用表的别名。
#如果给表起了别名，一旦在SELECT或WHERE中使用表名的话，则必须使用表的别名，而不能再使用表的原名。
SELECT emp.employee_id,dept.department_name,emp.department_id
FROM employees emp,departments dept
WHERE emp.department_id = dept.department_id;

#如果有N个表实现多表的查询，则需要至少n-1个连接条件
#练习：查询员工的employee_id,last_name,department_name,city
SELECT employee_id,last_name,department_name,city
FROM employees e,departments d,locations l
WHERE e.department_id = d.department_id
AND d.location_id = l.location_id;

```

### 11.2 笛卡尔积（或交叉连接）的理解

笛卡尔乘积是一个数学运算。假设我有两个集合 X 和 Y，那么 X 和 Y 的笛卡尔积就是 X 和 Y 的所有可能组合，也就是第一个对象来自于 X，第二个对象来自于 Y 的所有可能。组合的个数即为两个集合中元素个数的乘积数。

![image-20211213110238932](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211213110238932.png)

### 11.3 案例分析与问题解决

- **笛卡尔积的错误会在下面条件下产生**：

  - 省略多个表的连接条件（或关联条件）
  - 连接条件（或关联条件）无效
  - 所有表中的所有行互相连接

- 为了避免笛卡尔积， 可以**在 WHERE 加入有效的连接条件。**

- 加入连接条件后，查询语法：

  ```mysql
  SELECT	table1.column, table2.column
  FROM	table1, table2
  WHERE	table1.column1 = table2.column2;  #连接条件
  ```

  - 在 WHERE子句中写入连接条件。

- 正确写法：

  ```mysql
  #案例：查询员工的姓名及其部门名称
  SELECT last_name, department_name
  FROM employees, departments
  WHERE employees.department_id = departments.department_id;
  ```

- **在表中有相同列时，在列名之前加上表名前缀。**



## 12. 多表查询的分类

- 角度1：等值连接	vs	非等值连接
- 角度2：自连接	vs	非自连接
- 角度3：内连接	vs	外连接



### 12.1 等值连接	vs	非等值连接

```mysql
#非等值连接的例子
SELECT * FROM job_grades;

SELECT e.last_name,e.salary,j.grade_level
FROM employees e,job_grades j
WHERE e.salary BETWEEN j.lowest_sal AND j.highest_sal;
```



### 12.2 自连接 	vs	非自连接

自连接经典的案例就是父级部门和子级之间的关系。例如：一张表，父级部门字段使用的是自增的主键id表示部门id，表示子级部门对应的父级id字段是dept_id。这张表就存在自连接。

    ```mysql
    #练习： 查询员工id，员工姓名及其管理者的id和姓名
    SELECT emp.employee_id,emp.last_name,mgr.employee_id,mgr.last_name
    FROM employees emp , employees mgr
    WHERE emp.manager_id = mgr.employee_id;
    ```



### 12.3 内连接	vs	外连接

**内连接**: 合并具有同一列的两个以上的表的行, **结果集中不包含一个表与另一个表不匹配的行**

```mysql
#案例：查询员工的姓名及其部门名称
#结果为106条数据；事实上本来应该有107条数据，有一条数据是where条件不成立的数据。
SELECT last_name, department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;
```



**外连接**: 两个表在连接过程中除了返回满足连接条件的行以外**还返回左（或右）表中不满足条件的行** **，这种连接称为左（或右） 外连接**。没有匹配的行时, 结果表中相应的列为空(NULL)。

**外连接的分类**：

- 左外连接
- 右外连接
- 满外连接

```mysql
#SQL92语法实现外连接：使用 + ;MySQL不支持SQL92语法中外连接的写法
SELECT employee_id, department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id(+);

#使用JOIN ... ON的方式实现多表的查询;解决外连接问题;
#SQL99语法：实现内连接
SELECT last_name, department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;

#SQL99语法实现外连接;

#练习：查询所有的员工的last_name,department_name信息
#左外连接：
SELECT last_name, department_name
FROM employees e
LEFT  JOIN departments d
ON e.department_id = d.department_id;	#107条数据

#右外连接：
SELECT last_name, department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id;	#122条数据

#满外连接：MySQL不支持 FULL OUTER JOIN连接方式
```



### 12.4 满外连接

- 满外连接的结果 = 左右表匹配的数据 + 左表没有匹配到的数据 + 右表没有匹配到的数据。
- SQL99语法是支持满外连接的。使用FULL JOIN 或 FULL OUTER JOIN来实现。
- 需要注意的是，MySQL不支持FULL JOIN，但是可以用 LEFT JOIN **UNION** RIGHT join代替。



### 12.5 UNION的使用

**合并查询结果**
利用UNION关键字，可以给出多条SELECT语句，并将它们的结果组合成单个结果集。合并时，两个表对应的列数和数据类型必须相同，并且相互对应。各个SELECT语句之间使用UNION或UNION ALL关键字分隔。

语法格式：

```mysql
SELECT column,... FROM table1
UNION [ALL]
SELECT column,... FROM table2
```

**UNION操作符**

![image-20211221104813948](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211221104813948.png)

UNION 操作符返回两个查询的结果集的并集，去除重复记录。

**UNION ALL操作符**

![image-20211221104834602](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211221104834602.png)

UNION ALL操作符返回两个查询的结果集的并集。对于两个结果集的重复部分，不去重。

> 注意：执行UNION ALL语句时所需要的资源比UNION语句少。如果明确知道合并数据后的结果数据不存在重复数据，或者不需要去除重复的数据，则尽量使用UNION ALL语句，以提高数据查询的效率。

举例：查询部门编号>90或邮箱包含a的员工信息

```mysql
#方式1
SELECT * FROM employees WHERE email LIKE '%a%' OR department_id>90;

#方式2
SELECT * FROM employees  WHERE email LIKE '%a%'
UNION
SELECT * FROM employees  WHERE department_id>90;
```

举例：查询中国用户中男性的信息以及美国用户中年男性的用户信息

```mysql
SELECT id,cname FROM t_chinamale WHERE csex='男'
UNION ALL
SELECT id,tname FROM t_usmale WHERE tGender='male';
```



### 12.6 7种SQL JOINS的实现

![微信截图_20211221155518](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211221155518.png)



#### 12.6.1 代码实现

![image-20211221110402114](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20211221110402114.png)

A表：员工表employees；B表：departments部门表

```mysql
#中图：内连接 A∩B
SELECT employee_id,last_name,department_name
FROM employees e 
JOIN departments d
ON e.`department_id` = d.`department_id`;	#结果：106条
```

```mysql
#左上图：左外连接
SELECT employee_id,last_name,department_name
FROM employees e 
LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;	#结果：107条
```

```mysql
#右上图：右外连接
SELECT employee_id,last_name,department_name
FROM employees e 
RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;	#结果：122条
```

```mysql
#左中图：A - A∩B
SELECT employee_id,last_name,department_name
FROM employees e 
LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL;	#结果：1条
```

```mysql
#右中图：B-A∩B
SELECT employee_id,last_name,department_name
FROM employees e 
RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;	#结果：16条
```

```mysql
#左下图：满外连接
#方式1：左上图 UNION ALL 右中图
SELECT employee_id,department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id
UNION ALL
SELECT employee_id,department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id
WHERE e.department_id IS NULL;	#结果：123条

#方式1： 左中图 UNION ALL 右上图  A∪B
SELECT employee_id,last_name,department_name
FROM employees e 
LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL  #没有去重操作，效率高
SELECT employee_id,last_name,department_name
FROM employees e 
RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;	#结果：123条
```

```mysql
#右下图
#左中图 UNION ALL 右中图  A ∪B- A∩B 或者 (A -  A∩B) ∪ （B - A∩B）
SELECT employee_id,last_name,department_name
FROM employees e 
LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,last_name,department_name
FROM employees e 
RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;	#结果17条
```



#### 12.6.2 语法格式小结

- 左中图

```mysql
#实现A -  A∩B
select 字段列表
from A表 left join B表
on 关联条件
where 从表关联字段 is null and 等其他子句;
```

- 右中图

```mysql
#实现B -  A∩B
select 字段列表
from A表 right join B表
on 关联条件
where 从表关联字段 is null and 等其他子句;
```

- 左下图

```mysql
#实现查询结果是A∪B
#用左外的A，union 右外的B
select 字段列表
from A表 left join B表
on 关联条件
where 等其他子句

union 

select 字段列表
from A表 right join B表
on 关联条件
where 等其他子句;
```

- 右下图

```mysql
#实现A∪B -  A∩B  或   (A -  A∩B) ∪ （B - A∩B）
#使用左外的 (A -  A∩B)  union 右外的（B - A∩B）
select 字段列表
from A表 left join B表
on 关联条件
where 从表关联字段 is null and 等其他子句

union

select 字段列表
from A表 right join B表
on 关联条件
where 从表关联字段 is null and 等其他子句
```



### 12.8 多表查询的课后练习

1. 显示所有员工的姓名，部门号和部门名称。

   ```mysql
   #结果：107条数据
   SELECT e.last_name,e.department_id,d.department_name
   FROM employees e
   LEFT JOIN departments d
   ON e.department_id = d.department_id;
   ```

2. 查询90号部门员工的job_id和90号部门的location_id

   ```mysql
   #结果:3条数据
   SELECT e.job_id,d.location_id
   FROM employees e
   JOIN departments d
   ON e.department_id = d.department_id
   WHERE e.department_id = 90
   ```

   结果：

   | job_id  | location_id |
   | ------- | ----------- |
   | AD_PRES | 1700        |
   | AD_VP   | 1700        |
   | AD_VP   | 1700        |

3. 查询所有有奖金的员工的 last_name , department_name , location_id , city

   ```mysql
   #先查询的看看所有有奖金的员工也就是commission_pct字段不为NULL的有多少条数据
   SELECT * FROM employees
   WHERE commission_pct IS NOT NULL;
   #以上语句查询出结果为35条数据，那么这道题的查询结果也必须为35条数据！！！
   
   
   #注意：使用以下sql语句查询得到的是34条数据，原因是一位员工，没有部门id，但是有奖金。
   #产生错误的原因是因为，没有使用外连接。
   SELECT e.last_name,e.commission_pct,d.department_name,d.location_id,l.city
   FROM employees e
   JOIN departments d
   ON e.department_id = d.department_id
   JOIN locations l
   ON d.location_id = l.location_id
   WHERE e.commission_pct IS NOT NULL;
   
   #正确的SQL语句;结果：35条数据
   SELECT e.last_name,e.commission_pct,d.department_name,d.location_id,l.city
   FROM employees e
   LEFT JOIN departments d
   ON e.department_id = d.department_id
   LEFT JOIN locations l
   ON d.location_id = l.location_id
   WHERE e.commission_pct IS NOT NULL;
   ```

4. 查询city在Toronto工作的员工的 last_name , job_id , department_id , department_name

   ```mysql
   #结果:2条数据
   SELECT e.last_name,e.job_id,d.department_id,d.department_name
   FROM employees e
   JOIN departments d
   ON e.department_id = d.department_id
   JOIN locations l
   ON d.location_id = l.location_id
   WHERE l.city = 'Toronto';
   ```

   结果：

   | last_name | job_id | department_id | department_name |
   | --------- | ------ | ------------- | --------------- |
   | Hartstein | MK_MAN | 20            | Marketing       |
   | Fay       | MK_REP | 20            | Marketing       |

5. 查询员工所在的部门名称、部门地址、姓名、工作、工资，其中员工所在部门的部门名称为'Executive' 

   ```mysql
   #结果：3条数据
   SELECT d.department_name,l.street_address,e.last_name,j.job_id,e.salary
   FROM departments d
   JOIN locations l
   ON d.location_id = l.location_id
   JOIN employees e
   ON d.department_id = e.department_id
   JOIN jobs j
   ON e.job_id = j.job_id
   WHERE d.department_name = 'Executive';
   ```

   结果：

   | department_name | street_address  | last_name | job_id  | salary   |
   | --------------- | --------------- | --------- | ------- | -------- |
   | Executive       | 2004 Charade Rd | King      | AD_PRES | 24000.00 |
   | Executive       | 2004 Charade Rd | Kochhar   | AD_VP   | 17000.00 |
   | Executive       | 2004 Charade Rd | De Haan   | AD_VP   | 17000.00 |

6. 查询指定员工的姓名，员工号，以及他的管理者的姓名和员工号

   ```mysql
   #结果类似于下面的格式 
   employees	Emp#	manager	Mgr# 
   
   kochhar		101		king	100 
   #结果：107条数据
   SELECT emp.last_name 'employees',emp.employee_id 'Emp#',mgr.last_name 'manager',mgr.employee_id 'Mgr#'
   FROM employees emp 
   LEFT JOIN employees mgr
   ON emp.manager_id = mgr.employee_id
   ```

7. 查询哪些部门没有员工

   ```mysql
   #结果：16条数据
   SELECT d.department_id ,d.department_name
   FROM departments d
   LEFT JOIN employees e
   ON d.department_id = e.department_id
   WHERE e.department_id IS NULL
   
   #方式2：使用子查询
   SELECT department_id FROM departments d 
   WHERE NOT EXISTS ( 
   	SELECT * 
   	FROM employees e 
   	WHERE 
   	e.`department_id` = d.`department_id` 
   )
   ```

8. 查询哪个城市没有部门

   ```mysql
   #结果：16条数据
   SELECT l.location_id,l.city 
   FROM locations l 
   LEFT JOIN departments d 
   ON l.`location_id` = d.`location_id` 
   WHERE d.`location_id` IS NULL
   ```

9. 查询部门名为 Sales 或 IT 的员工信息

   ```mysql
   #结果：39条数据
   SELECT e.employee_id,e.last_name,d.department_name 
   FROM employees e,departments d 
   WHERE e.department_id = d.`department_id` AND d.`department_name` IN ('Sales','IT');
   ```

   

## 13. 单行函数

### 13.1 什么是函数

函数在计算机语言的使用中贯穿始终，函数的作用是什么呢？它可以把我们经常使用的代码封装起来，需要的时候直接调用即可。这样既`提高了代码效率`，又`提高了可维护性`。在 SQL 中我们也可以使用函数对检索出来的数据进行函数操作。使用这些函数，可以极大地`提高用户对数据库的管理效率`。

从函数定义的角度出发，我们可以将函数分成`内置函数`和`自定义函数`。在 SQL 语言中，同样也包括了内置函数和自定义函数。内置函数是系统内置的通用函数，而自定义函数是我们根据自己的需要编写。

### 13.2 MySQL的内置函数及分类

MySQL提供的内置函数从`实现的功能角度`可以分为数值函数、字符串函数、日期和时间函数、流程控制函数、加密与解密函数、获取MySQL信息函数、聚合函数等。这里，我将这些丰富的内置函数再分为两类：`单行函数`、`聚合函数（或分组函数）`。

**两种SQL函数**

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227142300.png)



**单行函数**

- 操作数据对象
- 接受参数返回一个结果
- **只对一行进行变换**
- **每行返回一个结果**
- 可以嵌套
- 参数可以是一列或一个值



### 13.3 数值函数

#### 13.3.1 基本函数

| 函数                | 用法                                                         |
| ------------------- | ------------------------------------------------------------ |
| ABS(x)              | 返回x的绝对值                                                |
| SIGN(X)             | 返回X的符号。正数返回1，负数返回-1，0返回0                   |
| PI()                | 返回圆周率的值                                               |
| CEIL(x)，CEILING(x) | 返回大于或等于某个值的最小整数                               |
| FLOOR(x)            | 返回小于或等于某个值的最大整数                               |
| LEAST(e1,e2,e3…)    | 返回列表中的最小值                                           |
| GREATEST(e1,e2,e3…) | 返回列表中的最大值                                           |
| MOD(x,y)            | 返回X除以Y后的余数                                           |
| RAND()              | 返回0~1的随机值                                              |
| RAND(x)             | 返回0~1的随机值，其中x的值用作种子值，相同的X值会产生相同的随机数 |
| ROUND(x)            | 返回一个对x的值进行四舍五入后，最接近于X的整数               |
| ROUND(x,y)          | 返回一个对x的值进行四舍五入后最接近X的值，并保留到小数点后面Y位 |
| TRUNCATE(x,y)       | 返回数字x截断为y位小数的结果                                 |
| SQRT(x)             | 返回x的平方根。当X的值为负数时，返回NULL                     |

举例：

```mysql
SELECT ABS(-123),ABS(32),SIGN(-23),SIGN(43),PI(),CEIL(32.32),CEILING(-43.23),FLOOR(32.32),FLOOR(-43.23),MOD(12,5)FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227145825.png)

```mysql
SELECT RAND(),RAND(),RAND(10),RAND(10),RAND(-1),RAND(-1)
FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227145945.png)

```mysql
SELECT ROUND(12.33),ROUND(12.343,2),ROUND(12.324,-1),TRUNCATE(12.66,1),TRUNCATE(12.66,-1)
FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227150100.png)



#### 13.3.2 角度与弧度互换函数

| 函数       | 用法                                  |
| ---------- | ------------------------------------- |
| RADIANS(x) | 将角度转化为弧度，其中，参数x为角度值 |
| DEGREES(x) | 将弧度转化为角度，其中，参数x为弧度值 |

```mysql
SELECT RADIANS(30),RADIANS(60),RADIANS(90),DEGREES(2*PI()),DEGREES(RADIANS(90))
FROM DUAL;
```



#### 13.3.3 三角函数

| 函数       | 用法                                                         |
| ---------- | ------------------------------------------------------------ |
| SIN(x)     | 返回x的正弦值，其中，参数x为弧度值                           |
| ASIN(x)    | 返回x的反正弦值，即获取正弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| COS(x)     | 返回x的余弦值，其中，参数x为弧度值                           |
| ACOS(x)    | 返回x的反余弦值，即获取余弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| TAN(x)     | 返回x的正切值，其中，参数x为弧度值                           |
| ATAN(x)    | 返回x的反正切值，即返回正切值为x的值                         |
| ATAN2(m,n) | 返回两个参数的反正切值                                       |
| COT(x)     | 返回x的余切值，其中，X为弧度值                               |



#### 13.3.4 指数与对数

| 函数                 | 用法                                                 |
| -------------------- | ---------------------------------------------------- |
| POW(x,y)，POWER(X,Y) | 返回x的y次方                                         |
| EXP(X)               | 返回e的X次方，其中e是一个常数，2.718281828459045     |
| LN(X)，LOG(X)        | 返回以e为底的X的对数，当X <= 0 时，返回的结果为NULL  |
| LOG10(X)             | 返回以10为底的X的对数，当X <= 0 时，返回的结果为NULL |
| LOG2(X)              | 返回以2为底的X的对数，当X <= 0 时，返回NULL          |

```mysql
mysql> SELECT POW(2,5),POWER(2,4),EXP(2),LN(10),LOG10(10),LOG2(4)
    -> FROM DUAL;
+----------+------------+------------------+-------------------+-----------+---------+
| POW(2,5) | POWER(2,4) | EXP(2)           | LN(10)            | LOG10(10) | LOG2(4) |
+----------+------------+------------------+-------------------+-----------+---------+
|       32 |         16 | 7.38905609893065 | 2.302585092994046 |         1 |       2 |
+----------+------------+------------------+-------------------+-----------+---------+
1 row in set (0.00 sec)
```



#### 13.3.5 进制间的转换

| 函数          | 用法                     |
| ------------- | ------------------------ |
| BIN(x)        | 返回x的二进制编码        |
| HEX(x)        | 返回x的十六进制编码      |
| OCT(x)        | 返回x的八进制编码        |
| CONV(x,f1,f2) | 返回f1进制数变成f2进制数 |

```mysql
mysql> SELECT BIN(10),HEX(10),OCT(10),CONV(10,2,8)
    -> FROM DUAL;
+---------+---------+---------+--------------+
| BIN(10) | HEX(10) | OCT(10) | CONV(10,2,8) |
+---------+---------+---------+--------------+
| 1010    | A       | 12      | 2            |
+---------+---------+---------+--------------+
1 row in set (0.00 sec)
```



### 13.4 字符串函数

| 函数                              | 用法                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| ASCII(S)                          | 返回字符串S中的第一个字符的ASCII码值                         |
| CHAR_LENGTH(s)                    | 返回字符串s的字符数。作用与CHARACTER_LENGTH(s)相同           |
| LENGTH(s)                         | 返回字符串s的字节数，和字符集有关                            |
| **CONCAT(s1,s2,......,sn)**       | **连接s1,s2,......,sn为一个字符串，可以根据查出来的数据字段与自定义的字符串进行拼接** |
| CONCAT_WS(x, s1,s2,......,sn)     | 同CONCAT(s1,s2,...)函数，但是每个字符串之间要加上x           |
| INSERT(str, idx, len, replacestr) | 将字符串str从第idx位置开始，len个字符长的子串替换为字符串replacestr |
| REPLACE(str, a, b)                | 用字符串b替换字符串str中所有出现的字符串a                    |
| UPPER(s) 或 UCASE(s)              | 将字符串s的所有字母转成大写字母                              |
| LOWER(s)  或LCASE(s)              | 将字符串s的所有字母转成小写字母                              |
| LEFT(str,n)                       | 返回字符串str最左边的n个字符                                 |
| RIGHT(str,n)                      | 返回字符串str最右边的n个字符                                 |
| LPAD(str, len, pad)               | 用字符串pad对str最左边进行填充，直到str的长度为len个字符     |
| RPAD(str ,len, pad)               | 用字符串pad对str最右边进行填充，直到str的长度为len个字符     |
| LTRIM(s)                          | 去掉字符串s左侧的空格                                        |
| RTRIM(s)                          | 去掉字符串s右侧的空格                                        |
| TRIM(s)                           | 去掉字符串s开始与结尾的空格                                  |
| TRIM(s1 FROM s)                   | 去掉字符串s开始与结尾的s1                                    |
| TRIM(LEADING s1 FROM s)           | 去掉字符串s开始处的s1                                        |
| TRIM(TRAILING s1 FROM s)          | 去掉字符串s结尾处的s1                                        |
| REPEAT(str, n)                    | 返回str重复n次的结果                                         |
| SPACE(n)                          | 返回n个空格                                                  |
| STRCMP(s1,s2)                     | 比较字符串s1,s2的ASCII码值的大小                             |
| SUBSTR(s,index,len)               | 返回从字符串s的index位置其len个字符，作用与SUBSTRING(s,n,len)、MID(s,n,len)相同 |
| LOCATE(substr,str)                | 返回字符串substr在字符串str中首次出现的位置，作用于POSITION(substr IN str)、INSTR(str,substr)相同。未找到，返回0 |
| ELT(m,s1,s2,…,sn)                 | 返回指定位置的字符串，如果m=1，则返回s1，如果m=2，则返回s2，如果m=n，则返回sn |
| FIELD(s,s1,s2,…,sn)               | 返回字符串s在字符串列表中第一次出现的位置                    |
| FIND_IN_SET(s1,s2)                | 返回字符串s1在字符串s2中出现的位置。其中，字符串s2是一个以逗号分隔的字符串 |
| REVERSE(s)                        | 返回s反转后的字符串                                          |
| NULLIF(value1,value2)             | 比较两个字符串，如果value1与value2相等，则返回NULL，否则返回value1 |

> 注意：MySQL中，字符串的位置是从1开始的。

举例：

```mysql
mysql> SELECT FIELD('mm','hello','msm','amma'),FIND_IN_SET('mm','hello,mm,amma')
    -> FROM DUAL;
+----------------------------------+-----------------------------------+
| FIELD('mm','hello','msm','amma') | FIND_IN_SET('mm','hello,mm,amma') |
+----------------------------------+-----------------------------------+
|                                0 |                                 2 |
+----------------------------------+-----------------------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT NULLIF('mysql','mysql'),NULLIF('mysql', '');
+-------------------------+---------------------+
| NULLIF('mysql','mysql') | NULLIF('mysql', '') |
+-------------------------+---------------------+
| NULL                    | mysql               |
+-------------------------+---------------------+
1 row in set (0.00 sec)
```



### 13.5 日期和时间函数

#### 13.5.1 获取日期、时间

| 函数                                                         | 用法                           |
| ------------------------------------------------------------ | ------------------------------ |
| **CURDATE()** ，CURRENT_DATE()                               | 返回当前日期，只包含年、月、日 |
| **CURTIME()** ， CURRENT_TIME()                              | 返回当前时间，只包含时、分、秒 |
| **NOW()** / SYSDATE() / CURRENT_TIMESTAMP() / LOCALTIME() / LOCALTIMESTAMP() | 返回当前系统日期和时间         |
| UTC_DATE()                                                   | 返回UTC（世界标准时间）日期    |
| UTC_TIME()                                                   | 返回UTC（世界标准时间）时间    |

举例：

```mysql
SELECT CURDATE(),CURTIME(),NOW(),SYSDATE()+0,UTC_DATE(),UTC_DATE()+0,UTC_TIME(),UTC_TIME()+0
FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227153603.png)



#### 13.5.2 日期与时间戳的转换

| 函数                     | 用法                                                         |
| ------------------------ | ------------------------------------------------------------ |
| UNIX_TIMESTAMP()         | 以UNIX时间戳的形式返回当前时间。SELECT UNIX_TIMESTAMP() ->1634348884 |
| UNIX_TIMESTAMP(date)     | 将时间date以UNIX时间戳的形式返回。                           |
| FROM_UNIXTIME(timestamp) | 将UNIX时间戳的时间转换为普通格式的时间                       |

举例：

```mysql
mysql> SELECT UNIX_TIMESTAMP(now());
+-----------------------+
| UNIX_TIMESTAMP(now()) |
+-----------------------+
|            1576380910 |
+-----------------------+
1 row in set (0.01 sec)

mysql> SELECT UNIX_TIMESTAMP(CURDATE());
+---------------------------+
| UNIX_TIMESTAMP(CURDATE()) |
+---------------------------+
|                1576339200 |
+---------------------------+
1 row in set (0.00 sec)

mysql> SELECT UNIX_TIMESTAMP(CURTIME());
+---------------------------+
| UNIX_TIMESTAMP(CURTIME()) |
+---------------------------+
|                1576380969 |
+---------------------------+
1 row in set (0.00 sec)

mysql> SELECT UNIX_TIMESTAMP('2011-11-11 11:11:11')
+---------------------------------------+
| UNIX_TIMESTAMP('2011-11-11 11:11:11') |
+---------------------------------------+
|                            1320981071 |
+---------------------------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT FROM_UNIXTIME(1576380910);
+---------------------------+
| FROM_UNIXTIME(1576380910) |
+---------------------------+
| 2019-12-15 11:35:10       |
+---------------------------+
1 row in set (0.00 sec)
```



#### 13.5.3 获取月份、星期、星期数、天数等函数

| 函数                                     | 用法                                            |
| ---------------------------------------- | ----------------------------------------------- |
| YEAR(date) / MONTH(date) / DAY(date)     | 返回具体的日期值                                |
| HOUR(time) / MINUTE(time) / SECOND(time) | 返回具体的时间值                                |
| MONTHNAME(date)                          | 返回月份：January，...                          |
| DAYNAME(date)                            | 返回星期几：MONDAY，TUESDAY.....SUNDAY          |
| WEEKDAY(date)                            | 返回周几，注意，周1是0，周2是1，。。。周日是6   |
| QUARTER(date)                            | 返回日期对应的季度，范围为1～4                  |
| WEEK(date) ， WEEKOFYEAR(date)           | 返回一年中的第几周                              |
| DAYOFYEAR(date)                          | 返回日期是一年中的第几天                        |
| DAYOFMONTH(date)                         | 返回日期位于所在月份的第几天                    |
| DAYOFWEEK(date)                          | 返回周几，注意：周日是1，周一是2，。。。周六是7 |

举例：

```mysql
SELECT YEAR(CURDATE()),MONTH(CURDATE()),DAY(CURDATE()),
HOUR(CURTIME()),MINUTE(NOW()),SECOND(SYSDATE())
FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227153851.png)

```mysql
SELECT MONTHNAME('2021-10-26'),DAYNAME('2021-10-26'),WEEKDAY('2021-10-26'),
QUARTER(CURDATE()),WEEK(CURDATE()),DAYOFYEAR(NOW()),
DAYOFMONTH(NOW()),DAYOFWEEK(NOW())
FROM DUAL;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227153934.png)



#### 13.5.4 日期的操作函数

| 函数                    | 用法                                       |
| ----------------------- | ------------------------------------------ |
| EXTRACT(type FROM date) | 返回指定日期中特定的部分，type指定返回的值 |

**EXTRACT(type FROM date)函数中type的取值与含义：**

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227154053.png)

```mysql
SELECT EXTRACT(MINUTE FROM NOW()),EXTRACT( WEEK FROM NOW()),
EXTRACT( QUARTER FROM NOW()),EXTRACT( MINUTE_SECOND FROM NOW())
FROM DUAL;
```

#### 13.5.5 时间和秒钟转换的函数

| 函数                 | 用法                                                         |
| -------------------- | ------------------------------------------------------------ |
| TIME_TO_SEC(time)    | 将 time 转化为秒并返回结果值。转化的公式为：`小时*3600+分钟*60+秒` |
| SEC_TO_TIME(seconds) | 将 seconds 描述转化为包含小时、分钟和秒的时间                |

举例：

```mysql
mysql> SELECT TIME_TO_SEC(NOW());
+--------------------+
| TIME_TO_SEC(NOW()) |
+--------------------+
|               78774 |
+--------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT SEC_TO_TIME(78774);
+--------------------+
| SEC_TO_TIME(78774) |
+--------------------+
| 21:52:54            |
+--------------------+
1 row in set (0.12 sec)
```



#### 13.5.6 计算日期和时间的函数

**第1组：**

| 函数                                                         | 用法                                           |
| ------------------------------------------------------------ | ---------------------------------------------- |
| DATE_ADD(datetime, INTERVAL  expr type)，ADDDATE(date,INTERVAL expr type) | 返回与给定日期时间相差INTERVAL时间段的日期时间 |
| DATE_SUB(date,INTERVAL expr type)，SUBDATE(date,INTERVAL expr type) | 返回与date相差INTERVAL时间间隔的日期           |

**上述函数中type的取值：**

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20211227154310.png)

举例：

```mysql
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY) AS col1,DATE_ADD('2021-10-21 23:32:12',INTERVAL 1 SECOND) AS col2,
ADDDATE('2021-10-21 23:32:12',INTERVAL 1 SECOND) AS col3,
DATE_ADD('2021-10-21 23:32:12',INTERVAL '1_1' MINUTE_SECOND) AS col4,
DATE_ADD(NOW(), INTERVAL -1 YEAR) AS col5, #可以是负数
DATE_ADD(NOW(), INTERVAL '1_1' YEAR_MONTH) AS col6 #需要单引号
FROM DUAL;
```

![image-20220105154614077](https://gitee.com/Amazjing/markdown-img/raw/master/img/image-20220105154614077.png)



```mysql
SELECT DATE_SUB('2021-01-21',INTERVAL 31 DAY) AS col1,
SUBDATE('2021-01-21',INTERVAL 31 DAY) AS col2,
DATE_SUB('2021-01-21 02:01:01',INTERVAL '1 1' DAY_HOUR) AS col3
FROM DUAL;
```

**第2组：**

| 函数                         | 用法                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| ADDTIME(time1,time2)         | 返回time1加上time2的时间。当time2为一个数字时，代表的是`秒`，可以为负数 |
| SUBTIME(time1,time2)         | 返回time1减去time2后的时间。当time2为一个数字时，代表的是`秒`，可以为负数 |
| DATEDIFF(date1,date2)        | 返回date1 - date2的日期间隔天数                              |
| TIMEDIFF(time1, time2)       | 返回time1 - time2的时间间隔                                  |
| FROM_DAYS(N)                 | 返回从0000年1月1日起，N天以后的日期                          |
| TO_DAYS(date)                | 返回日期date距离0000年1月1日的天数                           |
| LAST_DAY(date)               | 返回date所在月份的最后一天的日期                             |
| MAKEDATE(year,n)             | 针对给定年份与所在年份中的天数返回一个日期                   |
| MAKETIME(hour,minute,second) | 将给定的小时、分钟和秒组合成时间并返回                       |
| PERIOD_ADD(time,n)           | 返回time加上n后的时间                                        |

举例：

```mysql
SELECT ADDTIME(NOW(),20),SUBTIME(NOW(),30),SUBTIME(NOW(),'1:1:3'),DATEDIFF(NOW(),'2021-10-01'),
TIMEDIFF(NOW(),'2021-10-25 22:10:10'),FROM_DAYS(366),TO_DAYS('0000-12-25'),
LAST_DAY(NOW()),MAKEDATE(YEAR(NOW()),12),MAKETIME(10,21,23),PERIOD_ADD(20200101010101,10)
FROM DUAL;
```

```mysql
mysql> SELECT ADDTIME(NOW(), 50);
+---------------------+
| ADDTIME(NOW(), 50)  |
+---------------------+
| 2019-12-15 22:17:47 |
+---------------------+
1 row in set (0.00 sec)

mysql> SELECT ADDTIME(NOW(), '1:1:1');
+-------------------------+
| ADDTIME(NOW(), '1:1:1') |
+-------------------------+
| 2019-12-15 23:18:46     |
+-------------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT SUBTIME(NOW(), '1:1:1');
+-------------------------+
| SUBTIME(NOW(), '1:1:1') |
+-------------------------+
| 2019-12-15 21:23:50     |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT SUBTIME(NOW(), '-1:-1:-1'); 
+----------------------------+
| SUBTIME(NOW(), '-1:-1:-1') |
+----------------------------+
| 2019-12-15 22:25:11        |
+----------------------------+
1 row in set, 1 warning (0.00 sec)
```

```mysql
mysql> SELECT FROM_DAYS(366);
+----------------+
| FROM_DAYS(366) |
+----------------+
| 0001-01-01     |
+----------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT MAKEDATE(2020,1);
+------------------+
| MAKEDATE(2020,1) |
+------------------+
| 2020-01-01       |
+------------------+
1 row in set (0.00 sec)

mysql> SELECT MAKEDATE(2020,32);
+-------------------+
| MAKEDATE(2020,32) |
+-------------------+
| 2020-02-01        |
+-------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT MAKETIME(1,1,1);
+-----------------+
| MAKETIME(1,1,1) |
+-----------------+
| 01:01:01        |
+-----------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT PERIOD_ADD(20200101010101,1);
+------------------------------+
| PERIOD_ADD(20200101010101,1) |
+------------------------------+
|               20200101010102 |
+------------------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT TO_DAYS(NOW());
+----------------+
| TO_DAYS(NOW()) |
+----------------+
|          737773 |
+----------------+
1 row in set (0.00 sec)
```

举例：查询 7 天内的新增用户数有多少？

```mysql
SELECT COUNT(*) as num FROM new_user WHERE TO_DAYS(NOW())-TO_DAYS(regist_time)<=7
```



#### 13.5.7 日期的格式化与解析

| 函数                              | 用法                                       |
| --------------------------------- | ------------------------------------------ |
| DATE_FORMAT(date,fmt)             | 按照字符串fmt格式化日期date值              |
| TIME_FORMAT(time,fmt)             | 按照字符串fmt格式化时间time值              |
| GET_FORMAT(date_type,format_type) | 返回日期字符串的显示格式                   |
| STR_TO_DATE(str, fmt)             | 按照字符串fmt对str进行解析，解析为一个日期 |

上述`非GET_FORMAT`函数中fmt参数常用的格式符：

| 格式符 | 说明                                                        | 格式符 | 说明                                                        |
| ------ | ----------------------------------------------------------- | ------ | ----------------------------------------------------------- |
| %Y     | 4位数字表示年份                                             | %y     | 表示两位数字表示年份                                        |
| %M     | 月名表示月份（January,....）                                | %m     | 两位数字表示月份（01,02,03。。。）                          |
| %b     | 缩写的月名（Jan.，Feb.，....）                              | %c     | 数字表示月份（1,2,3,...）                                   |
| %D     | 英文后缀表示月中的天数（1st,2nd,3rd,...）                   | %d     | 两位数字表示月中的天数(01,02...)                            |
| %e     | 数字形式表示月中的天数（1,2,3,4,5.....）                    |        |                                                             |
| %H     | 两位数字表示小数，24小时制（01,02..）                       | %h和%I | 两位数字表示小时，12小时制（01,02..）                       |
| %k     | 数字形式的小时，24小时制(1,2,3)                             | %l     | 数字形式表示小时，12小时制（1,2,3,4....）                   |
| %i     | 两位数字表示分钟（00,01,02）                                | %S和%s | 两位数字表示秒(00,01,02...)                                 |
| %W     | 一周中的星期名称（Sunday...）                               | %a     | 一周中的星期缩写（Sun.，Mon.,Tues.，..）                    |
| %w     | 以数字表示周中的天数(0=Sunday,1=Monday....)                 |        |                                                             |
| %j     | 以3位数字表示年中的天数(001,002...)                         | %U     | 以数字表示年中的第几周，（1,2,3。。）其中Sunday为周中第一天 |
| %u     | 以数字表示年中的第几周，（1,2,3。。）其中Monday为周中第一天 |        |                                                             |
| %T     | 24小时制                                                    | %r     | 12小时制                                                    |
| %p     | AM或PM                                                      | %%     | 表示%                                                       |

GET_FORMAT函数中date_type和format_type参数取值如下：

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220105163727.png)

举例：

```mysql
#格式化
SELECT DATE_FORMAT(CURRENT_DATE(),'%Y-%M-%D'),
DATE_FORMAT(NOW(),'%Y-%m-%d'),TIME_FORMAT(CURTIME(),'%h:%i:%s'),
DATE_FORMAT(NOW(),'%Y-%M-%D %h:%i:%S  %W %w %T %r')
FROM DUAL

#解析：格式化的逆过程
SELECT STR_TO_DATE('2022-January-6th 08:11:36  Thursday 4','%Y-%M-%D %h:%i:%S  %W %w')
FROM DUAL
```



![](https://gitee.com/Amazjing/markdown-img/raw/master/img/微信截图_20220106200858.png)

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/微信截图_20220106201607.png)



```mysql
mysql> SELECT DATE_FORMAT(NOW(), '%H:%i:%s');
+--------------------------------+
| DATE_FORMAT(NOW(), '%H:%i:%s') |
+--------------------------------+
| 22:57:34                        |
+--------------------------------+
1 row in set (0.00 sec)
```

```mysql
SELECT STR_TO_DATE('09/01/2009','%m/%d/%Y')
FROM DUAL;

SELECT STR_TO_DATE('20140422154706','%Y%m%d%H%i%s')
FROM DUAL;

SELECT STR_TO_DATE('2014-04-22 15:47:06','%Y-%m-%d %H:%i:%s')
FROM DUAL;
```

```mysql
mysql> SELECT GET_FORMAT(DATE, 'USA');
+-------------------------+
| GET_FORMAT(DATE, 'USA') |
+-------------------------+
| %m.%d.%Y                |
+-------------------------+
1 row in set (0.00 sec)

SELECT DATE_FORMAT(NOW(),GET_FORMAT(DATE,'USA')),
FROM DUAL;
```

```mysql
mysql> SELECT STR_TO_DATE('2020-01-01 00:00:00','%Y-%m-%d'); 
+-----------------------------------------------+
| STR_TO_DATE('2020-01-01 00:00:00','%Y-%m-%d') |
+-----------------------------------------------+
| 2020-01-01                                    |
+-----------------------------------------------+
1 row in set, 1 warning (0.00 sec)
```



## 14. 流程控制函数

流程处理函数可以根据不同的条件，执行不同的处理流程，可以在SQL语句中实现不同的条件选择。MySQL中的流程处理函数主要包括IF()、IFNULL()和CASE()函数。

| 函数                                                         | 用法                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| IF(value,value1,value2)                                      | 如果value的值为TRUE，返回value1，否则返回value2 |
| IFNULL(value1, value2)                                       | 如果value1不为NULL，返回value1，否则返回value2  |
| CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2 .... [ELSE resultn] END | 相当于Java的if...else if...else...              |
| CASE  expr WHEN 常量值1 THEN 值1 WHEN 常量值1 THEN 值1 .... [ELSE 值n] END | 相当于Java的switch...case...                    |





```mysql
#流程控制函数
#14.1 IF(VALUE,VALUE1,VALUE2)
#如果value的值为TRUE，返回value1，否则返回value2

#salary大于6000的"details"列输出“高工资”，反之输出“低工资”
SELECT last_name,salary,
IF(salary >=6000,'高工资','低工资') "details"
FROM employees;

#commission_pct如果不为NULL,在"details"列，输出commission_pct的值；
#commission_pct如果为NULL,在"details"列，输出0
SELECT last_name,commission_pct,
IF(commission_pct IS NOT NULL,commission_pct,0) "details",
salary * 12 * (1 + IF(commission_pct IS NOT NULL,commission_pct,0)) "anunal_sal"
FROM employees;

#14.2 IF(VALUE1,VALUE2):看做是IF(VALUE,VALUE1,VALUE2)语句的特殊情况
#如果commission_pct不是NULL，在"details"列输出commission_pct字段的值；
#如果commission_pct是NULL，在"details"列输出0；
SELECT last_name,commission_pct,
IFNULL(commission_pct,0) "details"
FROM employees;


#14.3 CASE WHEN ... THEN ... WHEN ... THEN ... ELSE ... END
#类似于java的if ... else ... if ... else
#如果salary >= 15000，则“details”列输出'白骨精'；
#如果salary >= 10000，则“details”列输出'潜力股'；
#如果salary >= 8000，则“details”列输出'拼搏人'；
#其余的，则“details”列输出'普通群众'；
SELECT last_name,salary,
CASE WHEN salary >= 15000 THEN '白骨精'
		 WHEN salary >= 10000 THEN '潜力股'
		 WHEN salary >= 8000  THEN '拼搏人'
		 ELSE '普通群众' END "details"
FROM employees;

#14.4 CASE ... WHEN ... THEN ... WHEN ... THEN ... ELSE ... END
#类似于java的swich ... case
/*
练习1：
查询部门号为 10,20, 30 的员工信息, 若部门号为 10, 则打印其工资的 1.1 倍, 20 号部门, 则打印其工资的 1.2 倍, 30 号部门打印其工资的 1.3 倍数，其他部门，打印工资的1.4倍数
*/
SELECT employee_id,last_name,department_id,salary,
CASE department_id WHEN 10 THEN salary * 1.1
									 WHEN 20 THEN salary * 1.2
									 WHEN 30 THEN salary * 1.3
									 ELSE salary * 1.4 END "details"
FROM employees;									 

/*
练习2：
查询部门号为 10,20, 30 的员工信息, 若部门号为 10, 则打印其工资的 1.1 倍, 20 号部门, 则打印其工资的 1.2 倍, 30 号部门打印其工资的 1.3 倍数
*/
SELECT employee_id,last_name,department_id,salary,
CASE department_id WHEN 10 THEN salary * 1.1
									 WHEN 20 THEN salary * 1.2
									 WHEN 30 THEN salary * 1.3
									 END "details"
FROM employees
WHERE department_id IN(10,20,30);

```



```mysql
SELECT IF(1 > 0,'正确','错误')    
->正确
```

```mysql
SELECT IFNULL(null,'Hello Word')
->Hello Word
```

```mysql
SELECT CASE 
　　WHEN 1 > 0
　　THEN '1 > 0'
　　WHEN 2 > 0
　　THEN '2 > 0'
　　ELSE '3 > 0'
　　END
->1 > 0
```

```mysql
SELECT CASE 1 
　　WHEN 1 THEN '我是1'
　　WHEN 2 THEN '我是2'
ELSE '你是谁'
```

```mysql
SELECT employee_id,salary, CASE WHEN salary>=15000 THEN '高薪' 
				  WHEN salary>=10000 THEN '潜力股'  
				  WHEN salary>=8000 THEN '屌丝' 
				  ELSE '草根' END  "描述"
FROM employees; 
```

```mysql
SELECT oid,`status`, CASE `status` WHEN 1 THEN '未付款' 
								   WHEN 2 THEN '已付款' 
								   WHEN 3 THEN '已发货'  
								   WHEN 4 THEN '确认收货'  
								   ELSE '无效订单' END 
FROM t_order;
```

```mysql
mysql> SELECT CASE WHEN 1 > 0 THEN 'yes' WHEN 1 <= 0 THEN 'no' ELSE 'unknown' END;
+---------------------------------------------------------------------+
| CASE WHEN 1 > 0 THEN 'yes' WHEN 1 <= 0 THEN 'no' ELSE 'unknown' END |
+---------------------------------------------------------------------+
| yes                                                                  |
+---------------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CASE WHEN 1 < 0 THEN 'yes' WHEN 1 = 0 THEN 'no' ELSE 'unknown' END;  
+--------------------------------------------------------------------+
| CASE WHEN 1 < 0 THEN 'yes' WHEN 1 = 0 THEN 'no' ELSE 'unknown' END |
+--------------------------------------------------------------------+
| unknown                                                             |
+--------------------------------------------------------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT CASE 1 WHEN 0 THEN 0 WHEN 1 THEN 1 ELSE -1 END;
+------------------------------------------------+
| CASE 1 WHEN 0 THEN 0 WHEN 1 THEN 1 ELSE -1 END |
+------------------------------------------------+
|                                               1 |
+------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CASE -1 WHEN 0 THEN 0 WHEN 1 THEN 1 ELSE -1 END;
+-------------------------------------------------+
| CASE -1 WHEN 0 THEN 0 WHEN 1 THEN 1 ELSE -1 END |
+-------------------------------------------------+
|                                               -1 |
+-------------------------------------------------+
1 row in set (0.00 sec)
```

```mysql
SELECT employee_id,12 * salary * (1 + IFNULL(commission_pct,0))
FROM employees;
```

```mysql
SELECT last_name, job_id, salary,
       CASE job_id WHEN 'IT_PROG'  THEN  1.10*salary
                   WHEN 'ST_CLERK' THEN  1.15*salary
                   WHEN 'SA_REP'   THEN  1.20*salary
       			   ELSE      salary END     "REVISED_SALARY"
FROM   employees;
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/1554980865631.png)

练习：查询部门号为 10,20, 30 的员工信息, 若部门号为 10, 则打印其工资的 1.1 倍, 20 号部门, 则打印其工资的 1.2 倍, 30 号部门打印其工资的 1.3 倍数。



## 15. 加密与解密函数

加密与解密函数主要用于对数据库中的数据进行加密和解密处理，以防止数据被他人窃取。这些函数在保证数据库安全时非常有用。

| 函数                        | 用法                                                         |
| --------------------------- | ------------------------------------------------------------ |
| PASSWORD(str)               | 返回字符串str的加密版本，41位长的字符串。加密结果`不可逆`，常用于用户的密码加密 |
| MD5(str)                    | 返回字符串str的md5加密后的值，也是一种加密方式。若参数为NULL，则会返回NULL |
| SHA(str)                    | 从原明文密码str计算并返回加密后的密码字符串，当参数为NULL时，返回NULL。`SHA加密算法比MD5更加安全`。 |
| ENCODE(value,password_seed) | 返回使用password_seed作为加密密码加密value                   |
| DECODE(value,password_seed) | 返回使用password_seed作为加密密码解密value                   |

可以看到，ENCODE(value,password_seed)函数与DECODE(value,password_seed)函数互为反函数。

举例：

```mysql
mysql> SELECT PASSWORD('mysql'), PASSWORD(NULL);
+-------------------------------------------+----------------+
| PASSWORD('mysql')                         | PASSWORD(NULL) |
+-------------------------------------------+----------------+
| *E74858DB86EBA20BC33D0AECAE8A8108C56B17FA |                |
+-------------------------------------------+----------------+
1 row in set, 1 warning (0.00 sec)
```

```mysql
SELECT md5('123')
->202cb962ac59075b964b07152d234b70
```

```mysql
SELECT SHA('Tom123')
->c7c506980abc31cc390a2438c90861d0f1216d50
```

```mysql
mysql> SELECT ENCODE('mysql', 'mysql');
+--------------------------+
| ENCODE('mysql', 'mysql') |
+--------------------------+
| íg　¼　ìÉ                  |
+--------------------------+
1 row in set, 1 warning (0.01 sec)
```

```mysql
mysql> SELECT DECODE(ENCODE('mysql','mysql'),'mysql');
+-----------------------------------------+
| DECODE(ENCODE('mysql','mysql'),'mysql') |
+-----------------------------------------+
| mysql                                   |
+-----------------------------------------+
1 row in set, 2 warnings (0.00 sec)
```



## 16. MySQL信息函数

MySQL中内置了一些可以查询MySQL信息的函数，这些函数主要用于帮助数据库开发或运维人员更好地对数据库进行维护工作。

| 函数                                                  | 用法                                                     |
| ----------------------------------------------------- | -------------------------------------------------------- |
| VERSION()                                             | 返回当前MySQL的版本号                                    |
| CONNECTION_ID()                                       | 返回当前MySQL服务器的连接数                              |
| DATABASE()，SCHEMA()                                  | 返回MySQL命令行当前所在的数据库                          |
| USER()，CURRENT_USER()、SYSTEM_USER()，SESSION_USER() | 返回当前连接MySQL的用户名，返回结果格式为“主机名@用户名” |
| CHARSET(value)                                        | 返回字符串value自变量的字符集                            |
| COLLATION(value)                                      | 返回字符串value的比较规则                                |

举例：

```mysql
mysql> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)

mysql> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT USER(), CURRENT_USER(), SYSTEM_USER(),SESSION_USER();
+----------------+----------------+----------------+----------------+
| USER()         | CURRENT_USER() | SYSTEM_USER()  | SESSION_USER() |
+----------------+----------------+----------------+----------------+
| root@localhost | root@localhost | root@localhost | root@localhost |
+----------------+----------------+----------------+----------------+
```

```mysql
mysql> SELECT CHARSET('ABC');
+----------------+
| CHARSET('ABC') |
+----------------+
| utf8mb4        |
+----------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT COLLATION('ABC');
+--------------------+
| COLLATION('ABC')   |
+--------------------+
| utf8mb4_general_ci |
+--------------------+
1 row in set (0.00 sec)
```



## 17. 其他函数

MySQL中有些函数无法对其进行具体的分类，但是这些函数在MySQL的开发和运维过程中也是不容忽视的。

| 函数                           | 用法                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| FORMAT(value,n)                | 返回对数字value进行格式化后的结果数据。n表示`四舍五入`后保留到小数点后n位 |
| CONV(value,from,to)            | 将value的值进行不同进制之间的转换                            |
| INET_ATON(ipvalue)             | 将以点分隔的IP地址转化为一个数字                             |
| INET_NTOA(value)               | 将数字形式的IP地址转化为以点分隔的IP地址                     |
| BENCHMARK(n,expr)              | 将表达式expr重复执行n次。用于测试MySQL处理expr表达式所耗费的时间 |
| CONVERT(value USING char_code) | 将value所使用的字符编码修改为char_code                       |

举例：

```mysql
# 如果n的值小于或者等于0，则只保留整数部分
mysql> SELECT FORMAT(123.123, 2), FORMAT(123.523, 0), FORMAT(123.123, -2); 
+--------------------+--------------------+---------------------+
| FORMAT(123.123, 2) | FORMAT(123.523, 0) | FORMAT(123.123, -2) |
+--------------------+--------------------+---------------------+
| 123.12             | 124                | 123                 |
+--------------------+--------------------+---------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT CONV(16, 10, 2), CONV(8888,10,16), CONV(NULL, 10, 2);
+-----------------+------------------+-------------------+
| CONV(16, 10, 2) | CONV(8888,10,16) | CONV(NULL, 10, 2) |
+-----------------+------------------+-------------------+
| 10000           | 22B8             | NULL              |
+-----------------+------------------+-------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT INET_ATON('192.168.1.100');
+----------------------------+
| INET_ATON('192.168.1.100') |
+----------------------------+
|                 3232235876 |
+----------------------------+
1 row in set (0.00 sec)

# 以“192.168.1.100”为例，计算方式为192乘以256的3次方，加上168乘以256的2次方，加上1乘以256，再加上100。
```

```mysql
mysql> SELECT INET_NTOA(3232235876);
+-----------------------+
| INET_NTOA(3232235876) |
+-----------------------+
| 192.168.1.100         |
+-----------------------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT BENCHMARK(1, MD5('mysql'));
+----------------------------+
| BENCHMARK(1, MD5('mysql')) |
+----------------------------+
|                          0 |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT BENCHMARK(1000000, MD5('mysql')); 
+----------------------------------+
| BENCHMARK(1000000, MD5('mysql')) |
+----------------------------------+
|                                0 |
+----------------------------------+
1 row in set (0.20 sec)
```

```mysql
mysql> SELECT CHARSET('mysql'), CHARSET(CONVERT('mysql' USING 'utf8'));
+------------------+----------------------------------------+
| CHARSET('mysql') | CHARSET(CONVERT('mysql' USING 'utf8')) |
+------------------+----------------------------------------+
| utf8mb4          | utf8                                   |
+------------------+----------------------------------------+
1 row in set, 1 warning (0.00 sec)
```



## 18. 单行函数练习题

```mysql
# 1.显示系统时间(注：日期+时间) 
SELECT NOW(),SYSDATE(),CURRENT_TIMESTAMP(),LOCALTIME(),LOCALTIMESTAMP()
FROM DUAL;

# 2.查询员工号，姓名，工资，以及工资提高百分之20%后的结果（new salary） 
SELECT employee_id,last_name,salary,salary * 1.2 'new salary'
FROM employees;

# 3.将员工的姓名按首字母排序，并写出姓名的长度（length）
SELECT last_name,LENGTH(last_name) 'last_name_length'
FROM employees
ORDER BY last_name ASC;

# 4.查询员工id,last_name,salary，并作为一个列输出，别名为OUT_PUT
SELECT CONCAT(employee_id,last_name,salary) 'OUT_PUT'
FROM employees;

# 5.查询公司各员工工作的年数、工作的天数，并按工作年数的降序排序
SELECT last_name,DATEDIFF(CURDATE(),hire_date)/365 'worked_years',DATEDIFF(CURDATE(),hire_date) 'worked_days',TO_DAYS(CURDATE()) - TO_DAYS(hire_date) 'worked_days1'
FROM employees
ORDER BY worked_years DESC

# 6.查询员工姓名，hire_date , department_id，满足以下条件：雇用时间在 1997年之后，department_id 为80 或 90 或110, commission_pct不为空
SELECT last_name,hire_date,department_id
FROM employees
WHERE department_id IN (80,90,110)
AND commission_pct IS NOT NULL
#AND hire_date >= '1997-01-01';		存在隐式转换
#AND DATE_FORMAT(hire_date,'%Y-%m-%d') >= '1997-01-01';		#显式转换操作，格式化：日期---> 字符串
AND hire_date >= STR_TO_DATE('1997-01-01','%Y-%m-%d');		#显式转换操作，格式化：字符串---> 日期

# 7.查询公司中入职超过10000天的员工姓名、入职时间
SELECT last_name,hire_date
FROM employees
WHERE DATEDIFF(CURDATE(),hire_date) >= 10000;
```



## 19. 聚合函数

聚合（或聚集、分组）函数，它是对一组数据进行汇总的函数，输入的是一组数据的集合，输出的是单个值。



### 19.1 聚合函数介绍

- 什么是聚合函数

  聚合函数作用于一组数据，并对一组数据返回一个值。

  ![](https://gitee.com/Amazjing/markdown-img/raw/master/img/微信截图_20220113191821.png)



- 聚合函数类型

  - **AVG()** 
  - **SUM()**
  - **MAX()** 
  - **MIN()** 
  - **COUNT() **

- 聚合函数语法

  ![](https://gitee.com/Amazjing/markdown-img/raw/master/img/微信截图_20220113192002.png)



- 聚合函数不能嵌套调用。比如不能出现类似“AVG(SUM(字段名称))”形式的调用。



#### 19.1.1 AVG和SUM函数

可以对**数值型数据**使用AVG 和 SUM 函数。

AVG：平均值

SUM ：总和

```mysql
SELECT AVG(salary), MAX(salary),MIN(salary), SUM(salary)
FROM   employees
WHERE  job_id LIKE '%REP%';
```



#### 19.1.2 MIN和MAX函数

可以对**任意数据类型**的数据使用 MIN 和 MAX 函数。

```mysql
SELECT MIN(hire_date), MAX(hire_date)
FROM employees;
```



#### 19.1.3 COUNT函数

- COUNT(*)返回表中记录总数，适用于**任意数据类型**。

  ```mysql
  SELECT COUNT(*)
  FROM employees
  WHERE department_id = 50;
  ```

- COUNT(expr) 返回**expr不为空**的记录总数。

  ```mysql
  SELECT COUNT(commission_pct)
  FROM employees
  WHERE department_id = 50;
  ```

- **问题：用count(*)，count(1)，count(列名)谁好呢?**

  其实，对于MyISAM引擎的表是没有区别的。这种引擎内部有一计数器在维护着行数。

  Innodb引擎的表用count(*),count(1)直接读行数，复杂度是O(n)，因为innodb真的要去数一遍。但好于具体的count(列名)。

- 问题：**能不能使用count(列名)替换count(*)?**

  不要使用 count(列名)来替代 `count(*)`，`count(*)`是 SQL92 定义的标准统计行数的语法，跟数据库无关，跟 NULL 和非 NULL 无关。 

  说明：count(*)会统计值为 NULL 的行，而 count(列名)不会统计此列为 NULL 值的行。



```mysql
#聚合函数
#1. 常见的聚合函数

#1.1 AVG /SUM	:只适应于数值类型的字段（或变量）
SELECT AVG(salary),SUM(salary)
FROM employees;
#如下的操作没有意义
SELECT SUM(last_name),AVG(last_name),SUM(hire_date)
FROM employees;

#1.2 MAX /MIN	:适用于数值类型、字符串类型、日期时间类型的字段（或变量）
SELECT MAX(salary),MIN(salary)
FROM employees;

SELECT MAX(last_name),MIN(last_name),MIN(hire_date)
FROM employees;


#1.3 COUNT:
#①作用：计算指定字段在查询结构中出现的个数
SELECT COUNT(employee_id),COUNT(salary),COUNT(2 * salary),COUNT(1),COUNT(2),COUNT(*)
FROM employees;
+--------------------+---------------+-------------------+----------+----------+----------+
| COUNT(employee_id) | COUNT(salary) | COUNT(2 * salary) | COUNT(1) | COUNT(2) | COUNT(*) |
+--------------------+---------------+-------------------+----------+----------+----------+
| 	 107             |  107          | 		  107        |   107	|	107	   |	107	  | 
+--------------------+---------------+-------------------+----------+----------+----------+

#如果计算表中有多少条记录，如何实现？
#方式1：COUNT(*)
#方式2：COUNT(1)
#方式3：COUNT(具体字段)	:不一定对！

#②注意：计算指定字段出现的个数时，是不计算NULL值的。
SELECT COUNT(commission_pct)
FROM employees;

SELECT commission_pct
FROM employees
WHERE commission_pct IS NOT NULL

#③ AVG = SUM / COUNT
SELECT AVG(salary),SUM(salary)/COUNT(salary),
AVG(commission_pct),SUM(commission_pct)/COUNT(commission_pct)
FROM employees;

#需求：查询公司中平均奖金率
#错误的
SELECT AVG(commission_pct)
FROM employees;

#正确的：
SELECT SUM(commission_pct) / COUNT(IFNULL(commission_pct,0)),
AVG(IFNULL(commission_pct,0))
FROM employees;

#如何需要统计表中的记录数，使用COUNT(*)、COUNT(1)、COUNT(具体字段) 哪个效率更高呢？
#如果使用的是MyISAM存储引擎，则三者效率相同，都是0（1）
#如果使用的是InnoDB存储引擎，则三者效率：COUNT(*) = COUNT(1) > COUNT(字段)
```



#### 19.1.4 GROUP BY

**在SELECT列表中所有未包含在组函数中的列都应该包含在 GROUP BY子句中**

**包含在 GROUP BY 子句中的列不必包含在SELECT 列表中**



#### 19.1.5 GROUP BY中使用WITH ROLLUP

使用`WITH ROLLUP`关键字之后，在所有查询出的分组记录之后增加一条记录，该记录计算查询出的所有记录的总和，即统计记录数量。

> 注意：
>
> 当使用ROLLUP时，不能同时使用ORDER BY子句进行结果排序，即ROLLUP和ORDER BY是互相排斥的。

```mysql
#2. GROUP BY 的使用
#需求：查询各个部门的平均工资，最高工资
SELECT employee_id,department_id,AVG(salary),SUM(salary)
FROM employees
GROUP BY department_id;

#需求：查询各个Job_id的平均工资
SELECT job_id,AVG(salary)
FROM employees
GROUP BY job_id;

#需求：查询各个department_id，job_id的平均工资
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY department_id,job_id;

#错误的！！！
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY department_id;
#结论1：SELECT中出现的非组函数的字段必须出现声明在GROUP BY中。反之，GROUP BY 声明的字段可以不出现在SELECT中。
#结论2：GOURP BY 声明在FROM后面，WHERE后面，ORDER BY前面，LIMIT前面。
#结论3：MySQL中GROUP BY使用WITH ROLLUP，当使用ROLLUP时，不能同时使用ORDER BY子句进行结果排序，即ROLLUP和ORDER BY是互相排斥的。

SELECT department_id,AVG(salary)
FROM employees
GROUP BY department_id
WITH ROLLUP

#需求：查询各个部门的平均工资，按照平均工资升序排列
SELECT department_id,AVG(salary) avg_sal
FROM employees
GROUP BY department_id
ORDER BY avg_sal ASC;
```



#### 19.1.6 HAVING的使用

##### 19.1.6.1 基本使用

**过滤分组：HAVING子句**

1. 行已经被分组。
2. 使用了聚合函数。
3. 满足HAVING 子句中条件的分组将被显示。
4. HAVING 不能单独使用，必须要跟 GROUP BY 一起使用。

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/1554981808091.png)



```mysql
#练习：查询各个部门中最高工资比10000高的部门信息
#错误的写法：
SELECT department_id,MAX(salary)
FROM employees
WHERE MAX(salary) > 10000
GROUP BY department_id;

#要求1：如果过滤条件中使用了聚合函数，则必须使用HAVING来替换WHERE。否则，报错。
#要求2：HAVING 必须声明在GROUP BY 的后面。
#正确的写法：
SELECT department_id,MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 10000;

#要求3：开发中，我们使用HAVING的前提是SQL中使用了 GROUP BY


#练习：查询部门id为10，20，30，40这四个部门中最高工资比10000高的部门信息
#方式1：推荐，执行效率高于方式2.
SELECT department_id,MAX(salary)
FROM employees
WHERE department_id IN (10,20,30,40)
GROUP BY department_id
HAVING MAX(salary) > 10000;

#方式2：
SELECT department_id,MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 10000 AND department_id IN (10,20,30,40);

#结论：当过滤条件中有聚合函数时，则此过滤条件必须声明在HAVING中。
#	  当过滤条件没有聚合函数时，则此过滤条件声明在WHERE中或HAVING中都可以。但是，建议大家声明在WHERE中。

/*
WHERE 与 HAVING 的对比
1.从使用范围上来讲，HAVING的适用范围更广。
2.如果过滤条件中没有聚合函数：这种情况下，WHERE的执行效率要高于HAVING
*/
```



##### 19.1.6.2 WHERE和HAVING的对比

**区别1：WHERE 可以直接使用表中的字段作为筛选条件，但不能使用分组中的计算函数作为筛选条件；HAVING 必须要与 GROUP BY 配合使用，可以把分组计算的函数和分组字段作为筛选条件。** 

这决定了，在需要对数据进行分组统计的时候，HAVING 可以完成 WHERE 不能完成的任务。这是因为，在查询语法结构中，WHERE 在 GROUP BY 之前，所以无法对分组结果进行筛选。HAVING 在 GROUP BY 之后，可以使用分组字段和分组中的计算函数，对分组的结果集进行筛选，这个功能是 WHERE 无法完成的。另外，WHERE排除的记录不再包括在分组中。

**区别2：如果需要通过连接从关联表中获取需要的数据，WHERE 是先筛选后连接，而 HAVING 是先连接后筛选。** 这一点，就决定了在关联查询中，WHERE 比 HAVING 更高效。因为 WHERE 可以先筛选，用一个筛选后的较小数据集和关联表进行连接，这样占用的资源比较少，执行效率也比较高。HAVING 则需要先把结果集准备好，也就是用未被筛选的数据集进行关联，然后对这个大的数据集进行筛选，这样占用的资源就比较多，执行效率也较低。 

小结如下：

|        | 优点                         | 缺点                                   |
| ------ | ---------------------------- | -------------------------------------- |
| WHERE  | 先筛选数据再关联，执行效率高 | 不能使用分组中的计算函数进行筛选       |
| HAVING | 可以使用分组中的计算函数     | 在最后的结果集中进行筛选，执行效率较低 |

**开发中的选择：**

WHERE 和 HAVING 也不是互相排斥的，我们可以在一个查询里面同时使用 WHERE 和 HAVING。包含分组统计函数的条件用 HAVING，普通条件用 WHERE。这样，我们就既利用了 WHERE 条件的高效快速，又发挥了 HAVING 可以使用包含分组统计函数的查询条件的优点。当数据量特别大的时候，运行效率会有很大的差别。



## 20. SELECT执行过程与原理

### 20.1 查询的结构

```mysql
#方式1：
SELECT ...,....,...
FROM ...,...,....
WHERE 多表的连接条件
AND 不包含组函数的过滤条件
GROUP BY ...,...
HAVING 包含组函数的过滤条件
ORDER BY ... ASC/DESC
LIMIT ...,...

#方式2：
SELECT ...,....,...
FROM ... JOIN ... 
ON 多表的连接条件
JOIN ...
ON ...
WHERE 不包含组函数的过滤条件
AND/OR 不包含组函数的过滤条件
GROUP BY ...,...
HAVING 包含组函数的过滤条件
ORDER BY ... ASC/DESC
LIMIT ...,...

#其中：
#（1）from：从哪些表中筛选
#（2）on：关联多表查询时，去除笛卡尔积
#（3）where：从表中筛选的条件
#（4）group by：分组依据
#（5）having：在统计结果中再次筛选
#（6）order by：排序
#（7）limit：分页
```



### 20.2 SELECT执行顺序

需要记住 SELECT 查询时的两个顺序：

**1. 关键字书写的顺序是不能颠倒的：**

```mysql
SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT...
```

**2.SELECT 语句的执行顺序**（在 MySQL 和 Oracle 中，SELECT 执行顺序基本相同）：

```mysql
FROM -> ON -> (LEFT/RIGHT JOIN) -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT
```

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/1566872301088.png)

![](https://gitee.com/Amazjing/markdown-img/raw/master/img/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20220125163659.png)

```mysql
/*

书写顺序：

SELECT...(存在聚合函数)
FROM...(查询哪张表)
(LEFT /RIGHT) JOIN...ON...多表的连接条件
WHERE...不包含聚合函数的过滤条件
GROUP BY...
HAVING...包含聚合函数的过滤条件
ORDER BY....（ASC/DESC）
LIMIT....
*/

```

执行顺序：

按照上图所示，先执行①，然后再执行②，最后执行③。其中①中从上向下依次执行。

比如你写了一个 SQL 语句，那么它的关键字顺序和执行顺序是下面这样的：

```mysql
SELECT DISTINCT player_id, player_name, count(*) as num # 顺序 5
FROM player JOIN team ON player.team_id = team.team_id # 顺序 1
WHERE height > 1.80 # 顺序 2
GROUP BY player.team_id # 顺序 3
HAVING num > 2 # 顺序 4
ORDER BY num DESC # 顺序 6
LIMIT 2 # 顺序 7
```

在 SELECT 语句执行这些步骤的时候，每个步骤都会产生一个`虚拟表`，然后将这个虚拟表传入下一个步骤中作为输入。需要注意的是，这些步骤隐含在 SQL 的执行过程中，对于我们来说是不可见的。



### 20.3 SQL 的执行原理

SELECT 是先执行 FROM 这一步的。在这个阶段，如果是多张表联查，还会经历下面的几个步骤：

1. 首先先通过 CROSS JOIN 求笛卡尔积，相当于得到虚拟表 vt（virtual table）1-1；
2. 通过 ON 进行筛选，在虚拟表 vt1-1 的基础上进行筛选，得到虚拟表 vt1-2；
3. 添加外部行。如果我们使用的是左连接、右链接或者全连接，就会涉及到外部行，也就是在虚拟表 vt1-2 的基础上增加外部行，得到虚拟表 vt1-3。

当然如果我们操作的是两张以上的表，还会重复上面的步骤，直到所有表都被处理完为止。这个过程得到是我们的原始数据。

当我们拿到了查询数据表的原始数据，也就是最终的虚拟表 `vt1`，就可以在此基础上再进行 `WHERE 阶段`。在这个阶段中，会根据 vt1 表的结果进行筛选过滤，得到虚拟表 `vt2`。

然后进入第三步和第四步，也就是 `GROUP 和 HAVING 阶段`。在这个阶段中，实际上是在虚拟表 vt2 的基础上进行分组和分组过滤，得到中间的虚拟表 `vt3` 和 `vt4`。

当我们完成了条件筛选部分之后，就可以筛选表中提取的字段，也就是进入到 `SELECT 和 DISTINCT 阶段`。

首先在 SELECT 阶段会提取想要的字段，然后在 DISTINCT 阶段过滤掉重复的行，分别得到中间的虚拟表 `vt5-1` 和 `vt5-2`。

当我们提取了想要的字段数据之后，就可以按照指定的字段进行排序，也就是 `ORDER BY 阶段`，得到虚拟表 `vt6`。

最后在 vt6 的基础上，取出指定行的记录，也就是 `LIMIT 阶段`，得到最终的结果，对应的是虚拟表 `vt7`。

当然我们在写 SELECT 语句的时候，不一定存在所有的关键字，相应的阶段就会省略。

同时因为 SQL 是一门类似英语的结构化查询语言，所以我们在写 SELECT 语句的时候，还要注意相应的关键字顺序，**所谓底层运行的原理，就是我们刚才讲到的执行顺序。**

