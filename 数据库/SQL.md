## SQL 概述

**SQL (Structured Query Language)** 是一种专门用来操作关系数据库的**结构化查询语言**，它既是一种数据定义语言 (DDL)，也是一种数据操作语言 (DML)，还包含数据控制语言 (DCL) 的功能。

### SQL 的主要特点

+ SQL 是高度**一体化**的语言，集 DDL、DML、DCL 于一身，用户只需掌握一种语言即可完成数据库的定义、操作和控制。
+ SQL 是一种**非过程化 (declarative)** 的语言，用户只需说明要获取什么数据，而不必说明如何获取数据。
+ SQL 采用**面向集合 (set-oriented)** 的操作方式，允许一次对一个或多个表进行操作，一次插入、删除、更新操作的对象也可以是元组的集合。
+ SQL 对**交互式**（自主型）与**嵌入式**（宿主型）两种使用方式提供统一的语法结构。
+ SQL 语言简洁，接近英语口语，因此易于学习、理解和使用。

### SQL 的体系结构

SQL 支持数据库的[[三级模式]]结构：
+ **内模式**由 SQL 存储文件、索引文件等组成；
+ **模式**由 SQL 基本表实现；
+ **外模式**由 SQL 基本表和视图实现。

**基本表 (base table)** 对应于一个关系，本身独立存在，是 SQL 数据库中数据实际存储的结构，每个基本表对应一个存储文件和若干个索引文件。

**视图 (view)** 是由一个或多个基本表通过查询操作形成的虚拟表，视图并不存储数据，而是仅在数据字典 (DD) 中存储视图的定义，其数据来自于基本表。

### SQL 的功能组成

SQL 的功能主要包括以下几个方面：
+ **数据定义 (data definition)**，即作为 DDL 的 SQL，用于定义 (`CREATE`)、删除 (`DROP`)、修改 (`ALTER`) 数据库模式、表、视图、索引等数据库对象。
	+ 定义、删除模式 `SCHEMA`
	+ 定义、删除、修改关系模式 `TABLE`
	+ 定义、删除视图 `VIEW`
	+ 定义、删除索引 `INDEX`
+ **数据查询 (data query)**，用于查询 (`SELECT`) 数据库中的数据。
+ **数据操作 (data manipulation)**，即作为 DML 的 SQL，用于插入 (`INSERT`)、删除 (`DELETE`)、修改 (`UPDATE`) 数据库中的数据。
+ **数据控制 (data control)**，即作为 DCL 的 SQL，用于用户访问权限的授予 (`GRANT`) 与回收 (`REVOKE`) 等。

### SQL 的语法结构

SQL 语句通常由**关键字 (keyword)**、**标识符 (identifier)**、**运算符 (operator)**、**分隔符 (delimiter)** 和**常量 (constant)** 等组成。SQL 关键字不区分大小写，但为了增强可读性，通常将关键字大写。

以下，约定：
+ 使用尖括号 `< >` 括起的表示**变量**；
+ 使用单方括号 `[ ]` 括起的表示**一组选项**，其使用 `|` 分隔的各项中必须选择一个；
+ 使用双方括号 `[[ ]]` 括起的表示**可选项**。

## SQL 数据定义

### 模式的定义与删除

#### 定义模式

SQL 使用 `CREATE SCHEMA` 语句定义模式：
```sql
CREATE SCHEMA [[<schema_name>]] AUTHORIZATION <owner_name>;
```
其中，**`<schema_name>`** 是**模式名**，**`<owner_name>`** 是该模式所有者的**用户名**；如果省略 `<schema_name>`，则创建一个以所有者用户名命名的模式。

