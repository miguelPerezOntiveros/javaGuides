# Chapter 6: Flow Control and Exceptions

### Contents
* Decision statements (_if_, _else_ and _switch_)
* Loops (_for_, _do_ and _while_)
* Exceptions

### Decision statements (_if_, _else_ and _switch_)

###### _if_ and _else_
- 1 y 0 are not boolean expressions in Java. 
- _else_ and _if_ can be combined to create _else-if_ constructs.


###### _switch_
- A _switch_'s expression must evaluate to _enum_, _string_ or values that can be implicitly cast to _int_ (not _long_, _float_ or _double_).
- A _switch_ can only check for equality, no other relational operators.
- A _case_ argument larger than 127 will not compile if you switch on a variable smaller than an int.
- 2 _case_ clauses cannot have the same constant in the same _switch_.
- Case constants are evaluated top-down, the first case constant that matches the switch's expression is the execution entry point.
- Execution _fall-through_: When no break is present, code execution continues to the next case.
- The _default_ case will run if non of the cases matched.
- A switch's cases must be compile-time constants or enum values (_final String_ is ok).

### Loops (_for_, _do_ and _while_)

###### _for_ loop
- The basic for loop:
    ```java
    for (/*Initialization*/ ; /*Condition*/ ;  /* Iteration */) { 
        /* Loop body */ 
    }
    ```
- Variables declared inside the _Initialization_ part only exist within the loop.
- You can declare multiple variables in the _Initialization_ part separating them with comas, but they will all be of the same type.
- The _Iteration_ expression runs after the body is executed.
- None of the 3 parts are required. In case of not having any part presen, the _for_ will act like an endless loop.
- If only the _Condition_ expression is provided, the _for_ act like a _while_ loop.
- You can put in virtually any arbitrary code statements that you want to happen with each iteration of the loop as the _Iteration_ expression.

###### Enhanced _for_ loop
- Similar to a _foreach_ in other languages.
    ```java
    for( /*Initialization*/ int n : /*Expression*/ array) { 
        /* Loop body */ 
    }
    ```

###### _while_ loop
- Any variables used in the expression of a while loop must be declared before the expression is evaluated. Example of a _while_ loop:
    ```java
    while ( /*Expression*/ 1 == 1) { 
        /* Loop body */ 
    }
    ```

###### _do_ loop
- The code in a do loop is guaranteed to execute at least once.  Example of a _do_ loop:
    ```java
    do { 
        /* Loop body */ 
    } while( /*Expression*/ 1 == 1);
    ```

###### _break_ and _continue_
- _break_ stops the entire loop.
- _continue_ stops the current iteration.
- Both _break_ and _continue_ can be labeled or unlabeled.
-  A label statement must be placed just before the statement being labeled, and it consists of a valid identifier that ends with a colon (:).
    ```java
    myFooLabel:
        for( ...
    ```
- labeled _break_ and _continue_ are used with nested loops
    ```java
    break myFooLabel;
    ```

### Exceptions
- If there is a return statement in the _try_ block, the _finally_ block executes before it executes.
- If a System.exit() is present, the _finally_ block will not execute. 
- A _try_ needs to have a _finally_, a _catch_, or both.
- Any method that might throw an exception (unless it's a subclass of RuntimeException) must declare the exception.
- If you have multiple _catch_ clauses, the most generic need to be below the most specific.
- Java's "handle or declare": Each method must either handle all checked exceptions by supplying a catch clause or list each unhandled checked exception as a thrown exception.
- A single generic _catch_ can be used to catch multiple subtypes.
- _RuntimeException_ are the only unchecked exceptions and it and it's decendants don´t need to be handled or declared. 
- You can create your own exceptions, for example extending from _Exception_.
- You sholdn´t handle an _error_, because you can rarely recover from one.
- _Error_ and _Exception_ are inmediate children of _Throwable_, who is an inmediate child of _Object_.
- An overriding method cannot throw checked exceptions that are broader than those thrown by the overridden method (Apart from _RuntimeException_). 

###### Common Exceptions
- 10 exceptions and errors to cover OCA Objective 8.5.

| Exception                                  | Description                                                                                                                           | Typically Thrown |
|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|------------------|
| ArrayIndexOutOfBoundsException,(Chapter 5) | Thrown when attempting to access an array with an invalid index value (either negative or beyond the length of the array).            | By the JVM       |
| ClassCastException,(Chapter 2)             | Thrown when attempting to cast a reference variable to a type that fails the IS-A test.                                               | By the JVM       |
| IllegalArgumentException                   | Thrown when a method receives an argument formatted differently than the method expects.                                              | Programmatically |
| IllegalStateException                      | Thrown when the state of the environment doesn't match the operation being attempted—for example, using a scanner that's been closed. | Programmatically |
| NullPointerException,(Chapter 3)           | Thrown when attempting to invoke a method on, or access a property from, a reference variable whose current value is null.            | By the JVM       |
| NumberFormatException,(this chapter)       | Thrown when a method that converts a String to a number receives a String that it cannot convert.                                     | Programmatically |
| AssertionError                             | Thrown when an assert statement's boolean test returns false.                                                                         | Programmatically |
| ExceptionInInitializerError,(Chapter 2)    | Thrown when attempting to initialize a static variable or an initialization block.                                                    | By the JVM       |
| StackOverflowError,(this chapter)          | Typically thrown when a method recurses too deeply. (Each invocation is added to the stack.)                                          | By the JVM       |
| NoClassDefFoundError                       | Thrown when the JVM can't find a class it needs, because of a command- line error, a classpath issue, or a missing .class file.       | By the JVM       |