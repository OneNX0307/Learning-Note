# How to compile and run a java program?

## Step one

Write your **source code** with a **.java** extension. We name it as **ExampleProgram.java**

```java
class MyClass{
  public static viod main(String[] args){
    System.out.println("Hello World");
  }
}
```



## Step two

compile your source code with the command as following:

```shell
javac ExampleProgram.java
```

Then a **bytecode** file named with **ExampleProgram.class** will be generated

## Step three

Run your program:

```shell
java ExampleProgram
```

Then the windows will output the result

```shell
Hello World.
```





