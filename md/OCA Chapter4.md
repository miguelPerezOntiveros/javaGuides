# Chapter 4: Operators

### Overloaded operators
- The + operator can be used to add two numeric primitives together or to perform a concatenation operation if either operand is a _String_.
- The &, |, and ^ operators can be used bitwise as well as non-short-circuit AND, OR, and XOR.

### Assignment Operators
- When assigning a value to a primitive: check the size; when assigning a value to a reference variable: check the type.
- Compound Assignment Operators (+=, -=, *=, and /= are the most important ones) all put in an implicit cast.
    ``` java
        byte b = 3; b = (byte) (b + 7); // will not compile without the cast.
        ...
        byte b = 3; b += 7; // no cast needed
    ```

### Relational Operators
- There are 6 ( <, <=, >, =>, == and !=)
- The "Equality" Operators
    - _==_ 
        - for primitives: checks equality of the values.
        - for objects: checks reference to the same object.
    - _.equals_
        - for objects: same as _==_, checks references.
        - for strings: overriden to return _true_ if the strings have the same value and is case sensitive.

### The _instanceof_ Comparison
- IS-A test

### Arithmetic Operators
- Use parenthesis to force something to be evaluated first.
- Postfix and prefix increment and decrement operators.
- The _+_ sign acts depending on the expression on its left.

### Conditional Operator
- ``` java
    x = (boolean expression) ? value to assign if true : value to assign if false
    ```

### Short-Circuit Logical Operators
- _&&_ Short.circuit AND: does not evaluate the expression on its right if the expression on its left evaluated to false.
- _||_ Short.circuit OR: does not evaluate the expression on its right if the expression on its left evaluated to true.