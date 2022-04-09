# Data structure and algorithm 



##  引论

### 1. 递归

1. **基准情况**：在第一次不进行递归运算时，基本情况作为递归运算的终结条件必须存在。即必须要有某种基本的情形，它们不用递归就能求解。数学中，例如数列起始项 a1。
2. **不断推进**：对于要进行递归运算的情形，递归必须总能够朝着一个基准情况推进。
3. **设计合法**：假设所有的递归调用都能运行。
4. **合成效益法则**：compound interest rule.



### 2. Generic 泛型

​	参数化类型：将原来具体的类型参数化类似方法中的变量参数，此时类型也可以定义成参数形式，在调用时才传入具体的参数。

​	Java的基本思想是通过Object超类来实现泛型类（不仅限于Object类）。



------



## ALgorithm analysis 算法分析

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



### 2.3 problem analysis

Sometimes, the time it takes to just read in the data from disk is likely orders of magnitude larger than the time required to solve the above problem. This is typical of many efficient algorithms. The reading of data is generally a bottleneck; once the data is read in, the problem is quickly resolved.





### 2.4 运行时间计算

#### **2.4.2 一般法则**

*principle1*：**for loop**

​		一个for循环的运行时间至多是该for 循环内部的语句（包括测试）的运行时间乘以迭代次数。



*principle*：**嵌套for循环**

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



*principle3* ：**sequential statement** 

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

*principle4*: **if / else statement**

```java
if(condition)
    S1
else
    S2
```

For the above program snippet, the running time of an if/else statement never exceeds the running time of the judgment plus the total running time of the longer running time in S1 and S2.





#### 2.4.3 最大子序列和问题的求解

共计四种典型算法，较为特别的是使用**“分治”**方法的算法，使用动态规划的算法。

**eg: 分治算法**  

时间复杂度：
$$
T(1) = 1
$$

$$
T(N) = 2T(N/2) + O(N)
$$

最终计算得：

若
$$
N = 2^k
$$
则
$$
T(N) = N * (k + 1) = Nlog N + N = O(N log N)
$$


```java
public class MaxSunRec {

    public static void main (String[] args) {
        int[] array = {123, -9, -63, 30, 56, -10, 3, 30};
        System.out.println(maxSumRec(array, 0, 7));

    }
    /**
     * Recursive maximum contiguous subsequence sum algorithm.
     * Finds maximum sum in subarray spanning a[left...right]
     * Does not attempt to maintain actual best sequence.
     * @param a
     * @param left
     * @param right
     * @return
     */
    private static int maxSumRec(int[] a, int left, int right) {
        // base case
        if (left == right) {
            if (a[left] > 0) {
                return a[left];
            } else {
                return 0;
            }
        }

        int center = (left + right) / 2;
        // left part
        int maxLeftSum = maxSumRec(a, left, center);
        // right part
        int maxRightSum = maxSumRec(a, center + 1, right);

        // center part
        int maxLeftBorderSum = 0;
        int leftBorderSum = 0;
        for (int i = center; i >= left; i--) {
            leftBorderSum += a[i];
            if(leftBorderSum > maxLeftBorderSum) {
                maxLeftBorderSum = leftBorderSum;
            }
        }

        int maxRightBorderSum = 0;
        int rightBorderSum = 0;
        for(int i = center + 1; i <= right; i++) {
            rightBorderSum += a[i];
            if ( rightBorderSum > maxRightBorderSum) {
                maxRightBorderSum = rightBorderSum;
            }
        }

        return max(maxLeftSum, maxRightSum, maxLeftBorderSum + maxRightBorderSum);
    }

    private static int max(int number1, int number2, int number3) {
        int maxNumber = (number1 > number2 ? number1 : number2) > number3 ?
                (number1 > number2 ? number1 : number2) : number3;
        return maxNumber;
    }
}
```



eg： algorithm 4  p30 

```java
// algorithm 4  Linear-time maximum contiguous sum algorithm.
    private static int maxSubSum4(int[] a) {
        int maxSum = 0;
        int thisSum = 0;

        for (int i = 0; i < a.length; i++) {
            thisSum += a[i];

            if (thisSum > maxSum) {
                maxSum = thisSum;
            } else if (thisSum < 0) {
                thisSum = 0;
            }
        }
        return maxSum;
    }
```



#### 2.4.4 logarithm in running time 

*如果一个算法用常数时间将问题的大小削减为其一部分（通常是1/2）， 那么该算法就是O(logN)。另一方面， 如果使用常数时间只是把问题减少一个常数的数量（如将问题减少1）， 那么这种算法就是O(N)的。*





------



## Lists, stacks and queues 表、栈和队列  



### 3.1 Abstract data type, ATD 抽象数据类型



### 3.2 List ATD 



#### 3.2.1 表的简单实现



**扩展数组方法 Extended array method**    

```java
// 初始化一个长度为10的数组
int[] arr = new int[10];
...
// 扩大数组
// 对数组进行扩大处理
int[] newArr = new int[arr.length * 2]; 
for (int i = 0; i < arr.length; i++) {
    newArr[i] = arr[i];
}
arr = newArr;

```



#### 3.2.2 Simple Linked List  简单链表

