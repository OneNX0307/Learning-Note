# Constructors

> A constructor can be used to provide initial values for object attributes. A constructor: 
>
> - name must be same as its class
> - must have no explicit return type

```java
public class Vehicle{
  private String color;
  Vehicle(){
    color = "red";
  }
}
//The Vehicle() method is the constructor of our class, so whenever an object of that class is crated, the color attribute will be set to "red".
```



```java
//Take parameters
public class Vehicle{
  private String color;
  Vehicle(String c){
    color = c;
  }
}

//use constructor
public class MyClass{
  public static void main(String[] args){
    Vehicle v = new Vehicle("blue");
  }
}
//This will call the constructor, which will set the color attribute to "blue".
```

```java
public class Vehicle{
  private String color;
}

//set the color attribute to a default value of "red"
Vehicle(){
  this.setColor("red");
}

//accept a parameter and assign it to the attribute
Vehicle(String c){
  this.setColor(c);
}

//Setter
public void setColor(String c){
  this.color = c;
}

//color will be "red"
Vehicle v1 = new Vehilce();
//color will be "green"
Vehicle v2 = new Vehicle("green");
```

