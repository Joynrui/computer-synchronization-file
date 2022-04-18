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



## Lists, stacks, and queues 表、栈和队列  



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

链表为一系列节点组成，节点不必在内存中相连。每一个节点包含到该元素后面的节点的链，称next链。

**双链表：** 每一个节点都持有一个指向它在表中的前驱节点的链。



### 3.3  List in Collection API  



#### **3.3.2 Iterator Interface** 

The main advantage of the Iterator `remove` method is that collection `remove` should find the item which will be deleted. In some cases, the Iterator is more effective than the Collection.  We use Iterator when needed. However, if Iterator called its own remove method, this Iterator is legal.  



Notice： If you want to change the structure of the collection (like use add, remove, clear method), this collection will be illegal. (And it will throw a `ConcurrentModificationException` after this situation. )

 

#### **3.3.3 List Interface, ArrayList Class and LinkedList Class**



ArrayList class's advantage is that calls to get and set use constant time. But it's not effective in some situations. Such as adding the new items into the ArrayList, unless the change is made at the end of the ArrayList. And the LinkedList class provides a doubly-linked list implementation of the List ADT.

LinkedList class's advantage is that adding the new items and deleting the old items both have a small overhead(开销). (The default assumes that the position of the variable is known) It means that adding and deleting the items at the front of the LinkedList use operate in constant time.



### 3.4 The implementation of the ArrayList class



This is an example program as follows:

**MyArrayList**    *p47*

```java
package chapter3;

import java.util.Iterator;

/**
 * The implement of ArrayList class.
 */
public class MyArrayList<E> implements Iterable<E> {

    private static final int DEFAULT_CAPACITY = 10;

    private int theSize;
    private E[] theItems;

    public MyArrayList() {
        doClear();
    }

    public void clear() {
        doClear();
    }

    private void doClear() {
        theSize = 0;
        ensureCapacity(DEFAULT_CAPACITY);
    }

    public int size() {
        return theSize;
    }

    public boolean isEmpty() {
        return size() == 0;
    }

    // change array size
    public void trimToSize() {
        ensureCapacity(size());
    }

    public E get(int index) {
        if (index < 0 || index >= size()) {
            throw new ArrayIndexOutOfBoundsException();
        }
        return theItems[index];
    }

    public E set(int index, E newValue) {
        if (index < 0 || index >= size()) {
            throw new ArrayIndexOutOfBoundsException();
        }
        E old = theItems[index];
        theItems[index] = newValue;
        return old;
    }

    // initialize the arrayList size
    public void ensureCapacity(int newCapacity) {
        // Shrink the array size
        if (newCapacity < theSize) {
            return;
        }
        /*  It is unlawful to create generic array.
            We can create an array of generic type bounds and then use an array for type conversion.
            This will generate a compile warning, but is unavoidable in the implementation of generic collections.
        */
        E[] old = theItems;
        theItems = (E[]) new Object[newCapacity];
        for (int i = 0; i < size(); i++) {
            theItems[i] = old[i];
        }
    }

    // add method 1
    public boolean add(E x) {
        add(size(), x);
        return true;
    }

    // add method 2
    public void add(int index, E x) {
        if (theItems.length == size()) {
            ensureCapacity(size() * 2 + 1);
            for (int i = theSize; i > index; i--) {
                theItems[i] = theItems[i - 1];
            }
            theItems[index] = x;
            theSize++;
        }
    }


    public E remove(int index) {
        E removedItem = theItems[index];
        for (int i = index; i < size() - 1; i++) {
            theItems[i] = theItems[i + 1];
        }
        theSize--;
        return removedItem;
    }


    @Override
    public java.util.Iterator<E> iterator() {
        return new ArrayListIterator();
    }

    private class ArrayListIterator implements java.util.Iterator<E> {

        private int current = 0;

        @Override
        public boolean hasNext() {
            return current < size();
        }

        public E next() {
            if (!hasNext()) {
                throw new java.util.NoSuchElementException();
            }
            return theItems[current++];
        }

        public void remove() {
            MyArrayList.this.remove(--current);
        }
    }
}

```



#### 3.4.2 The Iterator and Java Nested and Inner Classes

1. *p50*

**postfix ++ operator** and **prefix ++ operator** used in `arr[idx]`   (`arr[++idx] arr[idx++]`)

