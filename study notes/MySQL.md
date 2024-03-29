# MySQL

# 零、初始

1. 什么是数据库 database
2. 抛出问题，数据库的产生
1. 数据库萌芽阶段的发展历程
4. CRUD
5. 数据库架构

​			数据库的架构可以大致区分为三个概括层次：内层、概念层和外层。

- *内层*：最接近实际存储体，亦即有关资料的实际存储方式。
- *外层*：最接近用户，即有关个别用户观看资料的方式。
- *概念层*：介于两者之间的间接层。

6. **层次模型**

容易在一个系统中将相同的数据，因多种分类而储存多次。

```ascii
            ┌─────┐
            │     │
            └─────┘
               │
       ┌───────┴───────┐
       │               │
    ┌─────┐         ┌─────┐
    │     │         │     │
    └─────┘         └─────┘
       │               │
   ┌───┴───┐       ┌───┴───┐
   │       │       │       │
┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐
│     │ │     │ │     │ │     │
└─────┘ └─────┘ └─────┘ └─────┘
```

7. **网状模型**

- 允许一个以上的结点无双亲；
- 一个结点可以有多于一个的双亲。
- 容易造成数据结构冲突。（同一个文件可能有两个父节点）

```ascii
     ┌─────┐      ┌─────┐
   ┌─│     │──────│     │──┐
   │ └─────┘      └─────┘  │
   │    │            │     │
   │    └──────┬─────┘     │
   │           │           │
┌─────┐     ┌─────┐     ┌─────┐
│     │─────│     │─────│     │
└─────┘     └─────┘     └─────┘
   │           │           │
   │     ┌─────┴─────┐     │
   │     │           │     │
   │  ┌─────┐     ┌─────┐  │
   └──│     │─────│     │──┘
      └─────┘     └─────┘
```

8. 关系模型

- 数据之间分块管理，没有冲突
- 有公共字段

```ascii
┌─────┬─────┬─────┬─────┬─────┐
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┘
```



9. 企业和我们都选什么数据库呢？



------



# 一、安装、连接以及配置MySQL

1. windows两种安装方式，入门选手推荐第二种(win10演示)
2. 更改终端，放弃cmd作为主要终端，使用一流终端
1. MYSQL服务的启动与停止

- Windows

Turn on the MySQL server

```mysql
net start mysql
```

Turn off the MySQL server

```mysql
net stop mysql
```





4. 连接mysql

```mysql
mysql -u root -p // root is user's name; -p  -> password
```

```mysql
mysql -u root -p123456 // You can write password behind "-p";  not recommend
```



5. 退出mysql

```mysql
exit
```

```mysql
quit
```

```mysql
\q
```



6. 初始化data数据文件夹

```mysql
mysql --initialize-insecure --user=root
```

-  data file‘s   functions

