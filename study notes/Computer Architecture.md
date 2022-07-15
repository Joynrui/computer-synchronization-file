# Computer Organization and Architecture 

​																																			---*form ETH Zurich  苏黎世联邦理工*

## Four key direction 

1.   Fundamentally Secure/Reliable/Safe Architectures    安全，可靠，保险的基本结构
2.   Fundamentally Energy-Efficient Architectures      高效的基本结构
3.   Fundamentally Low-Latency and Predictable Architectures    底层，可预见的基本结构
4.   Architecture for AI/ML, Genomics, Medicine, Health      AI/机器学习，基因，药学，健康  



## How Computers Work



### The transformation hierarchy    转换层次

**problem --> Algorithm --> Program/Language --> Runtime system 运行时系统(VM,OS,MM) --> ISA(SW/HW Interface) --> Micro-architecture微架构 --> Logic逻辑门 --> Devices设备 --> Electrons电子元件** 

-   narrow view 狭义: Computer architecture contains  **SW/HW interface** and **Micro-architecture**.
-   Expanded view 广义:  From **Algorithm to devices**.

### ISA

Instruction Set Architecture 

## Algorithm

A Step-by-step procedure that is guaranteed to terminate where each step is precisely stated and can be carried out by a computer.

一个由计算机执行，保证每一个步骤都能被清晰地说明的程序。



Three characteristics

-   Finiteness   有限性 
-   Definiteness   确定性
-    Effective computability    有效计算性



## Memory Performance Attacks

Many Cores on chip, it's a trend. 



### Efficiency issues



Why is there any slowdown? 放缓

Why is there a disparity in slowdowns? 放缓不同步

How can we solve the problem if we do not want that disparity?



Why is slowdown important?

1.   We want to execute applications in parallel in multi-core systems  -> consolidate more and more (for efficiency)

-   Cloud computing
-   Mobile phones
-   Automotive systems 汽车系统

2.   We want to mix different types or applications together

-   those requiring QoS(Quality of service) guarantee(e.g., video, pedestrian detection步行记录)
-   those that are important but less so
-   those that are less important

3.   We want the system to be controllable and high-performance.可控且高效

     

-   Why the Disparity in slowdowns?

DRAM Memory Controller is **unfair**.

DRAM 处理请求时，会通过DRAM 存储控制器**不公平**地处理请求，运行速度快的进程DRAM加载速度快，运行速度慢的进程DRAM加载速度慢。





### DRAM Bank Operation  

DRAM 库操作

![image-20220714143334959](C:\Users\MaxCroft\AppData\Roaming\Typora\typora-user-images\image-20220714143334959.png)

This view of a bank is an abstraction.  (The bank means 存储库.)

Internally, a bank consists of many cells (transistors 晶体管 && capacitors 电容器) and other structures that enable access to cells.

![image-20220714144605800](C:\Users\MaxCroft\AppData\Roaming\Typora\typora-user-images\image-20220714144605800.png)

When you put a request on DRAM, this request will be saved as a coordinate(坐标) like  (column, row).  Here, the request will be decoded with Row Decoder, then the row will be activated and put into the Row Buffer.  Finally, the request will go through the column mux(列复用选择器), and the data will be loaded. 

At the same time, if we want to load the second data request, and the row number is the same as the row number of the first request, the request will skip the row buffer and be sent directly to the column multiplexer. **The reason is that row has been activated.**

 **row buffer 有 预装载， 激活， 列访问 三种功能。** 如何缓冲区没有任何内容，则缓冲区只需要一个列访问，三种功能都有不同的延迟。

**DRAM Controllers**

-   A row-conflict memory access takes significantly longer than a row-hit access. 内存冲突访问比行命中访问花费的时间长的多。
-   Current controllers take advantage of this fact
-   Commonly used scheduling policy (*FR-FCFS*)[Rixner 2000]*
    -   Row-hit first: Service row-hit memory accesses first
    -   Oldest-first: Theb service older accesses first
-   The scheduling policy aims to maximize DRAM throughput.(吞吐量)

​			增大吞吐量实际上时把buffer变小，因为在使用

*Rixner et al., "Memory Access Scheduling," ISCA 2000.*



**The Problem**

-   Multiple applications share the DRAM controller

-   DRAM controllers designed to maximize DRAM data throughput

-   DRAM scheduling policies are unfair to some applications    DRAM 调度策略对某些应用程序不公平

    -   Row-hit first: unfairly prioritizes apps with high row buffer locality

        ​							不公平地优先考虑具有高行缓冲区位置的应用程序		

        -   Threads that keep on accessing the same rowd

            继续访问同一行的线程

    -   Oldest-first: unfairly prioritizes memory-intensive applications

        ​							不公平地优先考虑内存密集型应用程序

-   DRAM controller vulnerable to denial of service attacks

    -   Can write programs to exploit unfairness
