[toc]

### MySQL 创建数据表

创建 MySQL 数据表需要以下信息：

* 表名
* 表字段名
* 定义每个表字段

#### 语法

以下为创建 MySQL 数据表的 SQL 通用语法：

```mysql
CREATE TABLE table_name (column_name column_type);
```

以下例子中我们将在 RUNOOB 数据库中创建数据表 runoob_tbl：

```mysql
CREATE TABLE runoob_tbl(
	runoob_id INT NOT NULL AUTO_INCREMENT,
    runoob_title VARCHAR(100) NOT NULL,
    runoob_author VARCHAR(40) NOT NULL,
    submission_date DATE,
    PRIMARY KEY ( runoob_id )
    )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

**实例解析**：

* 如果你不想字段为 **NULL** 可以设置字段的属性为 **NOT NULL**，在操作数据库时如果输入该字段为 **NULL**，就会报错。
* AUTO_INCREMENT 定义列为自增的属性，一般用于主键，数值会自动加 1。
* PRIMARY KEY 关键字用于定义列为主键。您可以使用多列来定义主键，列间以逗号分隔。
* ENGINE 设置存储引擎，CHARSET 设置编码。

> **注意**：MySQL 命令终止符为分号 `;`。
>
> **注意**：`->` 是换行符标识。

### 删除数据表

MySQL 中删除数据表是非常容易操作的，但是你在进行删除表操作时要非常小心，因为执行删除命令后所有数据都会消失。

#### 语法

以下为删除 MySQL 数据表的通用语法：

```mysql
DROP TABLE table_name;
```

以下实例删除了数据表 runoob_tbl：

```mysql
DROP TABLE runoob_tbl
```

### MySQL 插入数据

MySQL 表中使用 **INSERT INTO** SQL 语句来插入数据。

#### 语法

以下为向 MySQL 数据表插入数据通用的 **INSERT INTO** SQL 语法：

```mysql
INSERT INTO table_name ( field1, field2, ... , fieldN)
						VALUES
						(value1, value2, ... , valueN);
```

如果数据是字符型，必须使用单引号或者双引号，如："value"。

#### 实例

以下实例中我们将向 runoob_tbl 表插入三条数据：

```mysql
INSERT INTO runoob_tbl
(runoob_title, runoob_author, submission_date)
VALUES
("Learn PHP", "RUNOOB", NOW());

INSERT INTO runoob_tbl
(runoob_title, runoob_author, submission_date)
VALUES
("Learn MySQL", "RUNOOB", NOW());

