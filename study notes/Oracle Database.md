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