2. *p50*

**package visibility** 



- Nested class  *p50*

Make the `ArrayListIterator` class a nested class, When we make `ArraylistIterator` a nested class, it is placed inside of another class (in this case `MyArrayList`) which is the **outer class**. We must use the word **`static`** to signify that it is nested; without **`static`**, we will get an inner class, which is sometimes good and sometimes bad.  

- Inner class *p51*

When you declare an inner class, the compiler adds an implicit reference to the outer class object that caused the inner class object's construction. If the name of the outer class is `Outer`, then the implicit reference is `Outer.this.` Thus if `ArrayListIterator` is declared as an inner class, without the static, then `MyArrayList.this` and `theList` would both be referencing the same `MyArrayList`. Thus `theList` would be redundant and could be removed.





------



### 3.5 Implementation of LinkedList

Doubly linked list 

These extra nodes are sometimes known as **sentinel nodes**; specifically, the node at the front is sometimes known as a **header node**;  and the node at the end is sometimes known as a **tail node**.



```java
package chapter3;

import java.util.ConcurrentModificationException;

/**
 * The implementation of the LinkedList
 */
public class MyLinkedList<T> implements Iterable<T> {


    // node generic class
    private static class Node<T> {
        public Node(T d, Node<T> p, Node<T> n) {
            data = d;
            prev = p;
            next = n;
        }

        public T data;
        public Node<T> prev;
        public Node<T> next;
    }

    public MyLinkedList() {
        doClear();
    }

    public void clear() {
        doClear();
    }

    private void doClear() {
        // Create a begin marker and a end marker.Set the size equals 0;
        beginMarker = new Node<T>(null, null, null);
        endMarker = new Node<T>(null, beginMarker, null);
        beginMarker.next = endMarker;

        theSize = 0;
        modCount++;
    }

    public int size() {
        return theSize;
    }

    public boolean isEmpty() {
        return size() == 0;
    }

    public boolean add(T x) {
        add(size(), x);
        return true;
    }

    public void add(int idx, T x) {
        addBefore(getNode(idx, 0, size()), x);
    }

    public T get(int idx) {
        return getNode(idx).data;
    }

    public T set(int idx, T newVal) {
        Node<T> p = getNode(idx);
        T oldVal = p.data;
        p.data = newVal;
        return oldVal;
    }

    public T remove(int idx) {
        return remove(getNode(idx));
    }

    /**
     * Add an item to this collection, at specified position p;
     * Items at or after that position are slid one position higher.
     *
     * @param p Node to add before
     * @param x any object
     * @thorws IndexOutOfBoundsException if idx is not between 0 and size().
     */
    private void addBefore(Node<T> p, T x) {
        /*
            This part can be short like this:

            1>
            Node newNode = new Node(x, p.prev, p);
            p.prev = p.prev.next = newNode;

            2>
            p.prev = p.prev.next = new Node(x, p.prev, p);

         */
        Node<T> newNode = new Node<>(x, p.prev, p);
        newNode.prev.next = newNode;
        p.prev = newNode;
        theSize++;
        modCount++;
    }

    /**
     * Remove the object contains in Node p;
     *
     * @param p the Node containing the object.
     * @return the item was removed from the collection.
     */
    private T remove(Node<T> p) {
        p.next.prev = p.prev;
        p.prev.next = p.next;
        theSize--;
        modCount++;

        return p.data;
    }


    /**
     * Gets the Node at position idx, which must range from 0 to size() - 1.
     *
     * @param idx idx index to search at.
     * @return internal node corresponding to idx.
     * @throws IndexOutOfBoundsException if idx is not
     *                                   between 0 and size() - 1, inclusive.
     */
    private Node<T> getNode(int idx) {
        return getNode(idx, 0, size() - 1);
    }

    /**
     * Gets the Node at position idx, which must range from lower to upper.
     *
     * @param idx   index to search at.
     * @param lower Lowest valid index.
     * @param upper Highest valid index.
     * @return internal node corresponding to idx.
     * @throws IndexOutOfBoundsException if id is not
     *                                   between lower and upper, inclusive.
     */
    private Node<T> getNode(int idx, int lower, int upper) {
        Node<T> p;

        if (idx < lower || idx > upper) {
            throw new IndexOutOfBoundsException();
        }

        if (idx < size() / 2) {
            p = beginMarker.next;
            for (int i = 0; i < idx; i++) {
                p = p.next;
            }
        } else {
            p = endMarker;
            for (int i = size(); i > idx; i--) {
                p = p.prev;
            }
        }

        return p;
    }

    public java.util.Iterator<T> iterator() {
        return new LinkedListIterator();
    }

    private class LinkedListIterator implements java.util.Iterator<T> {
        private Node<T> current = beginMarker.next;
        private int expectedModCount = modCount;
        private boolean okToRemove = false;


        @Override
        public boolean hasNext() {
            return current != endMarker;
        }

        public T next() {
            if (modCount != expectedModCount) {
                throw new java.util.ConcurrentModificationException();
            }
            if (!hasNext()) {
                throw new java.util.NoSuchElementException();
            }

            T nextItem = current.data;
            current = current.next;
            okToRemove = true;
            return nextItem;
        }

        public void remove() {
            if (modCount != expectedModCount) {
                throw new ConcurrentModificationException();
            }
            if (!okToRemove) {
                throw new IllegalStateException();
            }

            MyLinkedList.this.remove(current.prev);
            expectedModCount++;
            okToRemove = false;

        }
    }

    private int theSize;
    private int modCount = 0;
    private Node<T> beginMarker;
    private Node<T> endMarker;


}

```