INSERT INTO runoob_tbl
(runoob_title, runoob_author, submission_date)
VALUES
("JAVA Course", "RUNOOB.COM", "2016-05-06");
```

> **注意**：在以上实例中，我们并没有提供 runoob_id 的数据，因为该字段我们在创建表的时候已经设置它为 AUTO_INCREMENT(自动增加) 属性。所以，该字段会自动递增而不需要我们去设置。
>
> 实例中的 NOW() 是一个 MySQL 函数，该函数返回日期和时间。

### MySQL 查询数据

MySQL 数据库使用 SQL SELECT 语句来查询数据。

#### 语法

以下为在 MySQL 数据库中查询数据通用的 SELECT 语法：

```mysql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][OFFSET M]
```

* 查询语句中你可以使用一个或者多个表，表之间使用逗号分隔，并使用 WHERE 语句来设定查询条件。
* SELECT 命令可以读取一条或者多条记录。
* 你可以使用星号来代替其他字段，SELECT 语句会返回表的所有字段数据
* 你可以使用 WHERE 语句来包含任何条件。
* 你可以使用 LIMIT 属性来设定返回的记录数。
* 你可以通过 OFFSET 指定 SELECT 语句开始查询的数据偏移量。默认情况下偏移量为 0。

以下实例将返回数据表 runoob_tbl 的所有记录：

```mysql
select * from runoob_tbl;
```

输出结果：

![G2n2nJ.png](https://s1.ax1x.com/2020/04/07/G2n2nJ.png)

### MySQL WHERE 子句

我们知道从 MySQL 表中使用 SQL SELECT 语句来读取数据。

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句中。

#### 语法

以下是 SQL SELECT 语句使用 WHERE 子句从数据表中读取数据地通用语法：

```mysql
SELECT field1, field2, ..., fieldN FROM table_name1, table_name2,...
[WHERE condition [AND [OR]] condition2 ......]
```

* 查询语句中你可以使用一个或者多个表，表之间使用逗号分隔，并使用 WHERE 语句来设定查询条件。
* 你可以在 WHERE 子句指定任何条件。
* 你可以使用 AND 或者 OR 指定一个或多个条件。
* WHERE 子句也可以运用于 SQL 的 DELETE 或者 UPDATE 命令。
* WHERE 子句类似于程序语言中的 if 条件，根据 MySQL 表中的字段值来读取指定的数据。

以下为操作符列表：

| 操作符 | 描述 |
| ------ | ---- |
| =      | 等号 |
| <>, != | 不等于|
|>       | 大于号|
|<       | 小于号|
|>=      | 大于等于号|
|<=      |小于等于号|

如果我们想在 MySQL 数据表中读取指定的数据，WHERE 子句是非常有用的。

使用主键来作为 WHERE 子句的条件查询是非常快速的。

如果给定的条件在表中没有任何匹配的记录，那么查询不会返回任何数据。

#### 实例

我们将在 SQL SELECT 语句使用 WHERE 子句来读取 MySQL 数据表 runoob_tbl 中的数据：

以下实例将读取 runoob_tbl 表中 runoob_author 字段值为 RUNOOB 的所有记录：

```mysql
SELECT * FROM runoob_tbl WHERE runoob_author="RUNOOB"
```

输出结果：

![G2Nu2d.png](https://s1.ax1x.com/2020/04/07/G2Nu2d.png)

MySQL 的 WHERE 子句的字符串比较是不区分大小写的。你可以使用 BINARY 关键字来设定 WHERE 子句的字符串比较是区分大小写的。

如下实例：

```mysql
SELECT * FROM runoob_tbl WHERE BINARY runoob_author="runoob.com";

SELECT * FROM runoob_tbl WHERE BINARY runoob_author="RUNOOB.COM";
```

结果如下：

![G2UiWQ.png](https://s1.ax1x.com/2020/04/07/G2UiWQ.png)

实例中使用了 BINARY 关键字，是区分大小写的，所以 runoob_author="runoob.com" 的查询条件是没有数据的。

### MySQL UPDATE 更新

如果我们需要修改或更新 MySQL 中的数据，我们可以使用 SQL UPDATE 命令来操作。

#### 语法

以下是 UPDATE 命令修改 MySQL 数据表数据的通用 SQL 语法：

```mysql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

* 你可以同时更新一个或多个字段。
* 你可以在 WHEERE 子句中指定任何条件。
* 你可以在一个单独表中同时更新数据。

当你需要更新数据表中指定行的数据时 WHERE 子句是非常有用的。

#### 实例

以下我们将在 SQL UPDATE 命令使用 WHERE 子句来更新 runoob_tbl 表中指定的数据：

以下实例将更新数据表中 runoob_id 为 3 的 runoob_title 字段值：

```mysql
UPDATE runoob_tbl SET runoob_title="Learn c++" WHERE runoob_id=3;

SELECT * FROM runoob_tbl WHERE runoob_id=3;
```

结果如下：

