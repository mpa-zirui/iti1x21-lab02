
# ITI 1121 - Lab 02

## Submission

Please read the [junit instructions](JUNIT.en.md) for help
running the tests for this lab.

Please read the [Submission Guidelines](SUBMISSION.en.md) carefully.
Errors in submitting will affect your grades.

Submit your answers to

* Combination.java
* DoorLock.java

# Part 1: Data type convension

## Learning Objectives

* **Learning** about the concept of data type convension;
* **Differentiate** between explicit and implicit data conversion
* **Understand** when it is possible to force a type conversion without consequences on the accuracy of the result.

## Type conversion

As we have seen in the last lab, Java is a strongly typed language. It is sometime useful to convert a primitive type to another type. To do so, we need to be **very careful to not lose any information**. There are 2 types of conversion: **Explicit** and **implicit**

### Implicit conversion (no information loss)

The implicit conversions are those where there is no possible loss of information. They happen automatically when the program runs.

For example, when assigning a value to a variable, the conversion is implicit:

```java
float money;
int cash= 25;
money = cash;         // Converts from int to float
System.out.println (money);
```

This conversion is implicit because the conversion of an **integer** to a decimal **float** happens without any loss of information. We also note that the program prints "25.0". the ".0" comes from the fact that the **int** 25 is converted to a **float**

