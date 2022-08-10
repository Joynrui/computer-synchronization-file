# Oracle Database

## 1. 什么是Oracle BD
### 1.1 Oracle文件类型
#### 1.1.1  数据文件（.DBF）

​		数据文件是一个二进制文件，用于保存用户应用程序数据和Oracle系统内部的数据的文件，这些文件在操作系统中就是普通的操作系统文件。OracleDB在创建表空间的同时会创建数据文件。

#### 1.1.2 控制文件（.CTL）

​		控制文件是二进制文件，，主要用于记录数据库的名称，数据库的存放位置等信息。一个控制文件只能属于一个数据库。若控制文件丢失则数据库无法工作。类似于配置文件。

#### 1.1.3日志文件（.LOG）

​		日志文件在OracleDB中分为**重做日志**文件和**归档日志**文件。重做日志文件是OracleDB正常运行的必要文件。重做日志文件主要记录了数据库的操作过程，用于备份和还原数据库，以达到数据库的最新状态。归档日志是对重做日志的一种归档处理。设备必须开去归档模式才能创建归档日志文件。

### 1.2 Oracle实例

​		实例就是数据库启动后**分配的内存和建立的后台进程**。数据库关闭后，数据库文件还存在但实例不存在了。

### 1.3 Oracle实例与数据库的关系

​		实例就是一组操作系统进程（或者是一个多线程的进程）以及一些内存。这些进程可以操作数据库，而数据库就是一个文件集合（数据文件，临时文件，重做文件和控制文件）。

​		在任何时刻，一个实例只能有一组相关的文件（与一个数据库关联），大多数情况下，反过来也成立；一个数据库上只有一个实例对其进行操作。

### 1.4 Oracle版本说明

​		Oracle 8i  /   Oracle 9i  /  Oracle 10g  /  Oracle 11g  /  Oracle 12c  

​		i: i 代表Internet。8i版本开始对Internet支持。                        g: g 代表Grid网格计算，10g加入了网格计算的功能

​		c: c代表cloud云计算设计。12c版本代表对云计算的支持。

## 2. Oracle目录说明

19c版本基本目录共4个：cfgtoollogs、checkpoints、diag、product。

### 2.1 cfgtoollogs

下面子目录分别存放当前运行的dbca，emca，netca等图形化配置时的log。

### 2.2 checkpoint

存检查点文件

### 2.3 diag

​		一个重组目录，用于存放所有组件的需要被用来诊断的log文件都存放在了这个目录。这个目录是11g中新添加的，10g以前的log文件是散放的。

### 2.4 flash_recovery_area 闪回区 

19c版本oracledb，本目录默认情况下暂未出现。已知11g默认创建flash_recovery_area 文件夹。

​		闪回区目录用于分配一个特定的目录位置来存放一些特定的恢复文件，用于集中和简化管理数据库恢复工作。闪回区可以存储完全的数据文件备份，增量文件备份，数据文件副本，当前的控制文件，备份的控制文件，spfile文件，快照控制文件，联机日志文件，归档日志，块跟踪文件，闪回日志。

### 2.5 oradata

存放数据文件

### 2.6 product

Oracle RDBMS 软件存放位置。Relational Database Management System,关系型数据库。



## 3. Oracle system user

### 3.1 sys

超级账户，可以控制数据库的所有功能。

### 3.2 system

系统用户，权限等级低于sys，通常用于创建一些用户查看管理信息的表或视图。

### 3.3 scott 用户

示例用户，提供了一些学习oracle的操作数据表。

### 3.4 HR 用户

Oracle示例用户，用于学习。

19c需要设置相关属性才能使用hr用户。

