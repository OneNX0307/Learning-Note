# Access Modifiers

[TOC]

> You can use access modifiers for classes, attributes, and methods.



## Class

### public

```java
public class Vehicle{
  //statements here
}
```

> `public`: the class is accessible by any other class. 

### default

```java
class MyClass{
  //statements here
}
```

> The class is accessible only by classes in the same package.

## Attributes & Methods

### default

> Available to any other class in the same package.

### public

> Accessible from any other class.

### protected

> Make the members visible only to the subclass.

### private

> Accessible only within the declared class itself. It's a best practice to keep the variables within a class private.



