# Arrays

An array is collection of variables of the same type.

## Declare

To declare an array:

```java
int[] arr;
```

## Capacity

Define the array's capacity or the number of elements it  will hold.

```java
int[] arr = new int[];
```

## Assignment

```java
arr[2] = 43
```

## Initializing

Place the values in a comma-separated list, enclosed in curly braces.

```java
String[] myNames = {"A", "B", "C", "D"};
System.out.println(myName[2]);

//Outputs "C"
```

## Summing Elements in Arrays

```java
int[] intArr = {6, 42, 3, 7};
int sum = 0;
for(int i = 0; x < myArr.length; x++){
  sum += myArr[x];
}
System.out.println(sum);
//Outputs 58
```

## Enhanced for loop

```java
int[] primes = {2, 3, 5,7};
for(int t: primes){
  System.out.print(t);
}
/*
2
3
5
7
*/
```

## Multidimensional Arrays

```java
int[][] sample = {{1, 2,3}, {4, 5, 6}};
int x = sample[1][0];
System.out.println(x);
//Outputs 4
```

 