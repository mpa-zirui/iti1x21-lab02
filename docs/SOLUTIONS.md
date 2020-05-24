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

### Solutions

```java
21.0
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

### Solutions

```java
   Test.java:5: error: incompatible types: possible lossy conversion from double to int
              int sum = num1 + num2;
                        ^
   1 error
```

Since there will be a loss of information (conversion from **double** to **int**) the compiler does not allow the **implicit** conversion.

Comme il y aurait perte d'information (conversion de **double** à **int**), le compilateur ne permet pas la conversion implicite de données.

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

### Solutions

```java
15
```

Comparez les questions 1.23 et 1.24\. Vous constaterez l'importance d'utiliser les **opérateur de cast** aux bons endroits afin d'obtenir les résultats voulus.

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

### Solutions

```java
16
```

Compare the question 1.23 and 1.24. you will see the importance of using the operator cast at the right place to get the right results.

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

### Solutions

```java
   Test.java:4: error: incompatible types: possible lossy conversion from int to char
              char a = num;
                    ^
   1 error
```

Once again there will be a possible loss of information! The compiler does not allow you to implicitly convert the type **int** to **char**. The opposite conversion (**char** to **int**) could however have been done implicitly

Encore une fois, il y aurait perte d'information! Le compilateur refuse donc de convertir implicitement les données de **int** à **char**. La conversion opposée, soit de **char** à **int**, peut toutefois être effectuée implicitement.

## Question 1.26 :

```java
public class Test {
  public static void main(String[] args) {
    System.out.println( (float)(int)2017.89432 );
  }
}
```

### Solutions

```java
2017.0
```

The operator **cast** (int) is executed first. Then, there is a conversion from this new value of type **int** to a **float**

L'**opérateur de cast** (int) est d'abord exécuté. Ensuite, il y a conversion de cette nouvelle valeur de type **int** en **float**.