![G2acv9.png](https://s1.ax1x.com/2020/04/07/G2acv9.png)

从结果上看，runoob_id 为 3 的 runoob_title 已被修改。

### MySQL DELETE 语句

你可以使用 SQL 的 DELETE FROM 命令来删除 MySQL 数据表中的记录。

#### 语法

以下是 SQL DELETE 语句从 MySQL 数据表中删除数据的通用语法：

```mysql
DELETE FROM table_name [WHERE Clause]
```

* 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除。
* 你可以在 WHERE 子句中指定任何条件。
* 你可以在单个表中一次性删除记录。

当你想删除数据表中指定的记录时 WHERE 子句是非常有用的。

#### 实例

这里我们将在 SQL DELETE 命令中使用 WHERE 子句来删除 MySQL 数据表 runoob_tbl 所选的数据。

以下实例将删除 runoob_tbl 表中 runoob_id 为 3 的记录：

```mysql
DELETE FROM runoob_tbl WHERE runoob_id=3;
```

### MySQL LIKE 子句

我们知道在 MySQL 中使用 SQL DELECT 命令来读取数据，同时我们可以在 SELECT 语句中使用 WHERE 子句来获取指定的记录。

WHERE 子句中可以使用等号来设定获取的条件，如 `runoob_author="RUNOOB.COM"`。

但是有时候我们需要获取 runoob_author 字段中含有 "COM" 字符的所有记录，这时我们就需要在 WHERE子句中使用 SQL LIKE 子句。

SQL LIKE 子句中使用百分号字符来表示任意字符，类似于 UNIX 或正则表达式中的星号。

如果没有使用百分号，LIKE 子句与等号的效果是一样的。

#### 语法

以下是 SQL SELECT 语句使用 LIKE 子句从数据中读取数据的通用语法：

```mysql
SELECT field1, field2, ..., fieldN
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] field2 = 'somevalue'
```

* 你可以在 WHERE 子句中指定任何条件。
* 你可以在 WHERE 子句中使用 LIKE 子句。
* 你可以使用 LIKE 子句代替等号。
* LIKE 通常与 `%` 一同使用，类似于一个元字符的搜索。
* 你可以使用 AND 或者 OR 指定一个或多个条件。
* 你可以在 DELETE 或 UPDATE 命令中使用 WHERE ... LIKE 子句来指定条件。

#### 实例

以下我们将在 SQL SELECT 命令中使用 WHERE ... LIKE 子句来从 MySQL 数据表 runoob_tbl 中读取数据。

以下是我们将 runoob_tbl 表中获取 runoob_author 字段中以 COM 结尾的所有记录：

```mysql
SELECT * FROM runoob_tbl WHERE runoob_author LIKE '%COM';
```

结果如下：

![GRk24S.png](https://s1.ax1x.com/2020/04/08/GRk24S.png)

### MySQL UNION 操作符

MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。

#### 语法

MySQL UNION 操作符语法格式：

```mysql
SELECT expression1, expression2, ..., expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ..., expression_n
FROM tables
[WHERE conditions];
```

**参数**：

* **expression1, expression2, ..., expression_n**：要检索的列
* **tables**：要检索的数据表
* **WHERE conditions**：可选，检索条件
* **DISTINCT**：可选，删除结果集中重复的数据。默认情况下 UNION 操作符已经删除了重复数据，所以 DISTINCT 修饰符对结果没啥影响。
* **ALL**：可选，返回所有结果集，包含重复数据。

#### 实例

下面是选自 Websites 表的数据：

![GRAi4O.png](https://s1.ax1x.com/2020/04/08/GRAi4O.png)

下面是 apps 的数据：

![GRNk0P.png](https://s1.ax1x.com/2020/04/08/GRNk0P.png)

下面的 SQL 语句从 Websites 和 apps 表中选取所有不同的 country (只有不同的值)：

```mysql
SELECT country FROM Websites
UNION
SELECT country FROM apps
ORDER BY country;
```

结果如下：

![GRUNUf.png](https://s1.ax1x.com/2020/04/08/GRUNUf.png)

> **注释**：UNION 不能用于列出两个表中所有的 country。如果一些网站和 APP 来自同一个国家，每个国家只会列出一次。UNION 只会选取不同的值。请使用 UNION ALL 来选取重复的值！

下面的 SQL 语句使用 UNION ALL 从 Websites 和 apps 表中选取所有的 country (也有重复的值)：

```mysql
SELECT country FROM Websites
UNION ALL
SELECT country FROM apps
ORDER BY country;
```

结果如下：

![GRdvDA.png](https://s1.ax1x.com/2020/04/08/GRdvDA.png)

下面的 SQL 语句使用 UNION ALL 从 Websites 和 apps 表中选取所有的中国(CN)的数据(也有重复的值)：

```mysql
SELECT country, name FROM Websites
WHERE country='CN'
UNION ALL
SELECT country, app_name FROM apps
WHERE country='CN'
ORDER BY country;
```

结果如下：

![GRDpU1.png](https://s1.ax1x.com/2020/04/08/GRDpU1.png)

### MySQL 排序

我没知道从 MySQL 表中使用 SQL SELECT 语句来读取数据。

如果我们需要对读取的数据进行排序，我们就可以使用 MySQL 的 **ORDER BY** 子句来设定你想按哪个字段那种方式排序，在返回搜索结果。

#### 语法

以下是 SQL SELECT 语句使用 ORDER BY 子句将查询数据排序后再返回数据：

```mysql
SELECT field1, field2,...,fieldN FROM table_name1, table_name2...
ORDER BY field1 [ASE [DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]]
```

* 你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。
* 你可以设定多个字段来排序。
* 你可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。默认情况下，它是按升序排列。
* 你可以添加 WHERE ... LIKE 子句来设置条件。

#### 实例

以下将在 SQL SELECT 语句中使用 ORDER BY 子句来读取 MySQL 数据表 run00b_tbl 中的数据：

尝试以下实例，结果将按升序及降序排列。

```mysql
SELECT * FROM runoob_tbl ORDER BY submission_date ASC;
```

结果如下：

![GRxa2q.png](https://s1.ax1x.com/2020/04/08/GRxa2q.png)

```mysql
SELECT * FROM runoob_tbl ORDER BY submission_date DESC;
```

结果如下：

![GRxoZD.png](https://s1.ax1x.com/2020/04/08/GRxoZD.png)

### MySQL GROUP BY 语句

GROUP BY 语句根据一个或多个列对结果集进行分组。

在分组的列上我们可以使用 COUNT，SUM，AVG 等函数。

#### GROUP BY 语法

```mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```

#### 实例

先将以下数据导入数据库中：

```mysql
SET NAMES utf8;
SET FOREIGN_KEY_CHECKS = 0;

-- ---------------------------
--  Table structure for employee_tbl
-- ---------------------------
DROP TABLE IF EXISTS employee_tbl;
CREATE TABLE employee_tbl (
	id int(11) NOT NULL,
	name cahr(10) NOT NULL DEFAULT '',
    date datetime NOT NULL,
    singin tinyint(4) NOT NULL DEFAULT '0' COMMENT 'Logins',
    PRIMARY KEY (id)
    )ENGINE=InnoDB DEFAULT CHARSET=utf8;
    
-- ---------------------------
--  Records of employee_tbl
-- ---------------------------
BEGIN;
INSERT INTO empleyee_tbl VALUES ('1','XiaoMing','2016-04-22
15:25:33','1'),('2','XiaoWang','2016-04-20 15:25:47','3'),('3',
'XiaoLi', '2016-04-11 15:26:40', '2'), ('4','XiaoWang','2016-
04-07 15:26:14','4'),('5','XiaoMing','2016-04-11 15:26:40','4'),
('6','XiaoMing','2016-04-04 15:26:54','2');
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
```

导入成功后，执行以下 SQL 语句：

```mysql
SELECT * FROM employee_tbl;
```

结果如下：

![GW1dAg.png](https://s1.ax1x.com/2020/04/08/GW1dAg.png)

接下来我们使用 GROUP BY 语句将数据表按名字进行分组，并统计每个人有多少条记录：

```mysql
SELECT name, COUNT(*) FROM employee_tbl GROUP BY name;
```

结果如下：

![GfUADs.png](https://s1.ax1x.com/2020/04/08/GfUADs.png)

#### 使用 WITH ROLLUP

WITH ROLLUP 可以实现在分组统计数据基础上再进行相同的统计(SUM，AVG，COUNT，$\cdots\cdots$)。

例如我们将以上的数据表按名字进行分组，再统计每个人登录的次数：

```mysql
SELECT name, SUM(singin) as singin_count FROM employee_tbl
GROUP BY name WITH ROLLUP;
```

结果如下：

![GfaJyQ.png](https://s1.ax1x.com/2020/04/08/GfaJyQ.png)

其中记录 NULL 表示所有人的登录次数。

我们可以使用 coalesce 来设置一个可以取代 NULLL 的名称，coalesce 语法：

```mysql
SELECT coalesce(a,b,c);
```

**参数说明**：如果 a==null，则选择 b；如果 b == null，则选择 c；如果 a != null，则选择 a；如果 a，b，c 都为 null，则返回为 null(没意义)。

以下实例中如果名字为空我们使用总数代替：

```mysql
SELECT coalesce(name, 'SUM'), SUM(singin) as singin_count
FROM employee_tbl GROUP BY name WITH ROLLUP;
```

结果如下：

![Gfw4MD.png](https://s1.ax1x.com/2020/04/08/Gfw4MD.png)

### MySQL 连接的使用

在前面几章节中，我们已经学会了如何在一张表中读取数据，这是相对简单的，但是真正的应用中经常需要从多个数据表中读取数据。

本章节我们将向大家介绍如何使用 MySQL 的 JOIN 在两个或多个表中查询数据。

你可以在 SELECT，UPDATE 和 DELETE 语句中使用 MySQL 的 JOIN 来联合多表查询。

JOIN 按照功能大致分为如下三类：

* **INNER JOIN(内连接或等值连接)**：获取两个表中字段匹配关系的记录。
* **LEFT JOIN(左连接)**：获取左表所有记录，即使右表没有对应匹配的记录。
* **RIGHT JOIN(右连接)**：与 LEFT JOIN 相反，用于获取右表所有数据，即使左表没有对应匹配的记录

#### INNER JOIN

我们在 RUNOOB 数据库中有两张表 tcount_tbl 和 runoob_tbl。两张数据表数据如下：

![Gf6lYd.png](https://s1.ax1x.com/2020/04/08/Gf6lYd.png)

![Gfcuj0.png](https://s1.ax1x.com/2020/04/08/Gfcuj0.png)

接下来我们就使用 MySQL 的 INNER JOIN(也可以省略 INNER 使用 JOIN，效果一样)来连接以上两张表来读取 runoob_tbl 表中所有 runoob_author 字段在 tcount_tbl 表对应的 runoob_count 字段值：

```mysql
SELECT a.runoob_id, a.runoob_author, b.runoob_count
FROMM runoob_tbl a INNER JOIN tcount_tbl b
ON a.runoob_author = b.runoob_author;
```

结果如下：

![Gfg5sx.png](https://s1.ax1x.com/2020/04/08/Gfg5sx.png)

以上 SQL 语句等价于：

```mysql
SELECT a.runoob_id, a.runoob_author, b.runoob_count
FROM runoob_tbl a, runoob_tbl b
WHERE a.runoob_author = b.runoob_author;
```

![alt](https://www.runoob.com/wp-content/uploads/2014/03/img_innerjoin.gif)

#### MySQL LEFT JOIN

MySQL LEFT JOIN 与 JOIN 有所不同。MySQL LEFT JOIN 会读取左边数据表的全部数据，即便右边表无对应数据。

尝试以下实例，以 runoob_tbl 为左表，tcount_tbl 为右表，理解 MySQL LEFT JOIN 的应用：

```mysql
SELECT a.runoob_id, a.runoob_author, b.runoob_count
FROM runoob_tbl a LEFT JOIN tcount_tbl b
ON a.runoob_author = b.runoob_author;
```

结果如下：

![GfR5VK.png](https://s1.ax1x.com/2020/04/08/GfR5VK.png)

以上实例中使用了 LEFT JOIN，该语句会读取左边的数据表 runoob_tbl 的所有选取的字段数据，即便在右侧表 tcount_tbl 中没有对应的 runoob_author 字段值。

![alt](https://www.runoob.com/wp-content/uploads/2014/03/img_leftjoin.gif)

#### MySQL RIGHT JOIN

MySQL RIGHT JOIN 会读取右边数据表中的全部数据，即便左边边表无对应数据。

尝试以下实例，以 runoob_tbl 为左表，tcount_tbl 为右表，理解 MySQL RIGHT JOIN 的应用：

```mysql
SELECT a.runoob_id, a.runoob_author, b.runoob_count
FROM runoob_tbl a RIGHT JOIN tcount_tbl b
ON a.runoob_author = b.runoob_author;
```

结果如下：

![GfhG4O.png](https://s1.ax1x.com/2020/04/08/GfhG4O.png)

以上实例中使用了 RIGHT JOIN，该语句会读取右边的数据表 tcount_tbl 的所有选取的字段数据，即便左侧表 runoob_tbl 中没有对应的 runoob_author 字段值。

![alt](https://www.runoob.com/wp-content/uploads/2014/03/img_rightjoin.gif)

### MySQL NULL 值处理

我们已经知道 MySQL 使用 SQL SELECT 命令及 WHERE 子句来读取数据表中的数据，但是当提供的查询条件字段为 NULL 时，该命令可能就无法正常工作。

为了处理这种情况，MySQL 提供了三大运算符：

* **IS NULL**：当列的值是 NULL，此运算符返回 true。
* **IS NOT NULL**：当列的值不为 NULL，运算符返回 true。
* **<=>**：比较操作符(不同于 `=` 运算符)，当比较的两个值相等或者都为 NULL 时返回 true。

关于 NULL 的条件比较运算时比较特殊的。你不能使用 `=NULL` 或 `!=NULL` 在列中查找 NULL 值。

在 MySQL 中，NULL 值与任何其它值得比较(即使是 NULL)永远返回 NULL，即 NULL=NULL 返回 NULL。

MySQL 中处理 NULL 使用 IS NULL 和 IS NOT NULL 运算符。

#### 实例

以下实例中假设数据库 RUNOOB 中的表 runoob_test_tbl 含有两列 runoob_author 和 runoob_count，runoob_count 中设置插入 NULL 值。

**创建数据表 runoob_test_tbl**:

```mysql
mysql> CREATE TABLE runoob_test_tbl (
	-> runoob_author VARCHAR(40) NOT NULL,
    -> runoob_count INT
    -> );
mysql> INSERT INTO runoob_test_tbl (runoob_author, runoob_count) VALUES ('RUNOOB', 20);
mysql> INSERT INTO runoob_test_tbl (runoob_author, runoob_count) VALUES ('RUNOOB.COM', NULL);
mysql> INSERT INTO runoob_test_tbl (runoob_author, runoob_count) VALUES ('Google', NULL);
mysql> INSERT INTO runoob_test_tbl (runoob_author, runoob_count) VALUES ('FK', 20);
mysql> SELECT * FROM runoob_test_tbl;
```

以下实例中你可以看到 `=` 和 `!=` 运算符是不起作用的：

```mysql
mysql> SELECT * FROM runoob_test_tbl WHERE runoob_count = NULL;
Empty set (0.00 sec)
mysql> SELECT * FROM runoob_test_tbl WHERE runoob_count != NULL;
Empty set (0.00 sec)
```

查询数据表中 runoob_test_tbl 列是否为 NULL，必须使用 **IS NULL** 和 **IS NOT NULL**，如下实例：

![alt](C:\Users\Administrator\Pictures\Saved Pictures\LearnMySQl\ISNOTNULL.png)

### MySQL ALTER 命令

当我们需要修改数据表名或者修改数据表字段时，就需要使用到 MySQL ALTER 命令。

首先我们创建一张表，表名为：testalter_tbl：

```mysql
mysql> CREATE TABLE testalter_tbl (
	-> i INT,
	-> c CHAR(1)
	-> );
mysql> SHOW COLUMNS FROM testalter_tbl;
```

![表testalter_tbl](C:\Users\Administrator\Pictures\Saved Pictures\LearnMySQl\testalter_tbl.png)

#### 删除，添加或修改表字段

如下命令使用了 ALTER 命令及 DROP 子句来删除以上创建表的 i 字段：

```mysql
mysql> ALTER TABLE testalter_tbl DROP i;
```

如果数据表中只剩余一个字段则无法使用 DROP 来删除字段。

MySQL 中使用 ADD 子句来向数据表中添加列，如下实例在表 testalter_tbl 中添加 i 字段，并定义数据类型：

```mysql
mysql> ALTER TABLE testalter_tbl ADD i INT;
```

执行以上命令后，i 字段会自动添加到数据表字段的末尾。

如果你需要指定新增字段的位置，可以使用 MySQL 提供的关键字 FIRST (设定为第一列)，AFTER 字段名(设定位于某个字段之后)。

尝试以下 ALTER TABLE 语句，在执行成功后，使用 SHOW COLUMNS 查看表结构的变化：

```mysql
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD INT FIRST;
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD i INT AFTER c;
```

FIRST 和 AFTER 关键字可用于 ADD 与 MODIFY 子句，所以如果你想重置数据表字段的位置就需要先使用 DROP 删除字段然后使用 ADD 来添加字段并设置位置。

#### 修改字段类型及名称

如果需要修改字段类型及名称，你可以在 AFTER 命令中使用 MODIFY 或 CHANGE 子句。

例如，把字段 c 的类型从 CHAR(1) 改为 CHAR(10)，可以执行以下命令：

```mysql
ALTER TABLE testalter_tbl MODIFY c CHAR(10);
```

使用 CHANGE 子句，语法有很大的不同。在 CHANGE 关键字之后，紧跟着的是你要修改的字段名，然后指定新字段名及类型。尝试如下实例：

```mysql
ALTER TABLE testalter_tbl CHANGE i j BIGINT;
ALTER TABLE testalter_tbl CHANGE j j INT;
```

#### ALTER TABLE 对 NULL 值和默认值的影响

当你修改字段时，你可以指定是否包含值或者是否设置默认值。

以下实例，指定字段 j 为 NOT NULL 且默认值为 100.

```mysql
mysql> ALTER TABLE testalter_tbl
	-> MODIFY j BIGINT NOT NULL DEFAULT 100;
```

如果你不设置默认值，MySQL 会自动设置该字段为 NULL。

#### 修改字段默认值

你可以使用 ALTER 来修改字段的默认值，尝试以下实例：

```mysql
ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000;
```

你也可以使用 ALTER 命令及 DROP 子句来删除字段的默认值，如下实例：

```mysql
ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
```

修改数据表类型，可以使用 ALTER 命令及 TYPE 子句来完成。尝试以下实例，我们将表 testalter_tbl 的类型修改为 MYISAM：

> **注意**：查看数据表类型可以使用 SHOW TABLE STATUS 语句。

```mysql
mysql> ALTER TABLE testalter_tbl ENGINE = MYISAM;
mysql> SHOW TABLE STATUS LIKE 'testalter_tbl'\G
```

![查看数据表类型](https://i.loli.net/2020/04/10/pdnucIg6LxH1mbX.png)

#### 修改表名

如果需要修改数据表的名称，可以在 ALTER  TABLE 语句中使用 RENAME 子句来实现。

尝试以下实例将数据表 testalter_tbl 重命名为 alter_tbl：

```mysql
ALTER TABLE testalter_tbl RENAME TO alter_tbl;
```

ALTER 命令还可以用来创建及删除 MySQL 数据表的索引。

