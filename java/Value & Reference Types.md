# Value & Reference Types

## Value Types

> Value types includes
>
> - byte
> - short
> - int
> - long
> - float
> - double
> - Boolean
> - char
>
> These data types store the values assigned to them in the corresponding memory locations. So when you pass them to a method, you basically operate on the variable's value, rather than on the variable itself.

```java
public class MyClass{
  public static void main(String[] args){
    int x = 5;
    addOneTo(x);
    System.out.println(x);
  }

static void addOneTo(int num){
  num = num + 1;
  }
}
//Outputs "5"
```

## Reference Types

> Reference types includes
>
> - arrays
> - Strings
>
> A reference type stores a reference to the memory location where the corresponding data is stored. When you create an object  using the constructor, you create a reference value.