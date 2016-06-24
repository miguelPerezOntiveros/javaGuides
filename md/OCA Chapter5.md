# Chapter 5: Strings, Arrays and ArrayLists
### Contents
* Strings
* Arrays
* ArrayLists
### Strings
###### The _String_ Class
- Once a String object is created, it can never be changed, it is inmutable, but its reference variable is not.
- In Java, each character in a string is a 16-bit Unicode character.
- You can create a new object of class _String_ and assign it to a reference variable in any of the following ways:
    ``` java
        String s = new String();
        s = "abcdef";
    ```
    ``` java
        String s = new String("abcdef");    // creates 2 objects and one reference variable
    ```
    ``` java
        String s = "abcdef";                // creates one String object and one reference variable
    ```
- If we do
    ``` java,
        s = s.concat(" more stuff");
    ```
    the string does not change, the reference variable _s_ was changed so that it would refer to a different string.
- The JVM sets aside a special area of memory called the String constant pool. When the compiler encounters a String literal, it checks the pool. If a match is found, the existing String is used.
- Overriding the _String_ class functionality could cause problems in the pool, so the _String_ class is marked final.
- Important Methods
    - public char charAt(int index) - Returns the character at the specified index.
    - public String concat(String s) - Returns a string with the value of the String passed in to the method appended to the end of the String used to invoke the method.
    - public boolean equalsIgnoreCase(String s) - Determines equality of 2 strings, ignoring case.
    - public int length() - Returns the number of characters in a String.
    - public String replace(char old, char new) - Replaces ocurrences od a character with a new character.
    - public String substring(int begin) - Returns a part of a String.
    - public String toLowerCase() - Returns a string, with uppercase characters converted to lowercase.
    - public String toString() - Returns the value of a String.
    - public String toUpperCase() - Retusn a string, with ñowercase characters converted to uppercase.
    - public String trim() - Removes whitespace from both ends of a String.
###### The _StringBuilder_ Class
- Objects of type StringBuilder can be modified over and over again without leaving behind a great effluence of discarded String objects.
- The _StringBuffer_ class has exactly the same API, except StringBuilder is not thread-safe. StringBuilder will run faster.
- There are 3 ways to create a _StringBuilder_:
    1. new StringBuilder();         // default cap. = 16 chars
    1. new StringBuilder("ab");     // cap. = 16 + arg's length
    1. new StringBuilder(x);        // capacity = x (an integer)
- When _append()_ ing and _insert()_ ing:
    - If an insert() attempts to start at an index after the StringBuilder's current length, an exception will be thrown.
    - If an append() or insert() grows a StringBuilder past its capacity, the capacity is updated automatically.
- Important Methods (of the following, all except _toString()_ modify the valueof the _StringBuilder_ object that invoked the call)
    - public StringBuilder append(String s)
    - public StringBuilder delete(int start, int end)
    - public StringBuilder insert(int offset, String s)
    - public StringBuilder reverse()
    - public String toString()
### Arrays
- Arrays can hold either primitives or object references.
- There is no such thing as a primitive array, but you can make an array of primitives.
- Declaring (Making a reference variable)
    - State the type, and follow that with square brackets to the right or to the left of the identifier. Brackets before the name is recomended.
        ``` java
            int[] key;  // recomended
            int key []; // legal
        ```
    - For multidimensional arrays, which are arrays of arrays:
        ``` java
            String[][][] occupantName;  // recommended
            String[] managerName [];    // legal
        ```
    - It is never legal to include the size of the array in your declaration.
- Constructing (Instantiating, or creating the array object on the heap)
    - Only up until this point, the size of the array is needed to allocate the appropriate space on the heap for the new array object.
    - Use the keyword _new_ followed by the array type, with a bracket specifying how many elements of that type the array will hold.
        ``` java
            int[] testScores;           // Declares
            testScores = new int[4];    // Constructs and assigns
        ```
        which is the same as:
        ``` java
            int[] testScores = new int[4];  // Still no actual threads have been created.
        ```
    - Multidimensional arrays are arrays of arrays. A two-dimensional array of type _int_ is really an object of type _int []_, with each element in that array holding a reference to another _int []_.
    - The following is valid since the JVM needs to know only the size of the object assigned to the variable _myArray_: 
        ``` java
            int[][] myArray = new int[3][];
        ```
