# Class and Objects

[TOC]

## OOP

Object_Orientation_Programming. A programming style that is intended to make thinking about programming closer to thinking about the real world.

## Class

> A class describe what the object will be, but is separate from the object itself. It can be describe as a

- blueprint
- description
- definition

> for an object.

### Create

```java
//declare a bark() method in our Animal class.

public class Animal{
  void bark(){
    System.out.println("Woof-Woof");
  }
}
```



## Object

Each object has three dimensions:

- Identity

> The object name

- Attributes

> An attribute describes the current state of an object.

- Behavior

> What the object is capable of doing.

### Create Objects

```java
class MyClass{
  public static void main(String[] args){
    Animal dog = new Animal();
    dog.bark();
  }
}
//Outputs "Woof-Woof"
```

### Define Attributes

```java
public class Vehicle{
  //define some attributes
  int maxSpeed;
  int wheels;
  String color;
  double fuelCapacity;
  
  //define a method named horn
  void horn(){
    System.out.println("Beep!");
  }
}
```



## Method

Method defines behavior. A method is a collection of statements that are grouped together to perform an operation.

- Declare & Call

```java
class MyClass{
  static viod sayHello(){
    System.out.println("Hello World!");
  }
  
  public static void main(String[] args){
    sayHello();
  }
}
//Outputs "Hello World!"
```

- Parameters

```java
class MyClass{
  static void sayHello(String name){
    System.out.println("Hello" + name);
  }
  
  public static void main(String args){
    sayHello("Alfred");
  }
}
//Outputs "Hello Alfred"
```

- Return

```java
class MyClass{
  //return an int value
  static int sum(int val1, int val2){
    return val1 + val2;
  }
  
  public static viod main(String args){
    int x = sum(2, 5);
    System.out.println(x);
  }
}
//Outputs "7"
```