------



### 3.6 The Stack ADT

#### 3.6.1 Stack Model

- Stack is sometimes known as **LIFO (last in, first out)** lists. 

- The general model is that there is some element that is at the top of the stack, and it is the only element that is visible.



#### 3.6.2 Implementation of Stacks



**Linked List Implementation of Stacks**



**Array Implementation of Stacks**





#### 3.6.3 Applications



- Balancing Symbols

- **Postfix Expressions**

Postfix notation, or reverse Polish notation, the easiest way to do this is to use the stack. When a number is seen, it is pushed onto the stack; when an operator is seen, the operator is applied to the two numbers(symbols) that are popped from the stack, and the result is pushed onto the stack. 

```java
package chapter3;

/**
 * Java program to evaluate value of a postfix
 * expression having multiple digit operands
 */


import java.util.Stack;

class PostfixExpression {
    // Method to evaluate value of a postfix expression
    public static int evaluatePostfix(String exp) {
        //create a stack
        Stack<Integer> stack = new Stack<>();

        // Scan all characters one by one
        for (int i = 0; i < exp.length(); i++) {
            char c = exp.charAt(i);

            if (c == ' ') {
                continue;
            }
                // If the scanned character is an operand(number here),
                // extract the number
                // Push it to the stack.
            else if (Character.isDigit(c)) {
                int n = 0;

                //extract the characters and store it in num
                while (Character.isDigit(c)) {
                    n = n * 10 + (int) (c - '0');
                    i++;
                    c = exp.charAt(i);
                }
                i--;

                //push the number in stack
                stack.push(n);
            }

            // If the scanned character is an operator, pop two
            // elements from stack apply the operator
            else {
                int val1 = stack.pop();
                int val2 = stack.pop();

                switch (c) {
                    case '+':
                        stack.push(val2 + val1);
                        break;

                    case '-':
                        stack.push(val2 - val1);
                        break;

                    case '/':
                        stack.push(val2 / val1);
                        break;

                    case '*':
                        stack.push(val2 * val1);
                        break;
                }
            }
        }
        return stack.pop();
    }

    // Driver program to test above functions
    public static void main(String[] args) {
        String exp = "100 200 + 2 / 5 * 7 +";
        System.out.println(evaluatePostfix(exp));
    }
}
```



##### Infix to Postfix Conversion (important)



- 几个注意事项

1. 中缀转后缀时，需要一个读取域、一个栈及一个输出域；
2. 读取域中存放将要被转换的中缀表达式（标准表达式）；
3. 数据去向基本路线：读取域 ------> 栈（停留或不停留） ------> 输出域；
4. 所有操作数都将从读取域经过堆栈并直接输出到输出域；
5. 运算操作符（即加减乘除等）从读取域被读取并进入堆栈；
6. 当堆栈为空时，读取到操作符时直接将操作符压入堆栈；
7. 当堆栈不为空时，**比较栈顶元素（栈顶操作符）与被读取（current）到的操作符的优先级（precedence），通过操作符的优先级判断即将进行的操作**；***若栈顶操作符的优先级低于被读取到的操作符的优先级，则不输出栈顶操作符，直接将读取到的操作符压入堆栈；若栈顶操作符的优先级高于被读取到的操作符的优先级，则先将栈顶操作符输出，再将被读取到的操作符压入堆栈***；

