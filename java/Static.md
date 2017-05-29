# Static

> When you declare a variable or a method as static it belongs to the class, rather than to a specific instance.

## Variable

```java
public class Counter{
  public static int COUNT = 0;
  Counter(){
    COUNT++；
  }
}

public static void main(String[] args){
  Counter c1 = new Counter();
  Counter c2 = new Counter();
  System.out.println(Counter.COUNT);	//Here the Counter in "Counter.COUNT" means the Counter class
}
//Outputs "2"
```

## Method

> The main method must always be static.

```java
public class Vehicle{
  public static void horn(){
    System.out.println("Beep")
  }
}


public class MyClass{
  public static void main(String[] args){
    Vehicle v1 = new Vehicle();
    Vehicle.horn();
  }
}
```

