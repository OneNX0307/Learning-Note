# Difference  between `i++` & `++i` in Java

## Prefix & Postfix

Two forms, prefix and postfix, may used with both the increment and the decrement operators. With prefix form, the operator appears before the operand, while in postfix form, the operator appears after the operand. Below is an explanation of how two forms work:

- **Prefix** 

  Increment the variable's value and uses the new value in the expression.

```java
int x = 34;
int y = ++x; //y is 35
```

The value of x is first incremented to 35, and is the assigned to y, so the values of both x and y are now 35.

- **Postfix**

  The variable's value is first used in the expression and is then increased.

```java
int x = 34;
int y = x++; //y is 34
```

x is first assigned to y, and is then incremented by one. Therefore, x becomes 35, while y is assigned the value of 34.