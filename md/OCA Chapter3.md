# Chapter 3: Assignments

### Stack and Heap
- The pieces of a Java program (methods, variables and objects) live in one of two places in memory:
    - The stack: for functions and local variables.
    - The heap: for instance variables and objects.

### Literals
- Integers
    - base 2: They start with _0B_ or _0b_.
        - _0b00011_ represents a 3.
    - base 8: They start with _0_.
        - You can have up to 21 digits in an octal number, not including the leading zero.
        - _010_ represents a 10. 
    - base 10.
    - base 16: They start with _0x_ or _0X_.
        - You can use uppercase or lowercase letters.
    - All four integer literals (binary, octal, decimal, and hexadecimal) are defined as int by default, but they may also be specified as _long_ by placing a suffix of _L_ or _l_ after the number: 
    - Numeric literals (_int_ s, _double_ s and _float_ s) can be writen with underscores inside them, though not at the beggining and not next to the decimal point: _1_000_000_.
- Floating point literals
    - They are _double_ s (64 bits) by default, so if you want to assign a floating-point literal to a variable of type _float_ (32 bits), you must attach the suffix _F_ or _f_ to the number. Possible loss of precision.
    - A _D_ or _d_ suffix makes them _double_ s. It's not necessary, it is allready the default behavior.
    - Numeric literals can´t include commas.
- _Boolean_ literals.
    - _true_ or _false_. They can´t be _0_ or _1_.
- _Character_ literals.
    - Represented by a single character in single quotes.
    - You can also type in the Unicode value of the character, prefixing the value with \u: _'\u004E'_ represents the character _N_.
    - Characters are just 16-bit unsigned integers under the hood.
    ``` java
        char a = 0x892;         // hexadecimal literal
        char b = 982;           // int literal
        char c = (char) 70000;  // the cast is required; 70000 is out of char range.
        char d = (char) -98     // legal
    ```
- String literals
    - Strings are not primitives, but can be represented as literals.
    - The only other nonprimitive type that has a literal representation is an array, which we'll look at later in the chapter.

### Assignment Operators
- Variables are just bit holders, with a designated type.
- For primitives, the bits represent a numeric value. A byte with a value of 6, for example, means that the bit pattern in the variable (the byte holder) is 00000110, representing the 8 bits.
- A reference variable bit holder contains bits representing a way to get to the object. The way in which object references are stored is virtual-machine specific.
- The compiler automatically casts an _int_ if you are assigning it to a smaller container (_byte_, _char_ or _short_) and if it fits. The following lines are identical:
    ``` java
    byte b = 27;
    byte b = (byte) 27;
    ```
-  The result of an expression involving anything int-sized or smaller is always an int, and in those cases you do need to add an explicit cast.
    ``` java
    byte c = (byte) (a + b); // if a and b are also _byte_ s, the cast is necessary.
    ```
- It's legal to declare multiple variables of the same type with a single line by placing a comma between each variable (the order matters):
    ``` java
    int j, k=1, l, m=3;
    ```

### Primitive Casting
- Typically, an implicit cast (one you don´t have to write) happens when you're doing a _widening_ conversion: putting a smaller thing into a bigger container (say, a _byte_ in an _int_).
- Possible loss of precision happens when trying to put a larger thing into a smaller container (say, a _long_ in a _short_): _narrowing_.
- When you cast a floating-point number to an integer type, the value loses all the digits after the decimal.
-  This results in the byte having a value of _-126_.
    ``` java
    long l = 130L;
    byte b = (byte)l;
    ```
-  This will get us a compiler error, it can be fixed with a cast:
    ``` java
    byte a = 128; // byte can only hold up to 127
    ```
-  +=, -=, *=, and /= will all put in an implicit cast. The following 2 are equivalent:
    ``` java
    byte b = 3;
    b += 7;
    ```
    ``` java
    byte b = 3;
    b = (byte) (b + 7);  // Won't compile without the cast, since b + 7 results in an int
    ```
-  You can assign a subclass of the declared type but not a superclass of the declared type.

### Scope
- There are four basic scopes:
    - Static variables: live while a class is loaded in the JVM.
    - Instance variables: live while an instance lives.
    - Local variables: live while their method remains on the stack.
    - Block variables: live while the code block is executing.