参考如下：[为oracle19c创建hr样例数据库](https://www.yikakia.com/%E4%B8%BAoracle19c%E5%88%9B%E5%BB%BAhr%E6%A0%B7%E4%BE%8B%E6%95%B0%E6%8D%AE%E5%BA%93/)



**普通用户可以有的最高权限是dba。数据库本身的最高权限用户是sys。**

## 4. Oracle 启动

oracle是通过系统的服务来启动的。

### 4.1 OracleServiceORCL（必须启动）

数据库服务（数据库实例），是Oracle核心服务，该服务是数据库启动的基础，只有该服务启动，Oracle数据库才能正常启动。

### 4.2 OracleOraDb19c_home1TNSListener（必须启动）

监听器服务，服务只有在数据库需要远程访问的时候或者使用PL/SQL Developer 等第三方工具时才需要。

### 4.3 OracleORCLVSSWriterService（非必须启动）

Oracle卷映射拷贝写入服务，VSS（Volume Shadow Copy Service）能够让存储基础设备（比如磁盘，阵列等）创建高保真的时间点映像，即映射拷贝（Shadow copy）.它可以在多卷或者单个卷上创建映射拷贝，同时不会影响到系统的系统能。

### 4.4 OracleDBConsoleorcl（非必需启动）

Oracle数据库控制台服务，orcl是Oracle的实例标识，默认的实例为rocl。在运行Enterprise Manager 的时候，需要启动这个服务。

### 4.5 OracleJobSchdulerORCL（非必需启动）

Oracle作业调度（定时器）服务，ORCL是Oracle实例标识。

### 4.6 OracleMTSRecoveryService（非必需启动）

服务端控制，该服务允许数据库充当一个微软事务服务器MTS，COM/COM+对象和分布式环境下的事务的资源管理器。



## 5. SQL Plus

-   login:  sys登录账户有两个： sysdba 与 sysoper

```sql
sys as sysdba // longin username
orcale123 // password
```

-   system账户可以直接登录

```sql
system
oracle123
```

-   在 all_users 表中可以查询oracle的所有用户；



## 6. Oracle表空间分类

### 6.1 永久表空间 permanent tablespace

​		保存数据库的逻辑划分，数据对象都存储在指定表空间中。主要存储表。

### 6.2 临时表空间 temporary tablespace

​		主要存放查询和缓冲数据。临时表空间是为了对查询的中间结果进行排序。重启数据库将释放临时表空间。





## 7. 创建用户，创建表空间，分配权限,  登录数据库，删除用户

1. 创建用户：notice：**创建用户时建议不使用双引号，双引号会被记录进用户名**。本笔记使用双引号仅为区分statement单词。
```sql
create user "username" identified by "password";
```
2. 修改密码：（optional）
```sql
alter user "username" identified by "new_password";
```
默认情况下用户创建完成之后系统会默认给该用户分配一个表空间（users）
3. 查询所有用户所在的表空间：
```sql
select "username", default_tablespace from dba_users; 
```
一般在开发过程中不使用用户默认表空间，这时需要创建表空间；
4. 创建永久表空间：e.g., 创建一个名为tablespace_name 的表空间， 绝对地址是 D:/oracle/oradata/user_name.dbf, 大小 20M 每次以10M 为最小单位自动扩大容量 。(.dbf为数据文件)


```sql
create tablespace "tablespace_name" datafile "D:/oracle/oradata/user_name.dbf" size 20M autoextend on next 10M permanent online;
```

5. 将表空间分配给用户：
```sql
alter user "username" default tablespace "tablespace_name";
```

6. **权限分配**
```sql
grant create session,create table, create view, create sequence,create trigger, create procedure, unlimited tablespace to "username";
```
（可以给用户以dba权限，授予最高控制权，便于学习）

7. 测试登录：
```sql
conn "username/password"
```
8. 删除用户及其相关对象：
```sql
drop user "username" cascade;
```

- **密码永不过期**：
```sql
sqlplus / as sysdba; # 命令行以sysdba的方式进入
select username,profile from dba_users;# 查看用户的密码策略，一般是default
select * FROM dba_profiles s 
Where s.profile='DEFAULT' AND  resource_name='PASSWORD_LIFE_TIME';# 查看指定概要文件（如default）的密码有效期设置
ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;# 将密码有效期由默认的180天修改成“无限制”
alter user yb_dev identified by yb_dev;# 修改密码，相当于重置密码
```



## 8.权限分配

### 8.1 对象权限(Object privileges)

对象权限是指在指定的表，视图，序列上制定执行动作的权限。

### 8.2 角色权限(Role privileges)

角色是可以授予用户的相关权限的组，该方法使用权限的授予，撤回更加容易管理。

### 8.3 系统权限(System privileges)

为用户分配权限创建表，创建用户，创建视图，创建存储过程等权限。





## 9.链接配置

### 9.1 文件位置

.\dbhome\network\admin       若安装数据库目录中包含product则为此目录

.\dbhome\network   若数据库软件本体不在product中则为此目录

### 9.2 sqlnet.ora

名称解析，此文件用于链接的链接字符串。

e.g. , 

```
NAMES.DIRECTORY_PATH= (TNSNAMES, EZCONNECT)
```



### 9.3 tnsnames.ora

用在oracle client端，用户配置连接数据库的别名参数。

e.g.,  

```
ORCL =      
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = localhost)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

- ORCL: 客户端链接服务端使用的服务别名，注意顶行写。 

- PROTOCOL: 客户端链接服务端的通讯协议。
- HOST:服务端ip地址，主机名。
- PORT: 数据库侦听端口号，1521是oracle默认使用的端口号。

### 9.4 listener.ora

用在oracle server端， 配置oracle的监听端口。

e.g.,

```
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = localhost)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )
```

- LISTENER:监听名称，可以配置多个监听，每个监听端口号不同。
- PROTOCOL:监听协议。
- HOST:本地ip或localhostname。
- PORT:监听端口号。



*Net Configuration Assistant 工具可以对listener.ora做简单修改*



[Oracle中TNS的完整定义](https://www.cnblogs.com/xubao/p/14228634.html)：transparence Network Substrate透明网络底层，监听服务是它重要的一部分，不是全部，不要把TNS当作只是监听器。

TNS是Oracle Net的一部分，专门用来管理和配置Oracle数据库和客户端连接的一个工具，在大多数情况下客户端和数据库要通讯，必须配置TNS，当然在少数情况下，不用配置TNS也可以连接Oracle数据库，比如通过JDBC。如果通过TNS连接Oracle，那么客户端必须安装Oracle client程序。

Oracle当中，如果想访问某个服务器，必须要设置TNS，它不像SQL SERVER那样在客户端自动列举出在局域网内所有的在线服务器，只需在客户端选择需要的服务器，然后使用帐号与密码登录即可。而Oracle不能自动列举出网内的服务器，需要通过读取TNS配置文件才能列出经过配置的服务器名。



**本地网络服务配置**





## 10. 数据类型



### 10.1 字符类型

- oracle存储数据时，西文，数字用一个字节存储，汉字用三个字节存储。e.g., char(12) 可以保存四个汉字。

1. **CHAR**：定长字符串，**会用空格填充来达到所设定的最大长度**。（非NULL） 最大长度**2000字节**。若创建表未给定长度则默认为1。
2. **VARCHAR2**：变长字符串，**其长度由其实际值决定**。最大长度为**4000字节**。(最常用)
3. **NVARCHAR2**：包含**UNICODE**格式数据的变长字符串，最大长度**4000字节**。

### 10.2 数字类型

1. **NUMBER:**  **NUMBER(P,S)**是最常见的数字类型。P是precison(精确)，精度，表示有效数字位数，最多不能超过38个有效数字。S是scale(刻度)，表示小数点的位数。
2. **INTEGER:** INTEGER是NUMBER的子类型，等同于NUMBER(38,0), 用于存储整数。若插入更新的数值中有小数，则四舍五入。

### 10.3 浮点类型

1. **BINARY_FLOAT:** 32位，单精度浮点数。支持至少6位精度，每个BINARY_FLOAT的值需要5个字节，包括长度字节。
2. **BINARY_DOUBLE:** BINARY_DOUBLE 64位双精度浮点数。每个值9个字节，包括长度字节。

### 10.4 日期类型

1. **DATE:** oracle日期类型存储以下信息：世纪，年，月，日，小时，分钟，秒。占用7个字节。
2. **TIMESTAMP:** 7字节或12字节的定宽日期时间类型。与data不同，timestamp可以包含小数秒，小数最多保留9位。
3. **TIMESTAMP WITH TIME ZONE:** timestamp变种，包含时区偏移量的值。
4. **TIMESTAMP WITH LOCAL TIME ZONE:** 将时间数据以数据库时区进行规范化后储存。

### 10.5 LOB类型

1. **CLOB**  (Character Large Object

二进制数据，存储单字节和多字节字符数据，最大长度4g

2. **BLOB** （Binary Large Object）

存储非结构化的进制数据大对象，可以被当作是没有字符集语义的比特流，一般是图像，声音，视频等文件。，最大4G

3. **NCLOB** 数据类型

存储unicode类型数据，最大长度4G

### 10.6 LONG&RAW&LONG RAW 类型

1. **LONG**

它存储变长字符串，最大长度2G（2000兆字节，非2000兆字符）

2. **LONG RAW**

存储2G原始二进制数据，存放多媒体数据。

3. **RAW** 

存储二进制字符类型数据，必须制定长度。这种数据类型存储的数据不会发生字符集转换。可存放多媒体数据。



##  11. 创建表

### 11.1 oracle表命名规则 

- **字母开头**
- 长度不超过30个字符
- 避免使用oracle的关键字
- 只使用大小写字母数字和_#$

### 11.2 使用带有特殊符号的表名

创建表时oracle会自动转换大写，表名对大小写不敏感。

**若定义表名需要有消写字母或特殊符号，则需要用双引号括起表名**。

## 12. 约束

### 12.1 主键约束 Primay key Constraint

### 12.2 外键约束 Foreign key Constraint

### 12.3 唯一约束 Unique Constraint

### 12.4 检查约束 Check Constraint

对该列数据的范围、格式的限制

### 12.5 非空约束Not Null Constraint 





## 13. 查询

### 13.1 select

1. select:  与mysql基本一致；允许select column 加减乘除。

e.g.,

```sql
select employee_id, first_name, salary * 12 from employees;
```



2. 定义列别名

使用 as 关键字，或可省略；

e.g.,

```sql
select first_name as name, salary "salary number" from employees;
```



3. 连字运算符：

  `||`  双竖线为连字符， 可以将两列 合并为一列输出

e.g.,

```sql
select first_name || last_name from employees;
```



4. 文字字符串：

连字符中间可以包含字符串，可以是数字。

e.g., notice : 文字字符串只能用单引号

```sql
select first_name || last_name || ' is a ' || job_id  as "employee details" from employees;
```



5. 去除重复值：

`distinct` 用于去重

e.g., notice: distinct 写在select 之后， 对结果集的所有列有效。

```sql
select distinct department_id, last_name from employees;
```

 

### 13.2 where

6. 限制输出：

使用where，类mysql;

e.g.,

```sql
select last_name, job_id, department_id from employees where department_id = 90;
```

notice:  oracle where 语句 中 不等于 可用 `!=, <>, ^=` 表示。 

- ​	其他比较条件：

| 操作               | 含义                 |
| ------------------ | -------------------- |
| BETWEEN ... AND... | 在两个值之间（包含） |
| IN(set)            | 匹配一个任意值列表   |
| LIKE               | 匹配一个字符模板     |
| IS NULL            | 是一个空值           |

>1. between A and B  会被转化为  >= A and <= B, 没有实质上的性能提升。
>
>2. in 只能用于 =  ，  多个in 条件用逗号隔开， 多个in会被转化为 = A or = B。
>
>3. like 写在 field后，字符串用单引号括起来，通配符包括多自通配符`%`和单字通配符`_`。
>
>    - escape关键字用于定义包含特殊字符的字符串
>
>    e.g.,
>
>    ```sql
>    select last_name, job_id from employees where job_id like 'SA\_%' escape '\';
>    ```
>
>4. IS NULL 
>
>    e.g.,
>
>    ```sql
>    select last_name, job_id, commission_pct from employees where commission_pct is null;
>    ```



### 13.3 逻辑条件

**AND OR NOT**

- 逻辑条件的优先级： not > and > or, 语句中可以使用括号指定优先级。



### 13.4 ORDER BY 排序

类mysql, ASC升序；DESC降序。

e.g.,

```sql
select hire_date, salary from employees order by hire_date, salary desc;
```





##  14. 函数

### 14.1 函数类型

#### 14.1.1 单行函数

**单行函数仅对单个函数进行运算，并且每行返回一个结果。**

>- 可能需要一个或多个参数
>- 可以修改结果集的数据类型
>- 可以嵌套
>- 可能返回一个与参数不同类型的数据值
>- 能在 SELECT, WHERE 和 ORDER BY 子句中



##### 字符函数

单行字符函数接收字符数据作为输入，可以返回字符值和数字值。



- 大小写处理函数

| 函数                      | 作用                       | 结果       |
| ------------------------- | -------------------------- | ---------- |
| **LOWER('SQL Course')**   | 所有字符转换成小写         | sql course |
| **UPPER('SQL Course')**   | 所有字符转换成大写         | SQL COURSE |
| **INITCAP('SQL Course')** | 每个单词首字母大写其他小写 | Sql Course |

- 字符串处理函数
    - dual表：一张只有一个字段，一行记录的表。亦称伪表，不存储主题数据。其目的是当前不需要从具体的表中取得数据仅为了显示输入的值时，满足select语句格式。 


| **函数**                        | **作用**                                                     | **结果**       |
| ------------------------------- | ------------------------------------------------------------ | -------------- |
| **CONCAT('Hello', 'World')**    | 链接字符串                                                   | HelloWorld     |
| **SUBSTR('HelloWorld', 1, 5)**  | 截取子串，arg2可以为负数，-1为最后一位，-2为倒数第二位       | Hello          |
| **LENGTH('HelloWorld')**        | 获取字符串长度                                               | 10             |
| **INSTR('Hello World', 'W')**   | 获取字符位置。对于重复出现的字符，INSTR重载为('HelloWorld', 'l', 3[起始位置], 2[出现次数]),返回4 | 6              |
| **LPAD(salary, 10, '*')**       | 在字符串左侧添加字符，arg2为字符串总长度（添加之后）         | *\*\*\*\*24000 |
| **RPAD(salary, 10, '*')**       | 在字符串右侧添加字符                                         | 24000*\*\*\*\* |
| **TRIM('H' FROM 'HelloWorld')** | 头尾剪切字符。默认头尾都剪切，剪切字符前加 both为头尾剪切，leading为剪切串头，trailing为剪切串尾。对大小写敏感。 | elloWorld      |

补充示例：

TRIM(both 'H' FROM 'HelloWorld')

TRIM(leading 'H' FROM 'HelloWorld')

TRIM(trailing 'H' FROM 'HelloWorld')



##### 数字函数

- **ROUND(arg1, arg2)**: 四舍五入。

e.g., ROUND(198.568)  结果为 199；round(198.568, 2) 结果为 198.57； round(198.568,-2) 结果为200。

- **TRUNC(arg1，arg2)**:  截断指定小数位，不做四舍五入处理。

e.g., TRUNC(198.568) 结果为 198； TRUNC(198.568, 2) 结果为 198.56；TRUNC(198.568, -1) 结果为190。

- **MOD(arg1,arg2)**: 取余,取模

e.g.,MOD(被除数，除数)





##### 日期函数

**SYSDATE** 是一个日期函数，返回当前服务器设备的日期时间。

sysdate不需要参数，使用可以直接写成 `select sysdate from dual;`。

- 日期的计算：

1. 日期加减一个数结果是一个日期值；

```sql
select sysdate - 1 from dual;
select sysdate + 2 from dual;
```



2. 两个日期相减结果是日期之间的天数；

```sql
select sysdate - hire_date from employees;  # 返回雇佣天数
```



3. 用小时数除以24，可以将小时数加在日期上，返回一个日期数。																																																																		

```sql
select sysdate - 48/24 from dual; # 返回当前系统时间的未来两天
select sysdate - 36/24 from dual; # 返回当前系统时间的未来两天
```



**其他日期函数**

| 函数               | 说明               |
| ------------------ | ------------------ |
| **MONTHS_BETWEEN** | 两个日期之间的月数 |
| **ADD_MONTHS**     | 加月份到日期       |
| **NEXT_DAY**       | 下个星期几是几号   |
| **LAST_DAY**       | 指定月的最后一天   |
| **ROUND**          | 四舍五入日期       |
| **TRUNC**          | 截断日期           |



complement:

1. months_between(date1, date2): 计算date1 和 date2 之间的月数。其结果可以是正数也可以是负数。如果date1大于date2，结果是正数。反之结果为负数。

​		date为日期类型

2. add_months(date, n): 添加n个日历月到date。n的值必须是整数，但可以是负数。

​		n为整数

3. next)day(date, 'char' or integer): 计算在date之后的下一个周('char')的指定天的日期。char的值可能是一个表示一天的数或者是一个字符串。如果使用数字表示星期，1从星期一开始，数字范围1~7。
4. last_day(date): 计算包含date的月的最后一天的日期。
5. round(date, 'format'): 返回用格式化模式format四舍五入到指定单位的date，如果格式模式format被忽略，date将被四舍五入到最近的天。 

​		round可以有以下用法：round(sysdate, 'yy')精确到年，round(sysdate,'mm')精确到月，round(sysdate,'dd')精确到日。

3. trunc(date,'format'): 返回用格式化模式format截断到指定单位的date。如果格式模式format被忽略，date被截断到最近的天。 









#### 14.1.2 聚合函数

聚合函数操作成组的行，每个组返回一个结果，也称组函数。



### 14.2 数据类型转换

#### 14.2.1 隐式数据类型转换

原始数据没有进行转换时，系统会根据需要自动进行数据类型转换，即隐式转换。

- 直接赋值转换

| 从                | 到       |
| ----------------- | -------- |
| varrchar2 or char | number   |
| varchar2 or char  | date     |
| number            | varchar2 |
| date              | varchar2 |

- 表达式赋值转换

| 从               | 到     |
| ---------------- | ------ |
| varchar2 or char | number |
| varchar2 or char | date   |

*隐式转换的性能问题和可读问题非常严重，隐式转换时索引失效导致数据库性能下降；可读性也因是隐式导致操作员不易清楚数据转换的实际情况。*



#### 14.2.2 TO_CHAR

to_char(arg1, 'fmt'): 将一个日期或者数字转换为字符类型，格式化样式fmt。

arg1: 数字或者日期类型，需要转换数据。

fmt：转换格式。

日期格式：

| element | illustrate       |
| ------- | ---------------- |
| YYYY    | 数字全写年       |
| YEAR    | 年的拼写         |
| MM      | 月的前两位       |
| MONTH   | 月全名           |
| MON     | 缩写             |
| DY      | 周中的三字母缩写 |
| DAY     | 周中天的全名     |

e.g.,

```sql
select to_char(sysdate, 'yyyy') from dual;
```

其他格式：

| element                 | illustrate                               |
| ----------------------- | ---------------------------------------- |
| SCC or CC               | 世纪，带  -  服务器前缀B.C. 日期         |
| 日期中的年YYYY or SYYYY | 年，带 -  服务器前缀B.C. 日期            |
| YYY or  YY or Y         | 年的最后3、2 或1个数字                   |
| Y,YYY                   | 年，在这个位置带逗号                     |
| IYYY,IYY,IY,I           | 基于ISO标准的4、3、2、或1位数年          |
| SYEAR 或YEAR            | 拼写年：带 -  服务器的前缀B.C.日期       |
| BC or AD                | B.C.A.D.指示器                           |
| Q                       | 四分之一                                 |
| MM                      | 月：两位数字值                           |
| MONTH                   | 9位字符长度的带空格填充的月的名字        |
| MON                     | 3字母缩写的月的名字                      |
| RM                      | 罗马数字月                               |
| WW or W                 | 年或月的周                               |
| DDD or DD or D          | 年、月或周的天                           |
| DAY                     | 9位字符长度的带空格填充的天的名字        |
| DY                      | 3字母的缩写的天的名字                    |
| J                       | 儒略日，从公元前4713年12月31日开始的天数 |



时间格式模板元素：

| element            | illustrate                              |
| ------------------ | --------------------------------------- |
| AM or PM           | 正午时间                                |
| A.M.或P.M          | 带句号的正午指示                        |
| HH or HH12 or HH24 | 天的小时，或小时（1-12）,或小时（0-23） |
| MI                 | 分钟（0-59）                            |
| SS                 | 秒（0-59）                              |
| SSSSS              | 午夜之后的秒(0-86399)                   |

在格式串中允许添加特殊字符，如 :  - 等。若要添加汉字或字母，则需要用双引号括起来。

e.g.,

```sql
select to_char(sysdate, 'y,yyy"年"MM"月"DD"日 and" hh24-mi:ss') from dual;
```

指定后缀来影响数字显示

| element      | illustrate                       |
| ------------ | -------------------------------- |
| TH           | 序数（DDTH 显示为4TH）           |
| SP           | 拼写出数字（DDSP 显示为 FOUR）   |
| SPTH or THSP | 拼写出序数（DDSPTH显示为FOURTH） |

  







## $$ Error 记录

- *ORA-01219*：这是因为物理上删除了A.DBF文件，但是在oracle系统中关联记录并没有删除。所以我们接下来做的就是使用“**alter database datafile 'E:\DBF\A.DBF' offline drop;**”语句删除oracle系统中的关联记录。

solution: 

>1. sysdba身份登录数据库；
>
>2. ```sql
>    alter database open;
>    ```
>
>    此时会报类似“**ORA-01157: 无法标识/锁定数据文件 12 - 请参阅 DBWR 跟踪文件ORA-01110: 数据文件 12: 'E:\DBF\A.DBF'**”的错误。
>
>3. ```sql
>    alter database datafile 'E:\DBF\A.DBF' offline drop;
>    ```
>
>4. 再次进行**alter database open;**操作，直到不报错为止即可。

reason：**不要将.dbf文件手动删除，会造成此错误**。



- *ORA-01034和ORA-27101*：

参考如下：[解决：ORA-01034: ORACLE not available ORA-27101](https://blog.csdn.net/qq_35804654/article/details/72810066)



