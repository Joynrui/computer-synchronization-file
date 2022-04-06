# Data structure and algorithm 



##  引论

### 1. 递归

1. **基准情况**：在第一次不进行递归运算时，基本情况作为递归运算的终结条件必须存在。即必须要有某种基本的情形，它们不用递归就能求解。数学中，例如数列起始项 a1。
2. **不断推进**：对于要进行递归运算的情形，递归必须总能够朝着一个基准情况推进。
3. **设计合法**：假设所有的递归调用都能运行。
4. **合成效益法则**：compound interest rule.



### 2. 泛型

​	参数化类型：将原来具体的类型参数化类似方法中的变量参数，此时类型也可以定义成参数形式，在调用时才传入具体的参数。

​	Java的基本思想是通过Object超类来实现泛型类（不仅限于Object类）。



------



## 算法分析

### 2.1 mathematical foundations

***principle 1***：如果 
$$
T_1(N) = O(f(N))  
$$
​		且
$$
T_2(N) = O(g(N))
$$
​		那么，

**（a）**
$$
T_1(N) + T_2(N) = O(f(N) + g(N))
$$
​		直观的和非正式地可以写成
$$
max(O(f(N)),O(g(N)))
$$
**(b)** 
$$
T_1(N) * T_2(N) = O(f(N) * g(N))
$$

------

***principle 2***: 如果
$$
T(N)
$$
是一个k次多项式，则
$$
T(N) = θ(N^k)
$$


------

***principle 3***: 对任意常数k，
$$
log^kN = O(N)
$$
这意味着对数增长的非常缓慢。

------



### 2.4 运行时间计算

**2.4.2. 一般法则**

*法则1*：**for loop**

​		一个for循环的运行时间至多是该for 循环内部的语句（包括测试）的运行时间乘以迭代次数。



*法则2*：**嵌套for循环**

​		从里面向外分析这些循环。在一组嵌套循环内部的一条语句总的运行时间为该语句的运行时间乘以该组所有的for循环的大小的乘积。

eg:下列程序的时间复杂度为*O*(N^2)

```java
public class Test{
    public static void main(String[] args) {
        int k;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++) {
                k++;
            }
        }
    }
}
```



*法则3* ：sequential statement 

​		将各个语句的运行时间求和即可。（即其中的最大值就是所得运行时间。[reason: 忽略级次较小的时间]）如下代码的运行时间为
$$
O（N^2）
$$


```c
#include<stdio.h>
int main(void)
{
    int array[5] = {12,34,34,23,98};
    for (int i = 0; i < n; i++)
    {
        a[i] = 0;
    }
    
    for (int i = 0; i < n; i++) 
    {
        for (int j = 0; j < n; j++) 
        {
            a[i] = a[j] + i + j;
        }
    }
    return 0;
}
```

​		