That is also what happens when a value of type **int** is assigned to a variable of type **long**. The type **long** also represents an integer but the range of value that it can have is far greater than the type **int**. The implicit conversion cannot be done in the opposite direction (**long** to **int**) because there are some values represented by a **long** that cannot be represented by an **int**. There is a lot of combination of primitive type conversion. You can find them in the [table](#tableau1) below.

There is a second case where the implicit conversion happens. It is the **arithmetic promotion**, which is when the **compiler** has to modify the type of one of the operand to do an operation.

For example:

```java
double num1 = 2.0;
int num2 = 6;
System.out.println (num2/num1);
```

In this example, the program prints 3.0. The variable "num2" is converted to **double** before the division.

For reference, there exist a list of rules that we can use to know the type of the operand when operations are used with

* `+`
* `-`
* `*`
* `/`
* `%`
* `<`
* `<=`
* `>`
* `>=`
* `==`
* `!=`

_To do in the following order:_

1.  If one of the operands is a **double**, the other is converted to a **double**
2.  If one of the operands is a **float**, the other is converted to a **float**
3.  If one of the operands is a **long**, the other is converted to a **long**
4.  In **any other case**, the two operands are converted to **int**

Note that there is not conversion for the type **boolean**.

The following table gives the list of conversions of **primitive type** without any **data loss**:

| From | To |
| --- | --- |
| byte | short, int, long, float, double |
| short | int, long, float, double |
| char | int, long, float, double |
| int | long, float, double |
| long | float, double |
| float | double |


### Explicit conversion / Cast

Explicit conversions are conversion where it is possible to lose data. To do it, we need to use the "cast" operator. It is 2 parentheses preceding a value, between the parentheses is the data type that we want to convert the value to.

For example:

```java
double d = 16.987;
float f = (float) d;   // Converts from double to float without any loss of data
int i = (int) f;      // Converts from float to int with loss of data
long l = (long) i;    // Converts from int to long without any loss of data
System.out.println (d);
System.out.println (f);
System.out.println (i);
System.out.println (l);
```

We get this output:

```java
16.987
16.987
16
16
```

In the output we can see that the decimal value ".987" is lost in the conversion from **float** to **int**. It is very important to be careful when doing this kind of conversion to make sure that any loss of data does not affect the output of our program. You will experiment more about this type of conversion in the next part of the lab.

## 2. Error messages

Through the semester, many ideas will be presented to you so that you learn to program more efficiently. One of the things that you will need to learn is: debugging. At first, students might have to spend a lot of time doing it, sometimes they will look at the wrong part of the code when trying to fix a mistake. We will come back to this in another lab. For now we will focus on the error messages. It is important to understand the error messages and to be familiar with each of them. To help you learn about them, I suggest that you create some small test programs that will show errors.

**Exercise!** Create a new class named **Test** with a main method. In the body of the main method, declare a variable of type **int** to which you will assign the value **Long.MAX_VALUE**. It is the biggest value of the type **long**.

<center><h3>What error message is displayed by the compiler?</h3></center>

Sometimes, depending on the logic of our program we might still want to do the conversion. If so, we need to be very careful. **Always use a test to make sure that the value of the expression is within the interval of the target type**. When we force a conversion (**cast**), we ignore the compiler’s check to see if the expression is uses compatible types. It is as if we tell the compiler "trust me I know what I’m doing; let me assign this value to the variable".

```java
long l;
...
if (l >= Integer.MIN_VALUE && l <= Integer.MAX_VALUE) {
  int i = (int) l;
  ...
}
```

Since the value of the variable `l` is within the possible interval for an **int**, why do we still need to force the conversion using the syntax _(int)_? Why can’t we simply write it like this:

```java
long l;
...
if (l >= Integer.MIN_VALUE && l <= Integer.MAX_VALUE) {
  int i = l;
  ...
}
```

The answer is quite simple: the compiler will never do an implicit conversion if there is the possibility of losing information! If you try it you will get this error message.

```java
Test.java:5: error: incompatible types: possible lossy conversion from long to int
             int i = l;
                     ^
1 error
```

Also, we can’t use the cast to transform an array of character (**String**) to a number! However, each **primitive type** has a **class "wrapper"**. This class has a name similar to the type to which it is associated. For example, for the type **int**, there is a class Integer (in the same way there is **Double, Boolean, Character**, etc). As the name indicates, each of these class **wrappers** are used to save a value within an **object** like this:

```java
public class Integer {
  private int value;

  public Integer(int v) {
   value = v;
  }
  ...
}
```

We will later see some example where theses object will be necessary (in the presentation of the abstract data type). However, an important aspect of these classes is that they regroup a number of methods useful for its type.

Take a look:

*  Go to [http://docs.oracle.com/javase/8/docs/api/overview-summary.html](http://docs.oracle.com/javase/8/docs/api/overview-summary.html)

It is documentation about the class and method of Java 8.0\. Through the session, you will need to reference this documentation in order to use its class and methods.

* Visit the package **lang**.

This is always loaded by default in your program (you do not need to use the import command). This is the package in which you will find the wrapper classes. You will also find the class System used to print to the console.

  * [http://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html](http://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html)

* Lower on this page, you will find the class **Integer**.
  * [http://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html](http://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)
* Now find the method **parseInt(String s)** and identify the type that it returns.

There are a lot of compilation error. These errors can be eliminated if you clearly understand the types and if you apply the **syntax rules** properly. The following table gives an overview of the most common compilation errors:

| ERROR MESSAGE | DESCRIPTION |
| --- | --- |
| `variable VARIABLE_NAME might not have been initialized` | You tried to use the variable VARIABLE_NAME without initializing it. Careful, it might have been a typo! |
| `';' expected` | A semi-colon was expected at the end of a line. |
| `cannot assign a value to a final variable VARIABLE_NAME` | You are trying to assign a value to a constant VARIABLE_NAME that was already initialized. |
| <pre>incompatible types<br>found: TYPE1<br>required: TYPE2</pre> | You are trying to assign a value of TYPE1 to a variable of type TYPE2 |
| <pre>cannot find symbol<br>symbol: WORD<br>location: LINE</pre> | The compiler finds a word that it does not understand. Make sure that it is not a typo. |
| `illegal start of expression` | The compiler finds an element that should not be there |
| `not a statement` | The line of code is not valid |
| <pre>reached end of file while parsing<br>}<br>\^</pre> | There is probably an error in your code block. Check your brackets {} |

In short, the error messages give you a lot of information (type and place of the error). Learn to read and understand these errors. This will help you to debug your code.

## Exercices!

What will be the output when compiling and running these programs?

## Question 1.21:

```java
 public class Test {
  public static void main ( String[] args ) {
    int num1 = 9 ;
    double num2 = 12.0;
    double sum = num1 + num2;
    System.out.println(sum);
  }
}
```

## Question 1.22:

```java
 public class Test {
  public static void main(String[] args) {
    double num1 = 18.4;
    double num2 = 1.6;
    int sum = num1 + num2;
    System.out.println(sum);
  }
}
```

## Question 1.23 :

```java
public class Test {
  public static void main(String[] args) {
    double num1 = 13.6;
    double num2 = 2.5;
    int sum = (int)num1 + (int)num2;
    System.out.println(sum);
  }
}
```

## Question 1.24 :

```java
public class Test {
  public static void main(String[] args) {
    double num1 = 13.6;
    double num2 = 2.5;
    int sum = (int)(num1 + num2);
    System.out.println(sum);
  }
}
```

## Question 1.25 :

```java
public class Test {
  public static void main(String[] args) {
    int num = 96;
    char a = num;
    System.out.println(a);
  }
}
```


## Question 1.26 :

```java
public class Test {
  public static void main(String[] args) {
    System.out.println( (float)(int)2017.89432 );
  }
}
```

## Question 1.27:

For this question, we will revisit the **main** method. As you already know, the main method as to contain the argument **String args[]**. This argument allows you to give data to you program as you start it. To do so, you need to pass the **"command-line arguments"** upon the invocation of your program like this:

```java
> java MyProgram one two
```

Where **args** now contains the strings "one" and "two". We can now use args like a regular array.

Example:

Now, create the class "Sum" that converts all the elements from the command line from **String** to **int**, and then do the **sum** of the elements.

_Hint: Use the method of the class "String" available in the Java documentation_

```java
> javac Sum.java
> java Sum 1 2 3 4 5
```

Your program should look like this:

```java
The sum is 15
```

You can watch the following video for a step by step explanation : [https://www.youtube.com/watch?v=38C2lJTbJNU](https://www.youtube.com/watch?v=38C2lJTbJNU)


# Part 2: Object oriented programming

## Objectives

* Implementing simple classes;
* Creating associations between classes;
* Explore further the notion of encapsulation.

For this part of the lab, you need to create 3 classes: **Combination**, **DoorLock** and **SecurityAgent**. We want to explore the concept of association between classes. So, an object of the class **DoorLock** has an instance variable of the type referring to an object of the class **Combination**. An object of the class **SecurityAgent** has a reference to an object of the class **DoorLock** and a reference to an object of the class **Combination**. This way, the object **SecurityAgent** and **DoorLock** both have access to the same object **Combination**.

In a class **Test**, we try to open the lock. This program tries to brute force the lock open using a combination of random numbers. In order for the program to find the right combination quickly, each number of the combination will be between 1 and 5 (inclusively). After three wrong tries, the lock will become unusable, we will need to ask the object **SecurityAgent** to reactivate it.

### Combination

You will hand in this exercise. Download and complete the starter file here:

* Combination.java

Implement a class, called **Combination**, to store three integer values (ints).

1. declare the necessary instance variables to store the three integer values;
2. create a constructor, public **Combination(int first, int second, int third)**, to initialize the values of this object.
3. implement the instance method **public boolean equals(Combination other)**, such that **equals** returns **true** if **other** contains the same values, in the same order, as this Combination; the order is defined by the order of the parameters of the constructor, given the following:

```java
 Combination c1, c2, c3;

 c1 = new Combination(1, 2, 3);
 c2 = new Combination(1, 2, 3);
 c3 = new Combination(3, 2, 1);
```

then **c1.equals(c2)** is **true** but **c1.equals(c3)** is **false**;

4.  finally, implement the method **public String toString()**, to return a **String** representation of this object, where the first, second and third values are concatenated and separated by ":" symbols. E.g.

```java
Combination c1;
c1 = new Combination(1, 2, 3);
System.out.println(c1);
```

**_displays "1:2:3"._**

The interface of the class **Combination** consists therefore of its **constructor**, the method **equals** and the method **toString**.

Ideally, the input data should be validated. In particular, all the values should be in the range 1 to 5\. However, since we do not yet have the tools to handle exceptional situations, we will assume (for now) that all the input data are valid!

**Note**: Simpler code is better and it is worthwhile spending time cleaning up code even if it was already working.

**Hint**: my implementation is approximately 20 lines long, not counting blank lines. This is not a contest to write the shortest class declaration. I am providing this information so that you can evaluate the relative complexity of the tasks.

### DoorLock

You will hand in this exercise. Download and complete the starter file here:

* DoorLock.java

Create an implementation for the class **DoorLock** described below.

1.  declare an integer constant, called **MAX_NUMBER_OF_ATTEMPTS**, that you will initialize to the value 3;
2.  instance variables. The class DoorLock must have the necessary instance variables to
  i.  store an object of the class **Combination**
  ii.  to represent the property of being opened or closed
  iii.  to represent its activation state (the door lock is activated or deactivated), and
  iv.  to count the number of unsuccessful attempts at opening the door;
3.  the class has a single constructor, **DoorLock( Combination combination )**, which initializes this instance with a combination. When a door lock is first created, the door lock is closed. Also, when the object is first created, it is activated and the number of failed attempts at opening it should be zero;
4.  implement the instance method **public boolean isOpen()** that returns **true** if this door lock is currently opened and **false** otherwise;
5.  implement the instance method **public boolean isActivated()** that returns **true** if this door lock is currently activated and **false** otherwise;
6.  implement the instance method **public void activate(Combination c)** that sets the instance variable "activated" to true if the parameter c "equals" to the combination of this object;
7.  finally, implement the instance method **public boolean open( Combination combination )** such that
  i.  an attempt is made at opening this door lock only if this door lock is activated
  ii.  if the parameter combination "equals" to the combination of this door lock, set the state of the door to be open, and the number of failed attempts should be reset to zero
  iii.  otherwise, i.e. if the wrong Combination was supplied, the number of failed attempts should be incremented by one,
  iv.  if the number of failed attempts reaches **MAX_NUMBER_OF_ATTEMPTS**, this door lock should be deactivated.

**Hint**: my implementation is approximately 40 lines long, not counting the blank lines.

### SecurityAgent (if there's time)

Implement the class **SecurityAgent** described below.

1.  instance variables. A security agent is responsible for a particular door lock. Declare the necessary instance variables such that a SecurityAgent
  i.  remembers (stores) a Combination and
  ii.  has access to this particular DoorLock, i.e. maintains a reference to a DoorLock object;
2.  implement a constructor with no parameter such that when a new SecurityAgent is created
  i.  it creates a new Combination and stores it,
  ii.  it creates a new DoorLock with this saved Combination. For the sake of simplicity, you may decide to always use the same combination:

```java
Combination secret;
secret = new Combination(1,2,3);
```

if **secret** is the name of the instance variable that is used to remember the Combination. Or, you can let your SecurityAgents use their imagination, so that each SecurityAgent has a new Combination that it only knows.

```java
int first, second, third;

first = (int) (Math.random()*5) + 1;
second = (int) (Math.random()*5) + 1;
third = (int) (Math.random()*5) + 1;

secret = new Combination(first, second, third);
```

Alternative way to generate a random combination:

```java
java.util.Random generator;
generator = new  java.util.Random();

int first, second, third;

first = generator.nextInt(5) + 1;
second = generator.nextInt(5) + 1;
third = generator.nextInt(5) + 1;

secret = new Combination(first, second, third);
```

The valid values are within the interval 1 to 5.

3.  implement the instance method **public DoorLock getDoorLock()** that returns a reference to the saved **DoorLock**;
4.  implement the instance method **public void activateDoorLock()** that simply reactivates the particular DoorLock that this SecurityAgent is responsible for, with the saved secret Combination.

**Hint**: my implementation is approximately 15 lines long, not counting the blank lines.

### Main program

The SecurityAgency class is provided with this laboratory to test the functionality of the three classes described above. I suggest that you only use it when all your classes have been successfully implemented and tested.

The SecurityAgency class consists of a main method that

1.  Takes one command line argument representing the maximum number of attempts allowed to unlock the door.
2.  Creates a SecurityAgent called bob,
3.  it asks bob for an access to the DoorLock that bob is in charge of,
4.  then it applies a "brute force" approach to unlock the door.
5.  After three failures, it has to ask bob to re-activate the lock.
6.  When the lock has been unlocked, it prints the combination of the lock, as well as the number of attempts that were necessary to open the door lock.

Pay attention at providing the required command line argument. Here are examples of successful runs:

```java
> java SecurityAgency 300
Success!
Number of attemtps: 266
The combination is: 3:1:3

> java SecurityAgency 10
Success!
Number of attemtps: 1
The combination is: 4:1:5

> java SecurityAgency 120
Success!
Number of attemtps: 115
The combination is: 2:2:1

> java SecurityAgency 400
Success!
Number of attemtps: 383
The combination is: 2:4:5

> java SecurityAgency 90
Success!
Number of attemtps: 89
The combination is: 3:5:1

> java SecurityAgency 8
Failed!
Reached the maximum number of attempts before finding the combination!
```

**Warning :** if the classes are not properly implemented and if you do not provide the maximum number of attempts as an argument, this program can run forever, if you encounter such a situation use Ctrl-c to kill the process.

**Hint:** build test classes for each of the three classes that you implement.

* SecurityAgency.java

## Resources

* [https://docs.oracle.com/javase/tutorial/getStarted/application/index.html](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html](https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html)
