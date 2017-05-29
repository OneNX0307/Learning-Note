# More on class

[TOC]

> There are 4 core concepts in OOP: 

- encapsulation
- inheritance 
- polymorphism
- abstraction

## Encapsulation

### Purpose

> To ensure that implementation details are not visible to users. The variables of one class will be hidden from the methods of the current class. This is called **data hidding**.

### How to 

> To achieve encapsulation in java, declare the class's variables as private and provide public **setter** and **getter** methods to modify and view the variables' values.

```java
class BankAccount{
  private double balance = 0;
  public void deposit(double x){
    if(x > 0){
      balance += x;
    }
  }
}
//This implemetation hides the balance variable, enabling access to it only through the deposit method.
```

### Benefits

- Control of the way data is accessed or modified
- More flexible and easily changed code
- Ability to change one part of the code without affecting other parts

## Inheritance

> Inheritance is the process that enable **subclass** class to acquire the properties(methods and variables) of **superclass**. When one class is inherited from another class, it inherits all of the superclass' **non-private** variables and methods.

### How to

> To inherit from a class, use the extends keyword.

```java
class Dog extends Animal{
  //some code
}
```

```java
//define a class Animal
class Animal{
  protected int legs;
  public void eat(){
    System.out.println("Animal eats");
  }
}

//define a subclass Dog inherited from Animal
//and the Dog class inherits the legs variable
class Dog extends Animal{
  Dog(){
    legs = 4;
  }
}

//create an instance in main and call the eat() method
class MyClass{
  public static void main(String[] args){
    Dog d = new Dog();
    d.eat();
  }
}
```

> Constructors are not member methods, and so are not inherited by subclass. However, the constructor of the superclass is called when the subclass is instantiated.

```java
class A{
  public A(){
    System.out.println("New A");
  }
}

class B extends A{
  public B(){
    System.out.println("New B");
  }
}

class Program{
  public static void main(String[] args){
    B obj = new B();
  }
}
/*Outputs
"New A"
"New B"
*/
```

## Polymorphism

```java
class Animal{
  public void makeSound(){
    System.out.println("Grr...");
  }
}

class Cat extends Animal{
  public void makeSound(){
    System.out.println("Meow");
  }
}

class Dog extends Animal{
  public void makeSound(){
    System.out.println("Woof");
  }
}

public static void main(String[] args){
  Animal a = new Dog();
  Animal b = new Cat();
}
```



## Overriding & Overloading

### Method Overriding

> Also known as **runtime polymorphism**

#### Rules

- Should have the same return type and arguments
- The access level cannot be more restrictive than the overridden method's access level
- A method declared final or static cannot be overridden
- If a method cannot be inherited , it cannot overridden
- Constructors cannot be overridden

```java
class Animal{
  public void makeSound(){
    System.out.println("Grr...");
  }
}

class Cat extends Animal{
  public void makeSound(){
    System.out.println("Meow");
  }
}
```



### Method overloading

> When methods have the same name, but different parameters, it is known as method overloading. Also known as **compile-polymorphism**.

```java
int max(int a, int b){
  if(a > b){
    return a;
  }
  else{
    return b;
  }
}

double max(double a, double b){
  if(a > b){
    return a;
  }
  else{
    return b;
  }
}
```