- Initializing (populate the array with elements)
    -  An array of objects (as opposed to primitives), doesn't actually hold the objects, but references to objects.
    - The individual elements in the array can be accessed with an index number (based 0).
    - If an array has three elements, trying to access the element [3] will raise an ArrayIndexOutOfBoundsException.
    - The following will cause a runtime exception:
        ``` java
            int[] x = new int[5];
		    x[5] = 3;    // Runtime  exception. There is no element at index 5!
        ```
    - Array objects have a single public variable, _length_, that gives you the number of elements in the array.
- Declaring, Constructing, and Initializing on One Line:
    ``` java
        int[] dots = {6,7,8};
        Dog[] myDogs = {new Dog("Puppy"), new Dog("Clover"), new Dog("Aiko")};
        int[][] scores = {{5,2,4,7}, {9,2}, {3,4}};
    ```
- Anonymous Arrays - _new int[] {4,7,2};_ can be assgined or passed to a function without being assigned to a reference variable.
- Element Asignments
    - Primitives - Can accept any value that can be promoted implicitly to the declared type of the array. An int array can hold any value that can fit into a 32-bit int variable (_byte_, _char_ and _short_).
    - Objects - You can put objects of any subclass of the declared type into the array. Any object that passes the IS-A test for the declared array type can be assigned to an element of that array.
    - One-dimensional Arrays - If you declare an int array, the reference variable you declared can be reassigned to any int array (of any size), but the variable cannot be reassigned to anything that is not an int array (not even a _byte_, _short_, or _char_ array). Arrays that hold object references CAN be assigned to arrays of other objects if they pass the IS-A test.
    - Multidimensional Arrays - When you assign an array to a previously declared array reference, the array you're assigning must be in the same dimension as the reference you're assigning it to.
    ``` java
        int[][]  books = new int[3][];
        int[] numbers = new int[6];
        int aNumber = 7;
        books[0] = aNumber;     // NO, expecting an int array not an int
        books[0] = numbers;     // OK, numbers is an int array
    ```
### ArrayLists
- The Java API provides classes that support common data structures such as _Lists_, _Sets_, _Maps_, and _Queues_. The classes that support these common data structures are a part of what is known as "The Collection API".
- They are easier to use than arrays in scenarios where you need to be able to increase or decrease the number of things in you list, and where the order is important and varies.
- The ArrayList class is in the java.util package.
- When you build an ArrayList you have to declare what kind of objects it can contain. This is a polyphormic declaration. The Syntax inbetween the _<>_ has to do with "generics".
    ``` java
        List<String> c = new ArrayList<String>();
    ```
- ArrayList implements the List interface.
- Like arrays, indexes for ArrayLists are zero-based.
- We don't need to declare how big the ArrayList will be.
- We are able to add a new element to the ArrayList on the fly, and even in the middle of the list.
- An _ArrayList_ maintains its order.
- The _ArrayList_'s _toString()_ method is overriden to show the contents of the ArrayList.
- _ArrayList_ s can have duplicates.
- _ArrayLists_ s hold only object references, not actual objects, and not primitives. In _myArrayList.add(7);_, the int is being autoboxed (converted) to an _Integer_ object and then added.
- Important Methods
    - add(element) - Adds _element_ at the end of the ArrayList.
    - add(index, element) - Adds _element_ at the _index_ position, shifts the remaining elements towards the end.
    - clear() - Removes all elements from the _ArrayList_.
    - boolean contains(element) - Returns whether _element_ is in the _ArrayList_.
    - Object get(index) - Returns the _Object_ located at the _index_ position.
    - int indexOf(object) - Returns the location of the element, or -1 if it was not found.
    - remove(index) - Removes the element at the _index_ position and shifts the remaining elements towards the beggining.
    - remove(Object) - Removes the first occurrence of the Object and shifts later elements toward the beginning.
    - int size() - Returns the number of elements in the ArrayList.
- Encapsulation
    - When encapsulating a mutable object like a StringBuilder, an array, or an ArrayList, if you want to let outside classes have a copy of the object, you must actually copy the object and return a reference variable to the object that is a copy. If you just return a copy of the original object's reference variable, you DO NOT have encapsulation.