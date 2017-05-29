# MySQL学习笔记

[TOC]

## 安装

```shell
sudo apt-get   install mysql-server mysql-client		#在终端输入mysql启动的是client,server作为系统服务在机器启动后自动加载（当然你也可以控制自动或者手动）
```

## 启动

```shell
sudo service mysql start
```

## 基本操作

在大多数系统中，SQL 语句都是不区分大小写的，但是出于严谨，而且便于区分保留字（保留字(reserved word)：指在高级语言中已经定义过的字，使用者不能再将这些字作为变量名或过程名使用。）和变量名，我们把保留字大写，把变量和数据小写。

### 登录

```shell
mysql -u root -p
```

### 查看信息

```mysql
SELECT VERSION(), CURRENT_DATE;		#版本号和当前日期
```

### 查看数据库

```mysql
SHOW DATABASES;
```

### 选择数据库

```mysql
USE [database_name];
```

### 查看表

```mysql
SHOW TABLES;
```

### 取消输入

```mysql
mysql> SELECT
    -> USER()
    -> \c
mysql>
```

### 退出

```mysql
quit(或者exit)
```

## 操作数据库

### 新建数据库

```mysql
CREATE DATABASE [database_name]		#新建后`show databases;`查询一下数据库
```

### 删除数据库

```mysql
DROP DATABASE mysql_shiyan;
```

### 加载数据库

```mysql
source [path/database_name.sql];
```

## 操作数据表

### 新建数据表

```mysql
CREATE TABLE 表的名字
(
列名a 数据类型(数据长度),
列名b 数据类型(数据长度)，
列名c 数据类型(数据长度)
);
```

数据类型

| 数据类型    | 大小（字节）  |    用途    |        格式         |
| :------ | :-----: | :------: | :---------------: |
| INT     |    4    |    整数    |                   |
| FLOAT   |    4    |  单精度浮点数  |                   |
| DOUBLE  |    8    |  双精度浮点数  |                   |
| ENUM    |         | 单选,比如性别  | ENUM('a','b','c') |
| SET     |         |    多选    | SET('1','2','3')  |
| DATE    |    3    |    日期    |    YYYY-MM-DD     |
| TIME    |    3    | 时间点或持续时间 |     HH:MM:SS      |
| YEAR    |    1    |   年份值    |       YYYY        |
| CHAR    |  0~255  |  定长字符串   |                   |
| VARCHAR |  0~255  |  变长字符串   |                   |
| TEXT    | 0~65535 |  长文本数据   |                   |

整数除了 INT 外，还有 TINYINT、SMALLINT、MEDIUMINT、BIGINT。

**CHAR 和 VARCHAR 的区别:** CHAR 的长度是固定的，而 VARCHAR 的长度是可以变化的，比如，存储字符串 “abc"，对于 CHAR(10)，表示存储的字符将占 10 个字节(包括 7 个空字符)，而同样的 VARCHAR(12) 则只占用4个字节的长度，`增加一个额外字节来存储字符串本身的长度`，12 只是最大值，当你存储的字符小于 12 时，按实际长度存储。

**ENUM和SET的区别:** ENUM 类型的数据的值，必须是定义时枚举的值的其中之一，即单选，而 SET 类型的值则可以多选。

### 描述数据表

```mysql
DESCRIBE [table_name];
```

### 查询数据

```mysql
SELECT * FROM [table_name];
```

### 插入数据

```mysql
INSERT INTO 表的名字(列名a,列名b,列名c) VALUES(值1,值2,值3);
```

```mysql
INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110);

INSERT INTO employee VALUES(02,'Jack',119119119);

INSERT INTO employee(id,name) VALUES(03,'Rose');
```

你已经注意到了，有的数据需要用单引号括起来，比如 Tom、Jack、Rose 的名字，这是由于它们的数据类型是 CHAR 型。此外 **VARCHAR,TEXT,DATE,TIME,ENUM** 等类型的数据也需要单引号修饰，而 **INT,FLOAT,DOUBLE** 等则不需要。

第一条语句比第二条语句多了一部分：`(id,name,phone)` 这个括号里列出的，是将要添加的数据 `(01,'Tom',110110110)` 其中每个值在表中对应的列。而第三条语句只添加了 `(id,name)` 两列的数据，**所以在表中Rose的phone为NULL**

### 约束

| 约束类型： | 主键          | 默认值     | 唯一     | 外键          | 非空       |
| ----- | ----------- | ------- | ------ | ----------- | -------- |
| 关键字：  | PRIMARY KEY | DEFAULT | UNIQUE | FOREIGN KEY | NOT NULL |

#### 主键

`PRIMARY KEY`

