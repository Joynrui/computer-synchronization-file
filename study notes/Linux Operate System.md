

# Linux Operate System





## 概论

### I. Linux 学习内容

1. **Linux kernel ;**
2. **GNU Tools ;**
3. **GUI Desktop environment ;**
4. **Application ;**



**注意：**Linux   属于现代名称，全称应叫做  “ **GNU/Linux** ”

- **GNU**是一个[自由](https://zh.wikipedia.org/wiki/自由軟體)的[操作系统](https://zh.wikipedia.org/wiki/作業系統)，其内容软件完全以[GPL](https://zh.wikipedia.org/wiki/GPL)方式发布。这个操作系统是[GNU计划](https://zh.wikipedia.org/wiki/GNU計劃)的主要目标，名称来自GNU's Not Unix!的[递归缩写](https://zh.wikipedia.org/wiki/遞迴縮寫)，因为GNU的设计类似[Unix](https://zh.wikipedia.org/wiki/Unix)，但它不包含具著作权的Unix代码。GNU的创始人，[理查德·马修·斯托曼](https://zh.wikipedia.org/wiki/理察·馬修·斯托曼)，将GNU视为“达成社会目的技术方法”。
- **GNU**亦指一个组织。由于Linux内核上原本没有任何软件，所以GNU 通过模仿Unix,为Linux 开发了一些必要的系统软件。
- **GNU通用公共许可协议**（英语：GNU General Public License，缩写GNU GPL 或 GPL），是被广泛使用的[自由软件](https://zh.wikipedia.org/wiki/自由軟件)[许可证](https://zh.wikipedia.org/wiki/软件许可证)，给予了终端用户运行、学习、共享和修改软件的自由。[[6\]](https://zh.wikipedia.org/wiki/GNU通用公共许可证#cite_note-blackduck2015-6)许可证最初由[自由软件基金会](https://zh.wikipedia.org/wiki/自由軟件基金會)的[理查德·斯托曼](https://zh.wikipedia.org/wiki/理查德·斯托曼)为GNU项目所撰写，并授予计算机程序的用户[自由软件定义](https://zh.wikipedia.org/wiki/自由軟體定義)（The Free Software Definition）的协议。

### II. Linux  基本框架

1. 应用软件 ------> GUI  ------>   GNU  ------>  Linux kernel ------->  hardware

2. Linux kernel 可直接控制GUI（Graphical  User Interface ,图形用户界面）

------



## GNU核心

​		原本在Unix 上的一些命令和工具，被模仿到了Linux上。

- 供Linux 使用的工具，GNU 核心工具组 ： GNU Core Utilities， 亦简写为coreutils. coreutils是一个软件包，它包含了了许多基本工具，用以在类Unix系统上实现。 



------



## Linux 内核  

1. 管理硬件设备；
2. 管理软件程序；
3. 管理内存；
4.  文件管理。



------



## Linux 文件管理

1. 文件系统： Linux 在最初的设计是 **MINIX1** 文件系统，它只支持 14 字节的文件名，它的最大文件只支持到 64 MB。在 MINIX 1 之后的文件系统是 ext 文件系统。ext 系统相较于 MINIX 1 来说，在支持字节大小和文件大小上均有很大提升，但是 ext 的速度仍没有 MINIX 1 快，于是，ext 2 被开发出来，它能够支持长文件名和大文件，而且具有比 MINIX 1 更好的性能。这使他成为 Linux 的主要文件系统。只不过 Linux 会使用 `VFS` 曾支持多种文件系统。在 Linux 链接时，用户可以动态的将不同的文件系统挂载倒 VFS 上。

   **Linux 中的文件是一个任意长度的字节序列**，Linux 中的文件可以包含任意信息，比如 ASCII 码、二进制文件和其他类型的文件是不加区分的。



2. ***延伸文件系统*** ： 缩写为 ext或 ext1，Extended file system,  ext采用Unix 文件系统（UFS）元数据结构， 克服MINIX文件系统性能不佳的 问题而开发的，它也是第一个在Linux 上通过虚拟文件系统实现的文件系统  。其后继版本为ext2，xfs等。
3. 其他文件系统： FAT32  、NTFS(Windows 主流文件系统)，exFAT等。

### Ubuntu Linux home content

1. Linux 一切皆为文件，没有分盘之说。
2. / ：Linux  root content.
3. /bin: Linux binary content  (GUN tools)
4. /etc : Linux system configuration content。
5. /lib : Linux system Library，存放软件依赖的程序。 
6. /mnt : Linux 挂载目录。
7. /proc : 伪文件目录。
8. /run :运行目录。
9. /tmp: temp content.
10. /var :可变目录 log.
11. /boot :启动目录。
12. /dev: 设备目录。
13. /media :媒体目录。
14. /opt: 可选目录，第三方文件.
15. /sbin: 系统二进制目录，GNU高级管理员命令工具。
16. /srv: 服务目录。
17. /usr:用户二进制目录， GUN tools.

#### Linux 文件分类

-  .xxxxx ：以点开头的文件或文件夹为隐藏文件。
-  

------



## Shell 

- Linux shell 源于Unix shell , 即“壳层”概念，Linux shell提供了Linux 用户 与电脑交互的方式，即Command-Line Interface,CLI,命令行。

- shell 命令行壳层提供了一个命令行界面（CLI）；图形壳层界面提供了一个图形用户界面（GUI）。

- **链接文件** ：**符号链接**（**软链接）**（快捷方式），**硬链接**，相当于文件副本。（文件真正删除的条件是与之相关的所有硬链接文件均被删除。且硬链接只能链接文件，不能指向文件夹）

     ​	**硬链接原理**：硬链接通过索引节点进行链接。在linux的文件系统，保存在磁盘分区的文件不管是什么类型都会给他分配一个编号，称为索引节点号。在linux中，多个文件名指向同一个索引节点是存在的。这种情况就是硬链接。即便删除源文件，如果这个文件的硬链接还存在，则这个文件不会被删除，除非所有的硬链接全部被删除（即当前文件的索引计数为0），这个文件才真正意义上的被删除（释放空间）。

     

- ~: 当前用户目录

- $:等待用户输入



### Shell Basic Command

#### Common command

- ls :展示当前文件，不包含隐藏文件

     ​		***，？：文件扩展匹配符**

     ​			**[ ]       元字符通配符。**

     ```linux
     ls "example?"(?代表一个字符)   ls "example*"(*代表多个字符)//用于过滤。
     
     max@ubuntu:~/Documents$ ls
     matxt.txt  mbtxt.txt  mctxt.txt  mytxt.txt
     max@ubuntu:~/Documents$ ls m[a-h]txt.txt
     matxt.txt  mbtxt.txt  mctxt.txt
     max@ubuntu:~/Documents$ ls m[!a-x]txt.txt
     mytxt.txt
     
     ```

     

- 常用提示： ''ls -l -a'' 、ls-al''ll'' ,显示当前所有文件和文件夹及其所有属性。

- **cd** : 切换目录

     ​		cd - ：返回上次操作的目录。

     ​		cd !$ : 执行上一条命令的最后一条地址。

- **cp** ：拷贝文件或文件夹 （cp可以更新文件修改时间，但会覆盖文件信息）

     ​	常用方式：cp -i  :    cp   1.txt   2.txt   (用1.txt  覆盖 2.txt)     cp  -i  1.txt  2.txt   覆盖之前询问  ，是否  overwirte

     -R/r：递归处理，将指定目录下的所有文件与子目录一并处理。即复制多个文件，包含文件夹。

     cp	路径	路径

     cp	源文件	目标文件

     cp	路径	目标文件

     cp	源文件	路径

      

- **!$** : 执行上一条命令的最后一条地址。（cd  + !$）

- "**man"+ "command**"：命令介绍

- **gedit**: 文件查看程序。（linux软件）

- 注意区分：    1. /Documents/doc  : 绝对路径
     	2. Documents/doc   : 相对路径
           						3. ./Documnets/doc  : 当前目录

- ***，？**：文件扩展匹配符。 dsaf

- 元字符通配符。[ ]

- **touch** : 创建一个新的空文件。（touch 可以更新一个文件的最后修改时间而不改变文件内容）

- **pwd** ： 输出当前文件夹的绝对路径。

- **rm -i** : 删除文件时，提醒用户是否确认删除。

- **sudo rm -i -rf  /*** :遍历删除文件，（危险，切勿轻易使用） u'

     ​	使用rm命令，删除的文件无法恢复。（不同于windows） 

- **mkdir** : 创建文件夹。

- **rmdir :** 删除文件夹。

- **file** : 用来探测给定文件的类型。file命令对文件的检查分为文件系统、魔法幻数检查和语言检查3个过程。



- **cat** : 查看文件。
- **less** ： 查看文件，可翻页。（上下）
- **more** ：查看文件，可翻页。（下）
- **tail** ：查看文件，显示文件最后两行。
- **head** : 查看文件，显示文件前十行。
- **sort** ：将文件中的内容排序之后在命令行中进行展示。



#### System Command

-  **|** : 命令并行执行符。
- **top** ：显示管理器。
- **grep** ：利用正则表达式的文本搜索工具。
- **ps**（重要） ： 输出终端运行程序。
		  1. ps -aux | grep xxxxx :  显示xxxxx进程的详细信息
- **kill** ： kill + PID 强制停止进程。
- **df** ： 显示磁盘相关信息。
- **du**：显示每个文件和目录的磁盘使用空间。
- **du -h** ：常用。
- **sort** :对文本文件中所有行进行排序。
		1. sort - M :按照月份排序。
		2. sort - n ：根据数字排序。
		3. sort -r : 将结果倒序排序。
- **sudo fdisk -l** : 按列表方式显示磁盘分区。
- **mount**：用于挂载Linux系统外的文件和硬件，例如U盘。
- **umount**： 用于卸载已挂载的文件或硬件。
- **source** ： 在当前Shell环境中从指定文件读取和执行命令。（在修改配置文件后，使用source 使修改后的配置文件）



#### Linux挂载

挂载软盘时，Linux默认目录为User/media

- 新建一个挂载映射到一个新的文件夹。 



#### Linux打包压缩

##### tar/tar.gz格式 

​		tar是在Linux中使用得非常广泛的文档打包格式。它的好处就是它只消耗非常少的CPU以及时间去打包文件，它仅仅只是一个打包工具，并不负责压缩。另一种说明是将许多文件一起保存至一个单独的磁带或磁盘归档，并能从归档中单独还原所需文件。
打包与压缩是两种概念。打包是指将一个文件目录打包成一个文件，并不会减小产生的文件的大小。压缩是指将一个单独的文件通过压缩算法减小其大小。

1. *打包一个文件*：

```shell
  tar -cvf newfilename.tar filename 
```

  （-c参数是建立新的存档，-v参数详细显示处理的文件， -f参数指定存档或设备,newfilename.tar是指压缩之后的文件名称，filename是指要压缩的文件名称）

2. *压缩已打包的目录*：

```shell
gzip filename.tar    --------filename.tar.gz
```

（ilename.tar.gz压缩文件名称）

3. *如何解压一个XXXX.tar.gz文件为一个XXXX.tar文件*：

   ```shell
   gzip -d filename.tar.gz  
   ```

   (解压为打包文件)

4.*将打包文件解包*：

- 解开在当前目录下面：

  ```shell
  tar -xvf filename.tar   
  ```

  （解包为多文件，filename是指要解包的文件名称）

- 解包到指定的路径： tar -xvf filename.tar -C newdir     （filename是指要解包的文件名称，newdir为指定路径，注意此处解包的参数是大写C，不是小写c）


##### zip格式

1. *压缩一个zip文件*：

```shell
 zip -r newfilename.zip filename  
```

 （-r是压缩文件,newfilename.zip是指压缩之后的文件名称，filename是指要压缩的文件名称）
zip可能是目前使用的最多的文档压缩格式。**优点**：可以在不同的操作系统平台上使用。**缺点**：支持的压缩率不是很高。而tar.gz和tar.bz2在压缩率方面做得非常好。




#### 	父子shell

1. 父子shell的一种实例： 在一个bash shell终端下，执行一次bash，即创建一个子shell 。创建子shell 可以嵌套，即类似与oop编程语言中的子类。

2. **ps  --forest**    or **ps f**：用ASCII字符显示树状结构，表达程序间的相互关系。 

3. ":" : 分号作为命令的分隔符，可以使用分号进行多命令单行执行。

```shell
ls ; pwd ; cd /  	
```

4. 用括号的方式在同一行执行多条命令：

```shell
(ls ; pwd ; cd /)
```

		此用法与不加括号结果一致但此用法是创建一个子shell 之后再执行命令。

5. **echo  $BASH_SUBSHELL** : 输出 此命令所产生的子shell个数。

6. **sleep**： 将当前行为推迟执行。单位：秒。

```shell
sleep 10  // 等待10秒
sleep 10& // 在后台等待10秒
```

7. **jobs** ：列出当前后台作业进程。

8. c**oproc xxxx { commomd ; commomd ; } &** : 创建一个子shell并用子shell 执行大括号中的命令。（注意： 大括号中的命令必须与大括号之间空出一格。&符也必须与大括号空出一格。）

     coproc 命令解释：  https://www.geeksforgeeks.org/coproc-command-in-linux-with-examples/
     
9. **type** ： 查看命令为外部命令还是内建命令。

     - 外部命令：bash shell 通过创建与其本身同级别的进程来执行的命令。
     - 内建命令：内建命令不会产生新的进程来执行。
     
10. **！！**：执行上一条命令。

11. **！+ history 编号** ： 执行所指向的命令。

12. **alias** ： 别名。

```shell
ubuntu@Dsaktop-MaxCroft:~$ alias li='ls -li '
ubuntu@Dsaktop-MaxCroft:~$ li
total 0
281474977266367 drwxr-xr-x 1 ubuntu ubuntu 4096 Nov 18 17:23 Documents
```

 注意： alias 只能将命名后的命令保存在内存中，关闭重新打开终端后无效。

#### Environment Variables

**环境变量**： 环境变量的作用是提前告诉系统你能用到的程序的地址，以确保在任何位置系统都可以找到你所要使用的程序。

- 全局变量：无论在任何位置都可执行的环境变量，对整个系统有效。
- 局部变量：限定在某一部分地址的环境变量。



1. **printenv**:  输出环境变量。

```shell
ubuntu@Dsaktop-MaxCroft:~$ printenv
SHELL=/bin/bash
WSL_DISTRO_NAME=Ubuntu-20.04
NAME=Dsaktop-MaxCroft
PWD=/home/ubuntu
LOGNAME=ubuntu
MOTD_SHOWN=update-motd
HOME=/home/ubuntu
LANG=C.UTF-8  ...

ubuntu@Dsaktop-MaxCroft:~$ printenv USER
ubuntu
```

2. echo $HOME : 输出环境变量HOME的地址。

		*注释：$+环境变量地址名 使用时可以替换其指代的地址。*

(PATH例外：PATH 并不是一个单独的路径，而是一个路径的集合)

3. 定义用户局部变量： 当输出一个未被定义的变量时，系统输出为空。此时可以使用   **变量名=“变量值”** 定义一个用户局部变量。定义之后便可以输出和替换指代地址。

	注意：变量名可任意，除shell保留关键字。

4. 定义用户全局变量：当输出一个违背定义的变量时，系统输出为空。可以使用  **export 变量名="变量值"** 定义一个用户全局变量。定义之后可以输出和替换指代地址。

- ***（强制）定义变量时，用户变量用小写，系统变量用大写，单词之间用下划线隔开。***
- 设定用户局部变量时，只在局部生效。例如在子shell中定义的用户变量在父shell中无法使用，如下。（退出一个已创建的子shell时，子shell会销毁。）
- 设定用户全局变量时，在用户全局范围内生效，即在用户的全局范围内有效。

	示例1：定义用户局部变量

```shell
ubuntu@Dsaktop-MaxCroft:~$ bash
ubuntu@Dsaktop-MaxCroft:~$ echo $max

ubuntu@Dsaktop-MaxCroft:~$ max="croft"
ubuntu@Dsaktop-MaxCroft:~$ echo $max
croft
ubuntu@Dsaktop-MaxCroft:~$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
ubuntu     151   150  0 23:05 tty1     00:00:00 -bash
ubuntu     166   151  0 23:05 tty1     00:00:00 bash
ubuntu     174   166  0 23:06 tty1     00:00:00 ps -f
ubuntu@Dsaktop-MaxCroft:~$ exit
exit
ubuntu@Dsaktop-MaxCroft:~$ echo $max

ubuntu@Dsaktop-MaxCroft:~$
```

​		示例2:定义用户全局变量

```shell
ubuntu@Dsaktop-MaxCroft:~$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
ubuntu     157   156  0 15:43 tty1     00:00:00 -bash
ubuntu     172   157  0 15:43 tty1     00:00:00 ps -f
ubuntu@Dsaktop-MaxCroft:~$ echo $max

ubuntu@Dsaktop-MaxCroft:~$ export max="croft"
ubuntu@Dsaktop-MaxCroft:~$ echo $max
croft
ubuntu@Dsaktop-MaxCroft:~$ bash
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@Dsaktop-MaxCroft:~$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
ubuntu     157   156  0 15:43 tty1     00:00:00 -bash
ubuntu     173   157  0 15:43 tty1     00:00:00 bash
ubuntu     181   173  0 15:43 tty1     00:00:00 ps -f
ubuntu@Dsaktop-MaxCroft:~$ echo $max
croft
ubuntu@Dsaktop-MaxCroft:~$ exit
exit
ubuntu@Dsaktop-MaxCroft:~$ echo $max
croft
ubuntu@Dsaktop-MaxCroft:~$ bash
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@Dsaktop-MaxCroft:~$ echo $max
croft
ubuntu@Dsaktop-MaxCroft:~$
```

5. 删除变量：**unset  变量名**  ，在一定范围内删除变量。（在子shell中删除的用户全局变量在其父shell中仍然可以使用）



6. **关于如何永久修改环境变量：**  

- linux 中，开机是通过**启动文件**来打开shell，确保系统能进性命令操作。开机时，系统默认执行环境变量。

- /etc/profile ：linux  中最重要的文件 

- ```shell
  ubuntu@Dsaktop-MaxCroft:~$ cat /etc/profile
  # /etc/profile: system-wide .profile file for the Bourne shell (sh(1))
  # and Bourne compatible shells (bash(1), ksh(1), ash(1), ...).
  
  if [ "${PS1-}" ]; then
    if [ "${BASH-}" ] && [ "$BASH" != "/bin/sh" ]; then
      # The file bash.bashrc already sets the default PS1.
      # PS1='\h:\w\$ '
      if [ -f /etc/bash.bashrc ]; then
        . /etc/bash.bashrc
      fi
    else
      if [ "`id -u`" -eq 0 ]; then
        PS1='# '
      else
        PS1='$ '
      fi
    fi
  fi
  
  if [ -d /etc/profile.d ]; then
    for i in /etc/profile.d/*.sh; do
      if [ -r $i ]; then
        . $i
      fi
    done
    unset i
  fi
  ```

  

###  软件安装

1. **package managements sysytem**: 包管理系统，简称  **PMS** ，wiki中解释到 ：

    **软件包管理系统**是在电脑中自动安装、配制、卸载和升级[软件包](https://zh.wikipedia.org/wiki/软件包)的工具组合，在各种[系统软件](https://zh.wikipedia.org/wiki/系统软件)和[应用软件](https://zh.wikipedia.org/wiki/应用软件)的安装管理中均有广泛应用。

*在Linux发行版中，几乎每一个发行版都有自己的软件包管理系统*。常见的有：

- 管理[deb](https://zh.wikipedia.org/wiki/Deb)软件包的[dpkg](https://zh.wikipedia.org/wiki/Dpkg)以及它的[前端](https://zh.wikipedia.org/wiki/前端)[APT](https://zh.wikipedia.org/wiki/APT)（使用于[Debian](https://zh.wikipedia.org/wiki/Debian)、[Ubuntu](https://zh.wikipedia.org/wiki/Ubuntu)）。
- [RPM包管理员](https://zh.wikipedia.org/wiki/RPM套件管理員)以及它的前端[dnf](https://zh.wikipedia.org/wiki/DNF_(软件))（使用于[Fedora](https://zh.wikipedia.org/wiki/Fedora_(作業系統))、[Red Hat Enterprise Linux](https://zh.wikipedia.org/wiki/Red_Hat_Enterprise_Linux) 8、[CentOS](https://zh.wikipedia.org/wiki/CentOS) 8）、前端[yum](https://zh.wikipedia.org/wiki/Yum)（使用于[Red Hat Enterprise Linux](https://zh.wikipedia.org/wiki/Red_Hat_Enterprise_Linux)、[CentOS](https://zh.wikipedia.org/wiki/CentOS)）、前端[ZYpp](https://zh.wikipedia.org/wiki/ZYpp)（使用于[openSUSE](https://zh.wikipedia.org/wiki/OpenSUSE)）、前端[urpmi](https://zh.wikipedia.org/wiki/Urpmi)（使用于[Mandriva Linux](https://zh.wikipedia.org/wiki/Mandriva_Linux)、[Mageia](https://zh.wikipedia.org/wiki/Mageia)）等。

2. 工具依赖。 

#### Ubuntu 工具

2. apt：
3. apt-get:

#### RedHat 工具

1. yum：



#### 第三方软件

示例： The fuck： 





### Linux用户与权限

*在linux中用户分为三类：*

**超级用户：**（root，UID=0），UID为0的用户就是超级用户

**普通用户：**（UID=500~60000），可以使用useradd  添加的用户

**伪用户：**（UID=1~499）

例如：yuanhongx:3:3:root:/root:/bin/bash，如果我们把UID  3 改为0，那么下次我们登陆yuanhong这个用户时，就是超级用户，在终端命令行中就显示的是#号。



**伪用户**
**伪用户分为两种**

一、**与系统相关**：比如有些伪用户是与系统的某些操作相关（比如关机，重启等等，会调用伪用户的身份）。在linux里面，任何一个进程操作都要有一个用户身份，这就需要调用伪用户。

二、**与程序服务相关**：比如apache，启动之后也要对应一个伪用户。

伪用户的最大作用会是在系统操作或应用服务的时候调用的一个用户身份而已，在一定程度上起到一定的安全作用。

伪用户的特点：不能登陆系统、没有宿主目录

- /etc/passwd  存储密码的文件。
- /etc/shadow  密码实际存储文件。

1. useradd： 添加用戶。
2. userdel ： 删除用户。
3. usermod： 
4. sudo passwd + 用户名 ： 修改有用户密码。
5. sudo chpasswd ： 修改用户密码。
6. chsh ：
7. chfn ：



#### Linux groups

Linux 小组的作用： 共享资源的权限。

- /etc/group : 组的保存位置。

- Ubuntu 默认为每个用户单独创建一个组。（发行版各有特色）

  

1. groupadd :创建组。
2. groupmod ：修改组的设置。
2. **chmod** （重要）： 



####  文件属性权限

![img](https://www.runoob.com/wp-content/uploads/2014/06/file-llls22.jpg)



![363003_1227493859FdXT](https://www.runoob.com/wp-content/uploads/2014/06/363003_1227493859FdXT.png)

**第一位为文件目录，后九位三位一组显示操作权限。第一组为，文件创始者权限；第二组：与文件创始者同组的成员权限；第三组： 与文件创始者不同组的成员权限。**



### VIM

- 普通模式（命令操作模式）： 操作文件。
- 插入模式（编辑模式）： 编辑文件时。
- 可视化模式：选择文本时。
- **切换到可视化模式**（visual）：普通模式下，按 **v** 切换到可视化模式   

​		*视图模式下，使用小写v进入时，光标可以停留任意一个字符，使用大写V进入时，光标可以选中任意一行。*

		1. 视图模式下，按 **G** 全选，按 **g** 普通选择。
		2. 视图模式下，按 **o** 跳跃到选中文本的首位或末位。
		3. 视图模式当中，可以使用各种光标跳跃命令。
		4. **control + v**： 矩阵选择。。

- **切换到插入模式**（insert）： 普通模式下，按  **i** 。(当页面左下角显示insert时，为插入模式)

- **切换到普通模式**： 插入模式下，按   ESC    退出到普通模式。

- **保存文件**：   “**:w**”  保存文件。“**:wq**” 保存并退出。

- **退出不保存**： ：q!  退出但不保存。

- **翻页** ：   **control + F** 向下一页  ；   **control + B**   向上一页 

  ​       		**control + E**  向下滚动一行 ； **control + Y** : 向上滚动一行 

  ​				**G**(大写)  翻到文件末尾。（注意： Linux中的命令仍然区分大小写）
  ​				**GG** 翻到文件开头。
  
- **光标的移动**：

 **H**  向左移动   **L** 向右移动  **J**  向下移动  **K** 向上移动

1.  **i**   在光标位置前插入； 
2.  **a**   在光标位置后插入；
3.  **o**   光标在某行的任意位置，直接enter到下一行输入
4.  **b**   向前跳跃到单词的首字母
5.  **e**  向后跳跃到单词的末尾
6.  **w**   向后跳跃整个单词包括其开头位置及末尾位置
7.  **shift + b/e/w**  联合操作
8.  **shift + 6   ^**   跳跃到本行开头
9.  **shift + 4 $**  跳跃到本行末尾
10.  **0**    光标跳跃到本行开头并包含一段空白字符（视图模式下0是选中补全）
11.  **{}**: 跳跃到大小括号前后
11.  **v** :选择（配合光标移动联合操作）
12.  **vaw**： 选中整个单词
13.  **vab**: 选中整个单词，和包含此单词的括号
14.  **vaB**: 选中整个单词包含大括号
15.  **va<** :选中整个单词包含尖括号
16.  **v shift + < > **: 行缩进
17.  **v shift + ~**: 切换选中文本大小写
18.  **vu**: 选中文本，全部转换成小写
19.  **vU**:选中文本，全部转换成大写
20.  **行号 + gg**: 在有行号的情况下，可以跳跃到指定行号。

- **删除，拷贝，粘贴，替换操作**

1.  **x**   删除光标所在位置的字符
2.  **dd**  删除一整行
3.  **u**   撤销上一步操作
4.  **dw**  删除当前所在光标往后的单词
5.  **R**   替换当前字符 为任意字符 
6.  **普通模式下，不建议使用Backspeace  和 Delete**
7.  **p**： 粘贴（dd（删除） 的东西也可以通过p粘贴出来）
7.  **y**：复制
7.  **yy**: 复制当前位置一整行。
8.  **yw**：复制一个单词
9.  **y$**: 从当前位置开始，复制整行
10.  **:s/第一段要查找的文字/需要替换的文本/g** : 在光标所在行，让规定字段替换成其他字段。
11.   **:%s/第一段要查找的文字/需要替换的文本/g** : 在全局范围内，让规定字段替换成其他字段。
12.  **:set number**: 显示行号。
13.  **:行号1，行号2s/第一段要查找的文字/需要替换的文本/g**:在规定行号范围内，让规定字段替换成其他字段。
14.  **:行号1，行号2s/第一段要查找的文字/需要替换的文本/gc**:在规定行号范围内，让规定字段替换成其他字段。(提示每个要替换的位置是否替换，或其他操作)



#### VIM的配置

vim的配置，以Ubuntu为例，需要在用户目录下创建一个 **.vimrc** 文件，在.vimrc中配置各项。

```shell
set syntax=on//设置语法高亮
set tabstop=4//设置tab为四位
set softtabstop=4
set number//显示行号
set enc=utf-8//设置文字编码为utf-8
set showmatch//设置括号匹配
```





------



## GUI

- X Windows : 类windows系统
- KDE : 桌面设计风格之一
- GNOME:专为Linux 的桌面设计风格。 
- Unity: **Unity** is a [graphical shell](https://en.wikipedia.org/wiki/Graphical_shell) for the [GNOME](https://en.wikipedia.org/wiki/GNOME) [desktop environment](https://en.wikipedia.org/wiki/Desktop_environment) originally developed by [Canonical Ltd.](https://en.wikipedia.org/wiki/Canonical_(company)) for its [Ubuntu operating system](https://en.wikipedia.org/wiki/Ubuntu),



------



## 快捷键

- Control  H : 从此位置删除。

- Control  F（右）: 光标往后移动。

- Control  B（左）: 光标往前移动。

- Control  T :移动此位置前面的字符到其他地方。

- Control  U :删除此字符之前的字符。

- Control  R: 搜索以前用过的命令。

- Control  K: 删除此字符之后的字符。

- Control  L: 清屏。

  



## Linux  发行版   

### Ubuntu LTS 版

   **LTS** 解释 ：https://linux.cn/article-12618-1.html  

