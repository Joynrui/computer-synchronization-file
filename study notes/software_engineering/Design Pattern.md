# Design Pattern

# Singleton Class

- Eager Initialization 主动初始化, Thread-safe

```java
public class Earth{
    private static Earth earthInstance = new Earth();
    // private constructor to prevent external instantiation
    private Earth(){}
    public static Earth getInstance() {
		return earthInstance;
    }
}
```

The instance is created as soon as the class is loaded, ensuring that the instance is always available when needed.


- Lazy Initialization 被动初始化, Thread-unsafe

```java
public class Earth{
    private static Earth earthInstance = new Earth();
    private Earth(){}
    public static Earth getInstance(){
        // If earthInstance doesn't exist, create a new Earth()
        if (earthInstance == null) {
            earthInstance = new Earth();
        }
        return earthInstance;
    }
}
```

In this situation,  the instance is created only when the `getInstance()` method is called for the first time. This can save resources if the instance is not always needed. However, it's important to note that this approach isn't thread-safe and might lead to issues in a multithreaded environment.



# Decorator Pattern

The Decorator Pattern used to expand a class, has the same effect as extending a class, but also the decorator pattern could expand a class dynamically. If you need new functions or parameters, you can use the Decorator Pattern and the original class will not be affected.