1. The storage areas for the database.
2. store ibdatadatabases file.(ibdata file is the storage for the database's information.)



------

# 三、数据库的基本操作

1. 数据库的显示讲解

```mysql
 SHOW DATABASES;// Show all the databases on the server.
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)
```

Notice: `information_schema`、`mysql`、`performance_schema` and `sys` are  system databases.



2. 创建数据库

- common create method

```mysql
 CREATE database test;// test is database name;
Query OK, 1 row affected (0.00 sec)
```

- second : create database if not exists the same name database.

```mysql
CREATE DATABASE IF NOT EXISTS test;
```

- third:

```mysql
CREATE DATABASE IF NOT EXISTS `test`;
```

**notice: 创建数据库虽然不能命名为关键字，但可以用反引号括起来使用关键字命名数据库，但会抛出一个warning。**



3. 删除数据库

- common drop method

```mysql
DROP DATABASE test;// test is database name.
Query OK, 0 rows affected (0.01 sec)
```

- second:

```mysql
DROP DATABASE IF EXISTS test;
```



4. 查看创建的数据库的SQL

```mysql
SHOW CREATE DATABASE test;//test is the DATABASE name 查看创建数据库的SQL语句
+----------+--------------------------------------------------------------------------------------------------------------------------------+
| Database | Create Database
                    |
+----------+--------------------------------------------------------------------------------------------------------------------------------+
| test     | CREATE DATABASE test /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */ |
+----------+--------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```



6. 创建数据库指定字符编码以及查看字符编码

- The windows default charset is GBK, but we should use UTF8 or UTF8MB4 in development.
- notice:  MySQL version 8.0 and above versions use utf8mb4 as its default charset.

```mysql
CREATE DATABASE IF NOT EXISTS test CHARSET=GBK; 
```



7. **修改数据库字符编码**

```mysql
ALTER DATABASE test CHARSET=UTF8MB4; 
ALTER DATABASE bookdb DEFAULT CHARSET SET utf8mb4;
```





------
# 四、表的基本操作

1. 提出问题，引入“表“的概念与思维模式 table
2. 引用数据库和查看数据库中的表

- 引用数据库中的表

```mysql
USE test; // Change current database 
Database changed
```

- 查看数据库中的表

```mysql
SHOW TABLES;
```

- 修改表字符集

```mysql
ALTER TABLE table_name CONVERT TO CHARACTER SET utf8mb4;
```



3. 创建表

```mysql
 CREATE TABLE table(// table is TBALE name 
 id int,// first element
 name varchar(30),// second element
 age int// third element
 ); 
Query OK, 0 rows affected (0.01 sec)

```



4. 正规创建表

```mysql
CREATE TABLE IF NOT EXISTS students(
id INT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT 'primary_key',
name VARCHAR(30) NOT NULL COMMENT 'students name',
telephone VARCHAR(20) DEFAULT 'unknown' COMMENT 'telephone_number',
address VARCHAR(100) DEFAULT 'unknown' COMMENT 'students family address'
)ENGINE=InnoDB;
```

**notice：**

- not null:  This element shouldn't be null.
- auto_increment: increase number by itself.
- primary key: 主键。
- comment: 注释。
- default: 默认值。
- engine=innodb: database's engine.
- 注释中不能使用单引号。



5. 查看表结构

- first:

```mysql
DESC table;// table is the Table name.
```

- second:

```mysql
SHOW COLUMNS FROM i;// i is the table name.
```

6. check table status:

```mysql
SHOW TABLE STATUS LIKE 'table name'\G
```



6. 删除表

```mysql
DROP TABLE table;//table is the Table name.
Query OK, 0 rows affected (0.01 sec)
```

- notice: You can use “，“ to drop complex tables.


7. 修改表

- add field:

```mysql
ALTER TABLE 'table_name' ADD 'i' INT;   // i
```

```mysql
ALTER TABLE 'table_name' ADD 'i' INT FIRST;
```

```mysql
ALTER TABLE 'table_name' ADD 'i' INT AFTER 'c';// c is the column name.
```

- drop column:

```MYSQL
ALTER TABLE 'table_name' DROP 'i';
```

- change column type:

```mysql
ALTER TABLE 'table_name' MODIFY 'c' CHAR(10);
```

- change column name:

```mysql
ALTER TABLE 'table_name' CHANGE  'i' 'j' BIGINT;// i is the quondam name. j is the changed name.
```

```mysql
ALTER TABLE 'table_name' CHANGE  'j' 'j' INT; 
```

notice: The table name can be changed before and after to be consistent.

- To rename a table, use the **RENAME** option of the **ALTER TABLE** statement.

```mysql
ALTER TABLE table `quondam name` RENAME TO `changed name`;
```



**The Effect of ALTER TABLE on Null and Default Value Attributes**

When you MODIFY or CHANGE a column, you can also specify whether or not the column can contain NULL values and what its default value is. In fact, if you don't do this, MySQL automatically assigns values for these attributes and the value is Null.

- You can change a default value for any column by using the **ALTER** command.

```mysql
ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000; 
```

- You can remove the default constraint from any column by using DROP clause along with the **ALTER** command.

```mysql
ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
```



<!--not finished-->


------
# 五、数据操作

1. 插入数据

- first：

```mysql
INSERT INTO 'table_name' (feild1, field2, ...) VALUES (value1, value2, ...);
```

- second：

```mysql
INSERT INTO 'table_name' VALUES(value1, value2, value3,...);
```

notice: Character string should be bracketed into a single quote or double quote.  

​			Value allows **default, null**.

2. 一次性插入多条数据

```mysql
INSERT INTO 'table_name' VALUES(value1, value2,...), (value1, value2,...);
```

3. 删除数据

- delete all the values in the specific table:

```mysql
DELETE FROM 'table_name';
```

- delete specific rows which include specific values.  

```mysql
DELETE FROM 'table_name' where 'feild_name' ><= figure.
```

notice:  We often use the **primary key** behind the WHERE command.

4. 清空表:

- empty table  (recommend):

```mysql
TRUNCATE 'table_name';
```

**NOTICE: For emptying table, if the table has auto_increment value, auto_increment value will continue to increment starting with the self-incrementing ordinal number of the previous table when you use the delete command. If you use the truncate command, auto_increment value will start from the beginning.**



5. 更新数据

- basic:

```mysql
UPDATE 'table_name' SET 'feild_name1' = 'value1', 'feild_name2' = 'value2',... WHERE 'feild_name' ='value3'; 
```

- satisfy one of the requirements behind the WHERE command : 

```mysql
UPDATE 'table_name' SET 'feild_name1' = 'value1', 'feild_name2' = 'value2',... WHERE 'feild_name' ='value3' or 'feild_name' = 'value4';
```



6. 查询表数据（基本）

```mysql
SELECT 'feild_name' FROM 'table_name';
```

Query row allows *.

1. SQL语句区分

- DDL, 数据定义语言, Data Definition Language

​				`create` `drop` `alter` `show`

- DML, 数据操纵语言, Data Manipulation Language

​				`insert` `update` `delete` `select` 

- DCL, 数据控制语言, Data Control Language



7. 字符集编码问题

- show encoding:

```mysql
show variables like 'character_set_%';
```

8. 撤销上一步操作

- rollback :

```mysql
rollback;
```

Rollback statement **allows you to rollback or undo one more statements that have been recently executed**. For example, if you have accidentally deleted or updated rows, you can use MySQL rollback those statements and restore original databases.







------
# 六、数据类型

**数据类型总结**

- **数值型**

|     类型     | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途           |
| :----------: | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------- |
|   TINYINT    | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值       |
|   SMALLINT   | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值       |
|  MEDIUMINT   | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值       |
| INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值       |
|    BIGINT    | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值     |
|    FLOAT     | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度浮点数值 |
|    DOUBLE    | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度浮点数值 |
|   DECIMAL    | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值         |

notice: decimal(x, y) : x is the precision of the number (**range of the number digit** (bit)), y is the scale (**digit after the decimal** (dot)).   



- **日期和时间类型**

| 类型      | 大小 ( bytes) | 范围                                                         | 格式                | 用途                     |
| :-------- | :------------ | :----------------------------------------------------------- | :------------------ | :----------------------- |
| DATE      | 3             | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3             | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1             | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8             | 1000-01-01 00:00:00/9999-12-31 23:59:59                      | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4             | 1970-01-01 00:00:00/2038结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYYMMDD HHMMSS     | 混合日期和时间值，时间戳 |



- **字符串类型**

| 类型       | 大小                  | 用途                            |
| :--------- | :-------------------- | :------------------------------ |
| CHAR       | 0-255 bytes           | 定长字符串                      |
| VARCHAR    | 0-65535 bytes         | 变长字符串                      |
| TINYBLOB   | 0-255 bytes           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255 bytes           | 短文本字符串                    |
| BLOB       | 0-65 535 bytes        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535 bytes        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215 bytes    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215 bytes    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 bytes | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 bytes | 极大文本数据                    |



- mysql mapping to java datatype

| MySQL Type    | Java Type            |
| ------------- | -------------------- |
| CHAR          | String               |
| VARCHAR       | String               |
| LONGVARCHAR   | String               |
| NUMERIC       | java.math.BigDecimal |
| DECIMAL       | java.math.BigDecimal |
| BIT           | boolean              |
| TINYINT       | byte                 |
| SMALLINT      | short                |
| INTEGER       | int                  |
| BIGINT        | long                 |
| REAL          | float                |
| FLOAT         | double               |
| DOUBLE        | double               |
| BINARY        | byte[]               |
| VARBINARY     | byte[]               |
| LONGVARBINARY | byte[]               |
| DATE          | java.sql.Date        |
| TIME          | java.sql.Time        |
| TIMESTAMP     | java.sql.Tiimestamp  |

​       



1. 数据库的数据类型问题


2. int数值类型


3.  int类型实际操作和注意事项

 Enter the number should be in range.


4. 浮点数类型

   ```mysql
   float(number1, number2)   // number1:  数字位数   number2: 小数位数
   ```

   ```mysql
   double(number1, number2)  // number1:  数字位数   number2: 小数位数
   ```


5. 定点数类型

```mysql
decimal(number1, number2)  // number1:   数字位数    number2: 小数位数
```

notice： decimal type clefts the number storage part: integer part and fractional part.


6. 字符串与文本类型


7. 布尔类型

ture –> 1    false–> 0


8. 枚举类型

``` mysql
enum(value1, value2, value3,...) //  value 只能为枚举类型中的一个值
```


9. 枚举类型的另类存储方式

notice 枚举类型存储值时，使用整数来存储。这种方法可以大幅降低存储值是占用的大量空间。

insert 时 可以直接输入整数来插入下标所对应的值（数组）

10. set类型

SET(val1, val2, val3, ...)  ： A string object that can have 0 or more values, chosen from a list of possible values. You can list up to 64 values in a SET list 

```mysql
insert into "table name"('value1, value2,...');
```



11. 时间日期类型

实际应用当中一定要使用时间field



------
# 七、列属性完整性

1. 列属性问题

primary key 若设置为auto_increment, 则删除一行值后则不能再次使用此id 值插入信息

About InnoDB and MyISAM, note that you cannot reset the counter to a value less than or equal to any that have already been used. For MyISAM, if the value is less than or equal to the maximum value currently in the AUTO_INCREMENT column, the value is reset to the current maximum plus one. For InnoDB, if the value is less than the current maximum value in the column, no error occurs and the current sequence value is not changed.

2. Primary key主键作用以及企业用途

一个表只能有一个主键，但一个主键可以有多个字段（field）.

3. 删除主键、组合键、选择主键

- set primary key

```mysql
alter table 'table_name' add primary key (Field); 
```

- drop primary key

```mysql
alter table 'table_name' drop primary key (Field);
```

- combination primary key

```mysql
alter table 'table_name' add primary key (Field1,Field2);
```



- **主键**:  对于关系表，有个很重要的约束，就是任意两条记录不能重复。不能重复不是指两条记录不完全相同，而是指能够通过某个字段唯一区分出不同的记录，这个字段被称为**主键**。

- 选取主键的一个*基本原则*是：**不使用任何业务相关的字段作为主键。**

- **自增整数类型(常用主键之一)**：数据库会在插入数据时自动为每一条记录分配一个自增整数，这样我们就完全不用担心主键重复，也不用自己预先生成主键；（自增类型尽量选择capacity较大的类型，避免出现容量不足的情况）

- **全局唯一GUID类型（常用主键之二）**：使用一种全局唯一的字符串作为主键，类似`8f55d96b-8acc-4636-8cb8-76bf8abc2f57`。GUID算法通过网卡MAC地址、时间戳和随机数保证任意计算机在任意时间生成的字符串都是不同的，大部分编程语言都内置了GUID算法，可以自己预算出主键。

- **联合主键**： 关系数据库实际上还允许通过多个字段唯一标识记录，**即两个或更多的字段都设置为主键**，这种主键被称为联合主键。

  对于联合主键，允许一列有重复，只要不是所有主键列都重复即可。
4. 复合主键究竟有什么用？(Not recommended)
5. unique唯一键的作用以及使用

唯一键与其他表无关，可以为null,一张表可以有多个唯一键。

```mysql
unique// 唯一键关键字
```
4. 唯一键扩展
5. 主键和唯一键区别

- 主键可能由多个字段构成，而唯一键是一个字段。（论坛id和昵称）
- 一张表有一个主键，可以有多个唯一键。
- 主键可能会被其他表引用，而唯一键不会。
- 主键不能为null, 唯一键可以为null. 

6. sql内注释代码注释

- 单行注释：  

  ```mysql
  create table t_1 (
  id int(10), # This is the comment about this row.
  );
  ```

- 多行注释：

```mysql
create table t_2(
id int(10) not null primary key , 
/*
    This is the primary key in the table.
*/
);
```

-  comment :

```mysql
create table if not exists t_3 (
id int(10) primary key auto_increment comment 'This is the comment about this field.'
);
```




8. 数据库完整性

- eg: 多种因素造成数据库的完整性约束。
- 域完整性，实体完整性，引用完整性，自定义完整性。



9. 引用数据表的完整性问题，抛出外键的概念



10. 外键约束

- 创建表使用：

```mysql
constraint 'foregin_key_name' FOREIGN KEY ('table2 field') REFERENCES 'table1 name'('table1 field');
```

- 修改表使用：

```mysql
alter 'table_name' add  CONSTRAINT 'foregin_key_name'  foreign key ('table2_field') references 'table1_name'('table1_field');  
```



**外来键**又称**外部键**，是指在关联式资料库中，每个资料表都是由关联来连系彼此的关系，父资料表（主表）（Parent Entity）的[主键](https://zh.wikipedia.org/wiki/主键)（Primary Key）会放在另一个资料表（子表），当做属性以建立彼此的关联，而这个属性就是外来键。

从表中包含主表中的primary key, 则称此key为从表的外键。

12. 什么时候设计外键呢？

- **并发设计时禁止使用外键。**

12. 删除外键

- **MUL**意为 此field可重复，并非是外键约束标签。

```mysql
alter table 'table_name' drop foreign key ('table_field'); 
```

- 此table_field 是 mysql生成的constraint (约束)的名称。直接drop foregin key 是无效的。所以，drop foregin key 之前先

```mysql
show create table 'table_name';
```

，查看是否添加foreign key 后再进行删除。（desc 'table_name'; 无法显示表是否包含外键）

12. 外键三种操作：严格、置空、级联的使用场景以及介绍

置空：删除主表中某一条信息，则与之绑定的外键中对应的信息置为NULL；

级联：删除主表中某一条信息，则将与之绑定的外键中对应的信息删除；

13. 置空和级联演示

- 置空：

创建表时，在foreign key 处使用：

```mysql
on delete set null // 删除时置空 ，定义此字段包含置空操作
```

- 级联：

创建表时，在foreign key 处使用：

```mysql
on update cascade // 更新将关联到此字段的外键信息进行相同的操作。
```

cascade: 瀑布，层叠； （cas- , 落下，降临； -ade, 状态，物品）

------
# 八、数据库设计思维

1. 数据库设计的基本概要

冗余： 

2. 实体和实体之间的关系

3. Codd第一范式：确保每列原子性 (All the Feild should be original and be united.)

- BC范式：

4. Codd第二范式：非键字段必须依赖与键字段 （全部属性均为primary_key）

5. Codd第三范式：消除传递依赖

- 避免数据冗余。

------
# 九、单表查询

1. 开端
2. select

- ```mysql
  select 'any date'; # the date may exist or not
  ```

- ```mysql
  select 'any date' as 'field name'; # as can be omit
  ```

  

3. from

​	from返回一个笛卡尔集。即可以from 多个表组合起来。

1. dual

​	dual 默认伪表

```mysql
select 7*9 as res from dual;
```



1. where 

条件筛选

equal: =  ;   unequal:    ！=   ,  <>;     小于：<;      大于：> ;       

1. in

​	可以进行特殊值查询



1. between...and

闭区间

1. is null



1. 聚合函数

自带的集成函数： sum(), avg(), max(), min(), count(), {count(*);count(1);}

1. 第三方客户端的使用

navicat

1. like模糊查询

```mysql
select * from 'table_name' where 'field' like '张%'; 
```



1. order by 排序查询

升序

```mysql
select * from 'table_name' order by 'field_name' asc;
```

降序

```mysql
select * from 'table_name' order by 'field_name' desc; 
```



1. group by 分组查询

for  example :

// 升序

```mysql
select avg('field_name') as '列名称', 'field_name' as '列名称' from 'table_name' group by 'field_name' asc;
```

// 降序

```mysql
select avg('field_name') as '列名称', 'field_name' as '列名称' from 'table_name' group by 'field_name' desc;
```



1. group_concat

```mysql
select group_concat('field_name'), 'field_name' from 'table_name' group by 'field_name';
```



1. having

在查询的结果集中查询用 having.

for example,

```mysql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```



1. limit 

limit 用来限定起始位置和终了位置。

```mysql
select * from 'table_name' limit 1, 5;
```

第一个数值代表起始位置，第二个数字代表查询长度。

1. distinct all

去重

```mysql
select count(distinct 'field_name') from 'table_name';
```



------
# 十、多表查询

1. union联合查询

The `UNION` operator is used to combine the result-set of two or more `SELECT` statements.

```mysql
select * from 'field_name1' union select 8 from 'field_name2';
```

You can use `distinct` after union to make row distinct.

like this:

```mysql
select * from 'field_name1' union distinct select 8 from 'field_name2';
```



1. inner join内联查询

通过两个表中的公共字段，在两张表之间建立连接。（主从关系）

```mysql
select 'field_name1', 'field_name2'
from 'table_name1'
inner join 'table_name2' on  'table_name1'.'field_name' = 'table_name2'.'field_name';
```

1. inner join注意事项

1. left join 

以左表为基准，将两个表建立连接

for example,

```mysql
select 'field_name1', 'field_name2'... 
from 'table_name1' left join 'table_name2'
on 'table_name1'.'field_name' = 'table_name2'.'field_name';
```

1. rigth join

以右表为基准，将两个表建立连接

for example,

```mysql
select 'field_name1', 'field_name2'... 
from 'table_name1' right join 'table_name2'
on 'table_name1'.'field_name' = 'table_name2'.'field_name';
```



1. cross join

将两个表的字段排列组合组成一个笛卡尔积输出。

1. natural join

默认将两张表字段中名称完全相同的作为公共字段，建立连接。

1. 无公共同名字段的自然返回笛卡尔积
2. using



1. 哪一个实用？

一般来说用inner join， 为了保证两张表的信息都能显示出来。 

------
# 十一、子查询

1. 子查询基本语法

在查询语句中嵌套一个子查询。

1. in 和 not in 

一般来说，在where 后使用in(‘child statement ’)

1. exists 和 not exists

exists: 只要条件存在就显示; not exists:只要不存在就显示; 

1. 基础结束语




------
# 十二、高级部分

## （一）view 视图

1. 开场
2. view视图创建、使用以及作用

```mysql
create view 'view_name' as
select 'field_name1','field_name2'... 
from 'table_name';
```



1. 显示视图  

```mysql
desc view 'view_name';
```

```mysql
show create view 'view_name';
```

```mysql
show table status where comment='view' \G
```



1. 更新和删除视图

更新

```mysql
alter view 'view_name' as select...;
```

删除

```mysql
drop view 'view_name';
```



1. 视图算法： temptable, merge

for example,

```mysql
create algorithm = temptable view 'view_name'as ...
```

temptable 临时算法

merge 合并算法

## （二）transaction 事务

1. 事务的提出
2. transaction

for example,

```mysql
start transaction;
update 'table_name' set 'field_name' = 'field_name' + 100;
rollback;
commit;
```

执行rollback 可以回滚到transaction开始；



1. rollback to point

类似与虚拟机快照；

for example,

```mysql
start transaction;
update 'table_name' set 'field_name' = 'field_name' + 100;
savepoint point_one;
insert into 'table' values(...);
rollback to point_one;
commit;
```

1. ACID

atomicity 原子性,    consistency 一致性,    lsoation  隔离性,    durability  持久性     

1. 注意事项

**innoDB 中，才可以使用事务。**

## （三）索引

- 索引是关系数据库中对某一列或多个列的值进行预排序的数据结构。

- 索引用于查找元素，分类column,加快查找速度。
- 使用主键索引的效率是最高的，因为主键会保证绝对唯一。
- [主键（Primary Key），外键（Foreign Key），唯一键（Unique Key）,索引（Index）的区别](https://www.ljwit.com/archives/database/255.html)  

1. 四大索引

## （四）存储过程

1. delimiter 
2. procedure存储过程的用途

## （五）有趣的函数

1. number
2. string

1. others

------
# 十三、企业规范约束

1. ★库表字段约束规范
2. 索引规范

1. ★SQL开发约束规范
2. 其他规范