```java
Stack<E> stack = new Stack<>();
if (operatorStackTop.precedence() < operatorRead.precedence()) {
	stack.push(operatorRead);     
}

if (operatorStackTop.precedence() > operatorRead.precedence()) {
    outputField = operatorStackTop;
    stack.push(operatorRead);
}
```

8. 关于圆括号：圆括号进行特殊处理。一般而言，**（ 左括号具有最高优先级**，当进行压栈时，无论栈顶是什么操作符，（的优先级都是较高的；**当读取到一个）右括号时，将堆栈中（之上所有的操作符全部输出**，最终舍弃左右括号。



eg:

```java
package chapter3;

import java.util.Scanner;
import java.util.Stack;

public class InfixToPostfix {

    /**
     * Checks if the input is operator or not
     * @param c input to be checked
     * @return true if operator
     */
    private boolean isOperator(char c){
        if(c == '+' || c == '-' || c == '*' || c =='/' || c == '^')
            return true;
        return false;
    }

    /**
     * Checks if c2 has same or higher precedence than c1
     * @param c1 first operator
     * @param c2 second operator
     * @return true if c2 has same or higher precedence
     */
    private boolean checkPrecedence(char c1, char c2){
        if((c2 == '+' || c2 == '-') && (c1 == '+' || c1 == '-'))
            return true;
        else if((c2 == '*' || c2 == '/') && (c1 == '+' || c1 == '-' || c1 == '*' || c1 == '/'))
            return true;
        else if((c2 == '^') && (c1 == '+' || c1 == '-' || c1 == '*' || c1 == '/'))
            return true;
        else
            return false;
    }

    /**
     * Converts infix expression to postfix
     * @param infix infix expression to be converted
     * @return postfix expression
     */
    public String convert(String infix){
        System.out.printf("%-8s%-10s%-15s\n", "Input","Stack","Postfix");
        String postfix = "";  //equivalent postfix is empty initially
        Stack<Character> s = new Stack<>();  //stack to hold symbols
        s.push('#');  //symbol to denote end of stack

        System.out.printf("%-8s%-10s%-15s\n", "",format(s.toString()),postfix);

        for(int i = 0; i < infix.length(); i++){
            char inputSymbol = infix.charAt(i);  //symbol to be processed
            if(isOperator(inputSymbol)){  //if a operator
                //repeatedly pops if stack top has same or higher precedence
                while(checkPrecedence(inputSymbol, s.peek()))
                    postfix += s.pop();
                s.push(inputSymbol);
            }
            else if(inputSymbol == '(')
                s.push(inputSymbol);  //push if left parenthesis
            else if(inputSymbol == ')'){
                //repeatedly pops if right parenthesis until left parenthesis is found
                while(s.peek() != '(')
                    postfix += s.pop();
                s.pop();
            }
            else
                postfix += inputSymbol;
            System.out.printf("%-8s%-10s%-15s\n", ""+inputSymbol,format(s.toString()),postfix);
        }

        //pops all elements of stack left
        while(s.peek() != '#'){
            postfix += s.pop();
            System.out.printf("%-8s%-10s%-15s\n", "",format(s.toString()),postfix);

        }

        return postfix;
    }

    /**
     * Formats the input  stack string
     * @param s It is a stack converted to string
     * @return formatted input
     */
    private String format(String s){
        s = s.replaceAll(",","");  //removes all , in stack string
        s = s.replaceAll(" ","");  //removes all spaces in stack string
        s = s.substring(1, s.length()-1);  //removes [] from stack string

        return s;
    }

    public static void main(String[] args) {
        InfixToPostfix obj = new InfixToPostfix();
        Scanner sc = new Scanner(System.in);
        System.out.print("Infix : \t");
        String infix = sc.next();
        System.out.print("Postfix : \t"+obj.convert(infix));
    }
}
```





