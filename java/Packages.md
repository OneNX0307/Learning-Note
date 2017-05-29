# Packages

> A package  can be define as a group made of similar types of classes, along with sub-packages. Packages are used to avoid name conflicts and to control access to classes.

```java
//import Vehicle class from samples package
import MyClass.Vehicle
  
class MyClass{
  public static void main(String[] args){
    Vehicle v1 = new Vehicle();
    v1.horn();
  }
}
```



> The major results occur when a class is placed in a package.
>
> - the name of the package becomes a part of the name of the class;
> - the name of the package must match the directory structure where the corresponding class file resides.



```java
//import all classes in a package
import samples.*
```