可以在定义模式的同时在该模式下[[#定义基本表]]、视图、索引等，如
```sql
CREATE SCHEMA [[<schema_name>]] AUTHORIZATION <owner_name>
	CREATE TABLE <table_name> (<table_definition>);
```
注意此处**模式定义末尾没有分号**；这等价于
```sql
CREATE SCHEMA [[<schema_name>]] AUTHORIZATION <owner_name>;
CREATE TABLE <schema_name>.<table_name> (<table_definition>);
```

#### 删除模式

使用 `DROP SCHEMA` 语句删除模式：
```sql
DROP SCHEMA <schema_name> [CASCADE | RESTRICT];
```
其中，`<schema_name>` 是要删除的模式名；**`CASCADE`** 和 **`RESTRICT`** 是两种删除模式的方式：
+ **`CASCADE` 级联删除**：删除模式时，同时删除该模式下的所有数据库对象（如表、视图、索引等）。
+ **`RESTRICT` 限制删除**：如果该模式下存在任何数据库对象，则拒绝删除该模式，只有先将模式下数据库对象删空后才能删除该模式。

### 基本表的定义、删除与修改

#### 定义基本表

使用 `CREATE TABLE` 语句定义基本表：
```sql
CREATE TABLE [[<schema_name>.]]<table_name> (
	<column_definition>[[, <table_constraint>]]
);
```
其中，
+ `<schema_name>` 是模式名，`<table_name>` 是表名；
+ **列定义 `<column_definition>`** 列出表的每个属性（列）的名称、数据类型及可选约束，每项格式为 
	```sql
	<column_name> <data_type> [[<column_constraint>]]
	```
	其中，`<column_name>` 是列名，`<data_type>` 是[[#^9a9ecc|数据类型]]，`<column_constraint>` 是列级完整性约束条件，包括：
	+ `NULL` 或 **`NOT NULL`**：指定该列是否允许存储空值；
	+ **`DEFAULT <default_value>`**：指定该列的默认值；
	+ `UNIQUE`：指定该列的值必须唯一；
	+ **`PRIMARY KEY`**：指定该列为**主键**，主键列的值必须唯一且不能为空；
	+ `CHECK (<search_condition>)`：指定该列的值必须满足的条件。
+ **表约束 `<table_constraint>`** 定义表级的完整性约束条件，包括：
	+ **`PRIMARY KEY (<column_list>)`**：指定多个列联合作为表的主键；
	+ `UNIQUE (<column_list>)`：指定多个列的值组合必须唯一；
	+ `FOREIGN KEY <column_list> REFERENCES [[<ref_schema_name>.]]<ref_table_name> [(<ref_column_list>)]`：指定一个或多个列作为外键，引用另一个表的主键或唯一键；
	+ `CHECK (<search_condition>)`：指定表中数据必须满足的条件。

SQL 支持的数据类型包括：
```tx
| 数据类型 || 说明 |
| :--- | :--- | :--- |
| 字符串 | `CHAR(n)` | 定长字符串，长度为 n 个字符 |
| ^^     | `VARCHAR(n)` | 变长字符串，最大长度为 n 个字符 |
| ^^     | `CLOB` | 大型字符对象，存储大量文本数据 |
| ^^     | `TEXT` | 可变长度字符串，适用于存储较长文本 |
| 二进制 | `BOOLEAN` 或 `BOOL` | 布尔值，取值为 TRUE 或 FALSE |
| ^^     | `BLOB` | 大型二进制对象，存储大量二进制数据 |
| 整型数 | `INTEGER` 或 `INT` | 4 字节整数 |
| ^^     | `SMALLINT` | 2 字节整数 |
| ^^     | `BIGINT` | 8 字节整数 |
| 浮点数 | `REAL` | 单精度浮点数 |
| ^^     | `DOUBLE PRECISION` | 双精度浮点数 |
| ^^     | `FLOAT(n)` | 精度为 n 位的浮点数 |
| ^^     | `DECIMAL(p, d)` | 定点数，p 为总位数，d 为小数位数 |\
|      | 或 `DEC(p, d)` |  |\
|      | 或 `NUMBER(p, d)` |  |
| 日期时间 | `DATE` | 日期，包括年、月、日，格式为 `YYYY-MM-DD` |
| ^^     | `TIME` | 时间，包括时、分、秒，格式为 `HH:MM:SS` |
| ^^     | `DATETIME` | 日期和时间的组合 |
| ^^     | `TIMESTAMP` | 时间戳，包含日期和时间，精确到秒或更高精度 |
| ^^     | `INTERVAL` | 时间间隔，用于表示两个时间点之间的差值 |
```
^9a9ecc

> [!example] 基本表定义示例
> 综合考虑数据库完整性，生成**学生选课数据库**的学生基本表 `S`、课程基本表 `C` 和选课基本表 `SC`。
> ```sql
> CREATE TABLE S (
> 	sNo CHAR(10) PRIMARY KEY,
> 	sName VARCHAR(50) NOT NULL,
> 	age SMALLINT NOT NULL CHECK (age >= 0),
> 	sex CHAR(1) NOT NULL CHECK (sex IN ('M', 'F')),
> 	sDept VARCHAR(50) NOT NULL
> );
> CREATE TABLE C (
> 	cNo CHAR(10) PRIMARY KEY,
> 	cName VARCHAR(100) NOT NULL,
> 	cPreNo CHAR(10) NULL, -- 允许为空，表示无先修课程
> 	FOREIGN KEY (cPreNo) REFERENCES C(cNo)
> );
> CREATE TABLE SC (
> 	sNo CHAR(10) NOT NULL,
> 	cNo CHAR(10) NOT NULL,
> 	grade DECIMAL(4,3) CHECK (grade >= 0 AND grade <= 4),
> 	PRIMARY KEY (sNo, cNo), -- 复合主键
> 	FOREIGN KEY (sNo) REFERENCES S(sNo),
> 	FOREIGN KEY (cNo) REFERENCES C(cNo)
> );
> ```

#### 修改基本表

#### 删除基本表

### 索引的建立、删除与更新

#### 建立索引

#### 更新索引

#### 删除索引

## SQL 数据查询

查询即检索操作，是对已经存在的基本表及视图进行数据检索，不改变数据本身。数据查询是数据库的核心操作。 SQL 使用 `SELECT` 语句进行数据查询：
```sql
SELECT [[DISTINCT | ALL]] <select_list>
	FROM <table_references>
	[[WHERE <search_condition>]]
	[[GROUP BY <group_by_list> [[HAVING <search_condition>]] ]]
	[[ORDER BY <order_by_list>]]
	[[LIMIT <limit_lines> [[OFFSET <offset_number>]] ]];
```
`SELECT` 语句具有灵活的使用方式和丰富强大的功能。

### 简单查询


### 连接查询


### 嵌套查询

**嵌套查询 (nested query)** 又称为**子查询 (subquery)**，是指在一个 SQL 查询语句中嵌套另一个 SQL 查询语句。嵌套查询通常用于需要多步查询才能得到结果的复杂查询。

> [!example] 简单的嵌套查询示例
> 求选修了《数据库》课程的学生的学号 `sNo` 和姓名 `sName`。
> 
> ```sql
> SELECT sNo, sName FROM S
> WHERE sNo IN (
> 	SELECT sNo FROM SC 
> 	WHERE cNo IN (
> 		SELECT cNo FROM C
> 		WHERE cName = '数据库'
> 	)
> );
> ```
^418cb9

这里，`IN` 谓词将子查询结果视为集合，执行**集合**运算；对子查询结果为单值的情形，也可使用比较运算符执行比较。

#### 相关嵌套查询

[[#^418cb9|上例]]中的子查询与主查询是**独立的**，即子查询的执行不依赖于主查询的处理，称为**不相关子查询 (non-correlated subquery)**。若子查询的执行依赖于主查询，则称为**相关子查询 (correlated subquery)**，整个查询语句称为**相关嵌套查询 (correlated nested query)**。

> [!example] 相关嵌套查询示例
> 查询每个学生**超过该学生自己平均成绩**的课程号 `cNo` 和成绩 `grade`。
> ```sql
> SELECT sNo, cNo, grade FROM SC x
> WHERE grade > (
> 	SELECT AVG(grade) FROM SC y
> 	WHERE x.sNo = y.sNo
> );
> ```

^d930b3

[[#^d930b3|上例]]中的子查询**依赖于主查询中当前处理的学生 `sNo`**，因此每处理一个学生，子查询就会执行一次。

#### 带有量词的嵌套查询

SQL 中可以使用**量词 (quantifier)** 来指定子查询结果与主查询条件的关系，从而允许**子查询返回多个元组**。常用的量词有：
+ **`ANY` (`SOME`)**：表示子查询结果中**至少有一个**值满足主查询条件，相当于在所有返回的元组之间加上逻辑「或」关系。
+ **`ALL`**：表示子查询结果中的**所有**值都满足主查询条件，相当于在所有返回的元组之间加上逻辑「且」关系。
+ **`EXISTS`**：表示子查询**至少返回一个元组**，用于检查子查询的条件是否能够成立。

> [!example] 带有量词 `ANY` 的嵌套查询示例
> 查询非电子系中比电子系某一个学生年龄小的学生学号 `sNo`、姓名 `sName`、年龄 `age`、系别 `sDept`。
> ```sql
> SELECT sNo, sName, age, sDept FROM S
> WHERE age < ANY (
> 	SELECT age FROM S
> 	WHERE sDept = '电子系'
> ) AND sDept <> '电子系';
> ```

> [!example] 带有量词 `ALL` 的嵌套查询示例
> 查询非电子系中比电子系所有学生年龄都小的学生学号 `sNo`、姓名 `sName`、年龄 `age`、系别 `sDept`。
> ```sql
> SELECT sNo, sName, age, sDept FROM S
> WHERE age < ALL (
> 	SELECT age FROM S
> 	WHERE sDept = '电子系'
> ) AND sDept <> '电子系';
> ```

> [!example] 带有量词 `EXISTS` 的嵌套查询示例
> 查询所有选修了《数据库》课程的学生学号 `sNo`、姓名 `sName`。
> ```sql
> SELECT sNo, sName FROM S
> WHERE EXISTS (
> 	SELECT * FROM SC
> 	WHERE S.sNo = SC.sNo AND SC.cNo = (
> 		SELECT cNo FROM C
> 		WHERE cName = '数据库'
> 	)
> );
> ```

一些带 `EXISTS` 或 `NOT EXISTS` 的子查询不能被其他形式的子查询等价替换，但其他形式的子查询通常都可以被等价地转换为带 `EXISTS` 或 `NOT EXISTS` 的子查询。尽管有意义的 `EXISTS` 子查询都是相关子查询，但其**只需返回是否存在元组的信息**，而不需要返回实际的元组数据，因此执行效率可能更高。

### 集合查询

`SELECT` 语句的结果是元组的集合，因此可以对多个 `SELECT` 语句的结果进行集合运算。SQL 支持以下几种集合运算：
+ **并 (UNION)**：返回两个查询结果的并集，结果中不包含重复元组。
+ **交 (INTERSECT)**：返回两个查询结果的交集。
+ **差 (EXCEPT)**：返回第一个查询结果中存在但第二个查询结果中不存在的元组。

参加集合操作的各查询结果必须具有**相同的列数**，且对应列的**数据类型必须兼容**。

### 派生查询

**派生表 (derived table)** 是指使用**子查询生成的临时表**作为 `FROM` 字句的数据源。派生表在查询执行过程中动态创建，并且只在该查询的生命周期内存在。

> [!example] 派生查询示例
> 同[[#^d930b3|相关嵌套查询示例]]，查询每个学生**超过该学生自己平均成绩**的课程号 `cNo` 和成绩 `grade`。
> ```sql
> SELECT sNo, cNo, grade 
> FROM SC, (
> 	SELECT sNo, AVG(grade) FROM SC
> 	GROUP BY sNo
> ) AS Avg_SC(avg_sNo, avg_grade)
> WHERE SC.sNo = Avg_SC.avg_sNo AND SC.grade > Avg_SC.avg_grade;
> ```

这种生成派生表的查询方式，有时可以提高查询效率，因为派生表只需计算一次，而相关子查询则可能需要为每个外层查询元组多次计算。

## SQL 数据更新

### 数据插入

使用 `INSERT INTO` 语句向基本表中插入一个元组，基本语法为
```sql
INSERT INTO [[<schema_name>.]]<table_name> [[(<column_list>)]]
	VALUES (<value_list>);
```
其中，
+ `<schema_name>` 是模式名，`<table_name>` 是表名；
+ `<column_list>` 是可选的列名列表，指定要插入值的列，若省略则表示为表的所有列；
+ `<value_list>` 是**与 `<column_list>` 中列对应**的值列表。

也可使用 `INSERT INTO ... SELECT` 语句从另一个表中插入多个元组，基本语法为
```sql
INSERT INTO [[<schema_name>.]]<table_name> [[(<column_list>)]]
	<select_query>;
```
其中，`<select_query>` 是一个 `SELECT` 查询语句，其结果集中的每个元组将被插入到指定的表中。

### 数据更新

使用 `UPDATE` 语句修改基本表中的数据，基本语法为
```sql
UPDATE [[<schema_name>.]]<table_name>
	SET <column_name> = <new_value> [[, <column_name> = <new_value> ...]]
	[[WHERE <search_condition>]];
```
其中，
+ `<schema_name>` 是模式名，`<table_name>` 是表名；
+ `<column_name>` 是要更新的列名，`<new_value>` 是该列的新值；
+ `<search_condition>` 是可选的搜索条件，指定要更新的元组范围，若省略则表示更新表中的所有元组。

### 数据删除

使用 `DELETE FROM` 语句删除基本表中的数据，基本语法为
```sql
DELETE FROM [[<schema_name>.]]<table_name>
	[[WHERE <search_condition>]];
```
其中，
+ `<schema_name>` 是模式名，`<table_name>` 是表名；
+ `<search_condition>` 是可选的搜索条件，指定要删除的元组范围，若省略则表示删除表中的所有元组。