### Variable Initialization
- An instance variable is declared within the class but outside any method or constructor, whereas a local variable is declared within a method (or in the argument list of the method).
- Local variables are sometimes called stack, temporary, automatic, or method variables.
- Although you can leave a local variable uninitialized, the compiler complains if you try to use it before initializing it with a value.
    - Array instances
        - An array is an object.
        - if the array is initialized, all array elements are given their default values (the same default values that elements of that type get when they're instance variables).
        - Array elements are always, given default values, regardless of where the array itself is declared or instantiated.
    - Instance Variables
        - Default values for primitive and object types:
        
| Variable Type          | Default Value |
|------------------------|---------------|
| Object reference       | 0             |
| byte, short, int, long | 0             |
| float, double          | 0.0           |
| boolean                | false         |
| char                   | '\u0000'      |
- Local (Stack, Automatic)
    - Primitives
        - Local variables, including primitives always must be initialized before you attempt to use them (though not necessarily on the same line of code).
        - If you initialize within a logically conditional block, the compiler knows that the initialization might not happen and can produce an error.
    - Objects
        - To the compiler, null is a value. Locally declared references can't get away with checking for null before use.
        - local references are not given a default value; in other words, they aren't null.
    - Arrays
        - Must be assigned a value before use. That just means you must declare and construct the array.
        - You do not, however, need to explicitly initialize the elements of an array. They get default values.
- Assigning one reference variiable to another.
    - The assignment copies a bit pattern to another container.
    - Two same bit patterns refer to the same instance.
    - Strings
        - Strings are an exception. They are inmutable. Any time we make any changes at all to a String, the VM will update the reference variable to refer to a different object.
        - When you use a String reference variable to modify a string:
            - A new string is created (or a matching String is found in the String pool), leaving the original String object untouched.
            - The reference used to modify the String (or rather, make a new String by modifying a copy of the original) is then assigned the brand new String object.

### Passing varibles into Methods
- Passing Objects and Primitives
    - When you pass an object variable into a method, you're passing a copy of the object reference, not the actual object itself. But because they refer to the same object, if the called method modifies the object, the caller will see that the object the caller's original variable refers to has also been changed.
    - Passing primitive or reference variables, you are always passing a copy of the bits in the variable.
    - The called method can't change the caller's variable, although for object reference variables, the called method can change the object the variable referred to. For object references, it means the called method can't reassign the caller's original reference variable and make it refer to a different object
or null.
- Shadowing: reusing a variable name that's already been declared somewhere else.

### Garbage Collection
- Overview
    - The exam focuses its garbage collection questions on non-String objects
    - The heap is that part of memory where Java objects live, and it's the one and only part of memory that is in any way involved in the garbage collection process.
    - It is about deleting any objects that are no longer reachable by the Java program running.
    - The GC looks for discarded objects and deletes them from memory so that the cycle of using memory and releasing it can continue.
- When?
    - JVM decides when to run the garbage collector. You can ask it to do so, but there are no guarantees that it will comply.
- How
    - It differs from one Java implementation to another. The Java specification doesn't guarantee any particular implementation.
    - An object is eligible for garbage collection when no live thread can access it.
    - Can a Java application run out of memory? Yes, if you maintain too many live objects the system can run out of memory.
    - Garbage collection cannot ensure that there is enough memory, only that the memory that is available will be managed as efficiently as possible.
- Explicitly make objects eligible for collection
    - Nulling a reference (_reference_ = null)
    - Reassigning a reference variable
        - Also, when a method is invoked, any local variables created exist only for the duration of the method. Once the method has returned, the objects created in the method are eligible for garbage collection.
    - Isolating a reference.
        For exampel: Two instances of a class exist and have a reference to each other. If all other references to these two objects are removed, then even though each object still has a valid reference, there will be no way for any live thread to access either object.
    - The _finalize()_ method
        - Lets you run some code just before your object is deleted by the garbage collector.
        - For any given object, _finalize()_ will be called only once (at most) by the
garbage collector.
        - It can actually result in saving an object from deletion. But if at some point later on this same object becomes eligible for garbage collection again, the GC will remember and it will not run _finalize()_ again.