主键 (PRIMARY KEY)是用于约束表中的一行，作为这一行的唯一标识符，在一张表中通过主键就能准确定位到一行，因此主键十分重要。主键不能有重复且不能为空。

#### 默认值

`DEFAULT '[value]'`

默认值约束 (DEFAULT) 规定，当有 DEFAULT 约束的列，插入数据为空时，将使用默认值。

```mysql
# 正常插入数据
INSERT INTO department(dpt_name,people_num) VALUES('dpt1',11);

#插入新的数据，people_num 为空，使用默认值
INSERT INTO department(dpt_name) VALUES('dpt2');
```

#### 唯一

`UNIQUE`

唯一约束 (UNIQUE) 比较简单，它规定一张表中指定的一列的值必须不能有重复值，即这一列每个值都是唯一的。

#### 外键

`FOREIGN KEY`

外键 (FOREIGN KEY) 既能确保数据完整性，也能表现表之间的关系。一个表可以有多个外键，每个外键必须 REFERENCES (参考) 另一个表的主键，被外键约束的列，取值必须在它参考的列中有对应值。

#### 非空

`NOT NULL`

非空约束 (NOT NULL),听名字就能理解，被非空约束的列，在插入值时必须非空。

#### 自增

``AUTO_INCREMENT``

### SELECT 语句

```mysql
SELECT 要查询的列名 FROM 表名字 WHERE 限制条件;
SELECT * FROM 表名;	#查询表的所有内容
```

#### 数学符号

```mysql
SELECT name,age FROM employee WHERE age>25;
SELECT name,age,phone FROM employee WHERE name='Mary';
SELECT name,age FROM employee WHERE age<25 OR age>30;
SELECT name,age FROM employee WHERE age>25 AND age<30;
```

#### 逻辑符号

```mysql
SELECT name,age FROM employee WHERE age BETWEEN 25 AND 30;		#包含25和30这两个数字
SELECT name,age,phone,in_dpt FROM employee WHERE in_dpt IN ('dpt3','dpt4');
SELECT name,age,phone,in_dpt FROM employee WHERE in_dpt NOT IN ('dpt1','dpt3');
```

#### 通配符

```mysql
SELECT name,age,phone FROM employee WHERE phone LIKE '1101__';		#关键字 LIKE 在SQL语句中和通配符一起使用，通配符代表未知字符。SQL中的通配符是 _ 和 % 。其中 _ 代表一个未指定字符，% 代表不定个未指定字符。
```

#### 正则表达式

```mysql
SELECT * FROM [table_name] WHERE name REGEXP '[正则表达式]';
```

如果你想强制使`REGEXP`比较区分大小写，使用`BINARY`关键字使其中一个字符串变为二进制字符串。该查询只匹配名称首字母的小写`‘b’`

```mysql
mysql> SELECT * FROM pet WHERE name REGEXP BINARY '^b';
```

| 正则表达式   | 匹配结果   |
| ------- | ------ |
| `.`     | 任何单个字符 |
| `[abc]` | a或b或c  |
| `[a-z]` | 小写字母   |
| `[A-Z]` | 大写字母   |
| `[0-9]` | 数字     |
| `^`     | 开头     |
| `$`     | 结尾     |
| `{n}`   | 重复n次   |

#### 排序

为了使查询结果看起来更顺眼，我们可能需要对结果按某一列来排序，这就要用到 **ORDER BY** 排序关键词。默认情况下，**ORDER BY**的结果是**升序**排列，而使用关键词**ASC**和**DESC**可指定**升序**或**降序**排序。

```mysql
SELECT name,age,salary,phone FROM employee ORDER BY salary DESC;
```

#### 内置函数和计算

SQL 允许对表中的数据进行计算。对此，SQL 有 5 个内置函数，这些函数都对 SELECT 的结果做操作：

| 函数名： | COUNT | SUM  | AVG  | MAX  | MIN  |
| ---- | ----- | ---- | ---- | ---- | ---- |
| 作用：  | 计数    | 求和   | 求平均值 | 最大值  | 最小值  |

其中 COUNT 函数可用于任何数据类型(因为它只是计数)，而 SUM 、AVG 函数都只能对数字类数据类型做计算，MAX 和 MIN 可用于数值、字符串或是日期时间数据类型。

```mysql
SELECT COUNT(*) FROM pet;	#计算行数
SELECT MAX(salary) AS max_salary,MIN(salary) FROM employee;		#计算出salary的最大、最小值
```

#### 子查询

想要知道名为 "Tom" 的员工所在部门做了几个工程。员工信息储存在 employee 表中，但工程信息储存在project 表中。

```mysql
SELECT of_dpt,COUNT(proj_name) AS count_project FROM project
WHERE of_dpt IN
(SELECT in_dpt FROM employee WHERE name='Tom');
```

