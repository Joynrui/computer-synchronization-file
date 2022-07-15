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

​		Oracle RDBMS 软件存放位置。Relational Database Management System,关系型数据库。



## 3. Oracle system user

### 3.1 sys

超级账户，可以控制数据库的所有功能。

### 3.2 system

系统用户，权限等级低于sys，通常用于创建一些用户查看管理信息的表或视图。

### 3.3 scott 用户

示例用户，提供了一些学习oracle的操作数据表。



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

1. 创建用户：
```sql
create user "username" identified by "password" ;
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


