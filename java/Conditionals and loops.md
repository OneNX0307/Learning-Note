# Conditionals and loops

## if

```java
if (condition){
  //Executes when the condition is true
}
```

| Comparison operators | meaning                  |
| -------------------- | ------------------------ |
| <                    | less than                |
| >                    | grater than              |
| !=                   | not equal                |
| ==                   | equal                    |
| <=                   | less than or equal to    |
| >=                   | greater than or equal to |

```java
int x = 7;
if(x < 42){
  System.out.println("Hi");
}
```

## if...else

```java
int age = 30;
if(age < 16){
  System.out.println)("Too young");
}else{
  System.out.println("Welcome!");
}
//outputs "Welcome!"
```

## else if

```java
int age = 25;
if(age <= 0){
  System.out.println("Error");
}else if(age <= 16){
  System.out.println("Too young");
}else if(age < 100){
  System.out.pirntln("Welcome!");
}else{
  System.out.println("Really?");
}
//outputs "Welcome!"
```

## while

```java
int x = 6;
while(x < 10){
  System.out.println(x);
  x++;
}
System.out.println("Loop ended");
/*
Outputs
6
7
8
9
Loop ended
*/
```

## for

- Syntax

```java
for (initilization; condition; increment/decrement){
  statement(s)
}
```



```java
for(int x = 1; x <= 5; x++){
  System.out.println(x);
}
/*
Outputs
1
2
3
4
5
*/
```

## do...while

```java
int x = 1;
do{
  System.out.println(x);
  x++;
}while(x < 5);
```

```java
int x = 1;
do{
  System.out.println(x);
  x++;
}while(x < 0);
//Outputs 1
```

## switch

```java
int day = 3;
switch(day){
  case 1:
    System.out.println("Monday");
    break;
  case 2:
    System.out.println("Tuesday");
    break;
  case 3:
    System.out.println("Wednesday");
    break;
}
//Output "Wednesday"
```

```java
int day = 3;
switch(day){
  case 6:
    System.out.println("Saturday");
    break;
  case 7:
    System.out.println("Sunday");
    break;
  defualt:
    System.out.println("Weekday");
}
//Output "Weekday"
//No break is needed in the default case, as it is always the last statement in the switch.
```

## Loop Control Statemnts

The break and continue statements change the loop's execution flow. The break statement terminates the loop and transfer execution to the statement immediately following the loop.

```java
int x =1;

while(x >0){
  System.out.println(x);
  if(x == 4){
    break;
  }
  x++;
}

/*Outputs
1
2
3
4
*/
```

The continue statement causes the loop to skip the remainder of its body and then immediately retest it condition prior to reiterating. In other words, it makes the loop skip to its next iteration.

```java
for(int x = 10; x <= 40; x = x + 10){
  if(x == 30){
    continue;
  }
  System.out.println(x);
}
/* Outputs
10
20
40
*/
```