#### 连接查询

在处理多个表时，子查询只有在结果来自一个表时才有用。但如果需要显示两个表或多个表中的数据，这时就必须使用连接 **(join)** 操作。

```mysql
SELECT id,name,people_num
FROM employee,department
WHERE employee.in_dpt = department.dpt_name
ORDER BY id;
#查询各员工所在部门的人数，其中员工的 id 和 name 来自 employee 表，people_num 来自 department 表
```

上述语句等价于

```mysql
SELECT id,name,people_num
FROM employee JOIN department
ON employee.in_dpt = department.dpt_name
ORDER BY id;
```

### 重命名数据表

```mysql
RENAME TABLE 原名 TO 新名字;
ALTER TABLE 原名 RENAME 新名;
ALTER TABLE 原名 RENAME TO 新名;
```

### 删除数据表

```mysql
DROP TABLE 表名字;
```

### 修改列

#### 增加

```mysql
ALTER TABLE 表名字 ADD COLUMN 列名字 数据类型 约束;
或： ALTER TABLE 表名字 ADD 列名字 数据类型 约束;
ALTER TABLE employee ADD test INT(10) DEFAULT 11 FIRST;		#新增列放在第一列
ALTER TABLE employee ADD test INT(10) DEFAULT 11 AFTER age;		#新增列放在age之后
```

#### 删除

```mysql
ALTER TABLE 表名字 DROP COLUMN 列名字;
或： ALTER TABLE 表名字 DROP 列名字;
```

#### 重命名

```mysql
ALTER TABLE 表名字 CHANGE 原列名 新列名 数据类型 约束;
```

#### 改变数据类型

```mysql
ALTER TABLE 表名字 MODIFY 列名字 新数据类型;
```

### 修改表的内容

#### 修改某个值

```mysql
UPDATE 表名字 SET 列1=值1,列2=值2 WHERE 条件;
```

#### 删除一行记录

```mysql
DELETE FROM 表名字 WHERE 条件;
```

## 其他操作

### 索引

对一张表中的某个列建立索引，有以下两种语句格式：

```mysql
ALTER TABLE 表名字 ADD INDEX 索引名 (列名);
CREATE INDEX 索引名 ON 表名字 (列名);
```

我们用这两种语句分别建立索引：

```mysql
ALTER TABLE employee ADD INDEX idx_id (id);  #在employee表的id列上建立名为idx_id的索引
CREATE INDEX idx_name ON employee (name);   #在employee表的name列上建立名为idx_name的索引
```

### 视图

理解视图是虚拟的表：

- 数据库中只存放了视图的定义，而没有存放视图中的数据，这些数据存放在原来的表中；
- 使用视图查询数据时，数据库系统会从原来的表中取出对应的数据；
- 视图中的数据依赖于原来表中的数据，一旦表中数据发生改变，显示在视图中的数据也会发生改变；
- 在使用视图的时候，可以把它当作一张表。

创建视图的语句格式为：

```mysql
CREATE VIEW 视图名(列a,列b,列c) AS SELECT 列1,列2,列3 FROM 表名字;
```

可见创建视图的语句，后半句是一个SELECT查询语句，所以**视图也可以建立在多张表上**，只需在SELECT语句中使用**子查询**或**连接查询**

### 导入

导入操作，可以把一个文件里的数据保存进一张表。导入语句格式为：

```mysql
LOAD DATA INFILE '文件路径' INTO TABLE 表名字;
```

### 导出

```mysql
SELECT 列1，列2 INTO OUTFILE '文件路径和文件名' FROM 表名字;
```

```mysql
SELECT * INTO OUTFILE '/tmp/out.txt' FROM employee;		#把整个employee表的数据导出到 /tmp 目录下，导出文件命名为 out.txt
```

### 备份

备份与导出的区别：导出的文件只是保存数据库中的数据；而备份，则是把数据库的结构，包括数据、约束、索引、视图等全部另存为一个文件。备份与导出的区别：导出的文件只是保存数据库中的数据；而备份，则是把数据库的结构，包括数据、约束、索引、视图等全部另存为一个文件。

```mysql
mysqldump -u root -p 数据库名>备份文件名;   #备份整个数据库
mysqldump -u root -p 数据库名 表名字>备份文件名;  #备份整个表
```

```mysql
mysqldump -u root -p mysql_shiyan > bak.sql;		#备份整个数据库 mysql_shiyan并将备份文件命名为 bak.sql
```

### 恢复

```mysql
source /tmp/SQL6/MySQL-06.sql
```

```mysql
mysql -u root	#登录
CREATE DATABASE test;  #新建一个名为test的数据库，然后退出数据库
mysql -u root -p test < bak.sql
```

