# Getter & Setter

[TOC]

```java
public class Vehicle{
  private String color;
}

//getter: return the value of the attribute
public String getColor(){
  return color;
}

//setter: take a parameter and assigns it to the attribute
public String setColor(){
  this.color = c;
}
//Keyword this is used to refer to the current object.

//use getter and setter in main
public static void (String[] args){
  Vehicle v1 = new Vehicle();
  v1.setColor("red");
  System.out.println(v1.getColor());
}
//Outputs "red"
```

