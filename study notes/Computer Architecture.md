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

1.   We want to execute applications in paraallel in multi-core systems  -> consolidate more and more (for efficiency)

-   Cloud computing
-   Mobile phones
-   Automotive systems 汽车系统

2.   We want to mix different types or applications together

-   those requiring QoS(Quality of service) guarantee(e.g., video, pedestrian detection步行记录)
-   those that are important but less so
-   those that are less important

3.   We want the system to be controllable and high performance.可控且高效

     
