# Chapter 1: Declarations and Access Control

### Identifiers, Keywords, Source File Rules and Conventions

###### Legal Identifiers
- Must start with a letter, currency character or connecting character. May contain numbers after that.
- Length is not limited.
- Must not be a Java keyword.
- They are case-sensitive.

###### Keywords (50 in total)
- abstract, boolean, break, byte, case, catch, char, class, const, continue, default, do, double, else, extends, final, finally, float, for, goto, if, implements, import, instanceof, int, interface, long, native, new, package, private, protected, public, return, short, static, strictfp, super, switch, synchronized, this, throw, throws, transient, try, void, volatile, while, assert, enum.

###### Source File Declaration Rules
- The number of public classes in a source code file can be either 1 or 0. If 1, its name and the file name must match.
- The package line goes first if it exists, then imports if they exist. Import and package statements affect the entire file.

###### Conventions
- Classes and interfaces: CamelCase.
- Interfaces: should be adjectives: _Runnable_ and _Serializable_.
- Variables and methods: should be CamelCase but with a lowercase first character. 
- Methods: should be verb-noun pairs: _getBalance_.
- Constants: should be uppercase with underscores as separators: _MIN_HEIGHT_.

### javac and java
- Compile: _javac_ [options] [source files]
- Run: _java_ [options] class [args]
- ``` sh
    javac -cp ./:myJar.jar MyClass.java
    java Main arg1
    ```

### The Special main()
- The following are all legal declarations for the "special" _main()_:
    ``` java
        static public void main(String[] args)
        public static void main(String... x)            // varargs
        static public void main(String bang_a_gong[])
- _main()_ can be overloaded.

### Import Statements
- They help you type less:
-   ``` java
        System.out.println(Integer.MAX_VALUE);
        System.out.println(Integer.toHexString(42));
        java.util.ArrayList<String> a = new ArrayList<String>();
    ```
    is the same as
-   ``` java
        import static java.lang.System.out;
        import static java.lang.Integer.*;
        import java.util.ArrayList;
        ...
        out.println(MAX_VALUE);
        out.println(toHexString(42));
        ArrayList<String> a = new ArrayList<String>();
    ```
- _Static import_ is used to import static members of a class:
    ``` java
        double r = Math.cos(Math.PI * theta);
    ```
    is the same as
    ``` java
        import static java.lang.Math.PI;
        ...
        double r = cos(PI * theta);
    ```

### Modifiers

###### Access modifiers for classes and members
- Cannot be applied to local variables, only _final_ can.
- _this._ always refers to the currently executing object.
- Determining access

| Visibility                                     | Public | Protected                | Default | Private |
|------------------------------------------------|--------|--------------------------|---------|---------|
| From the same class                            | Yes    | Yes                      | Yes     | Yes     |
| From any class in the same package             | Yes    | Yes                      | Yes     | No      |
| From a subclass in the same package            | Yes    | Yes                      | Yes     | No      |
| From a subclass outside the same package       | Yes    | Yes, through inheritance | No      | No      |
| From any nonsubclass class outside the package | Yes    | No                       | No      | No      |


###### Nonaccess modifiers (including strictfp, final, and abstract)
- _final_ on a(n)...
    - Class: it can´t be subclassed.
    - Method: it can´t be overridden in a subclass.
    - Variable: must be assigned an explicit value by the time the constuctor finishes, it can't be assigned a new value afterwards.
    - Argument: it can't be modified within the method.
- _abstract_ on a...
    - Class: it can't be instantiated, only extended (subclassed). 
    - Methods: contain no functional code or curly braces, they end in a semicolon: _public abstract void goUpHill()__;_.
- _synchronized_ (only for methods).
- _native_ (only for methods) indicates that a method is implemented in platform-dependent code, often in C.
- _transient_ (only for instance variables) tells the JVM to skip (ignore) this variable when you attempt to serialize the object containing it.
- _volatile_ (only for instance variables) tells the JVM that a thread accessing the variable must always reconcile its own private copy of the variable with the master copy in memory.
- _static_ is used to create variables and methods that will exist independently of any instances created for the class. Can also be applied to nested classes within another class, but not within a method, and to Initialization blocks.

###### Comparison of usable modifiers on variables, methods and classes
- Local Variables can be modified with: _final_.
- Variables (non-local) can be modified with: _public_, _protected_, _private_, _final_, _static_, _transient_ or _volatile_.
- Methods can be modified with: _public_, _protected_, _private_, _final_, _static_, _abstract_, _strictfp_, _synchronized_, or _native_.
- Classes can be modified with: _public_, _protected_, _private_, _final_, _abstract_ or _strictfp_ (can be _static_ in nested classes).

### Interfaces
- Contracts for what a class can do.
- All interface methods are implicitly _public_ and _abstract_. Because they are _abstract_, they cannot be _final_, _strictfp_, or _native_. They can´t be _static_ either.
- All variables defined in an interface are implicitly _public_, _static_, and _final_ (so constants).
- Extend: They can extend one or more other interfaces, but nothing other than an interface.
- Implement: cannot implement another interface or class.
- They must be declared with the keyword _interface_.
- Interface types can be used polymorphically (more on Chapter 2).
- An abstract implementing class does not have to implement the interface methods (but the first concrete subclass must).

### Constructors
- Can't have a return type.
- Must have the same name as the class.
- Can't be _static_ (they are associated with object instantiation), _final_ or _abstract_ (they can't be overridden)

### Range of Numeric Primitives
-  primitive types with their sizes and ranges.

| Type   | Bits | Bytes | Minimum Range | Maximum Range |
|--------|------|-------|---------------|---------------|
| byte   | 8    | 1     | -2 x 10^7     | 2 x 10^7 - 1  |
| short  | 16   | 2     | -2 x 10^15    | 2 x 10^15 - 1 |
| int    | 32   | 4     | -2 x 10^31    | 2 x 10^31 - 1 |
| long   | 64   | 8     | -2 x 10^63    | 2 x 10^63 - 1 |
| float  | 32   | 4     | n/a           | n/a           |
| double | 64   | 8     | n/a           | n/a           |


### Enumerated Types
- ``` java
    enum CoffeeSize { BIG, HUGE, OVERWHELMING };
    ...
    CoffeeSize cs = CoffeeSize.BIG;
    ```
- _enum_ s can be declared as their own separate class or as a class member; however, they must not be declared within a method.
- _enum_ s declared outside a class must NOT be marked _static_, _final_, _abstract_, _protected_, or _private_.
- It is optional to put a semicolon at the end of the enum declaration.
- Every enum has a static method: _values()_.
- If they are declared inside a class, the enclosing name class is required when accessing it.
- Enums are not _String_ s or _int_ s.
- Constant specific class bodies can override enum methods defined in the _enum_.
- ``` java
    enum CoffeeSize {
        BIG(8),
        HUGE(10),
        OVERWHELMING(16) {					// start a code block that defines the "body" for this constant
            public String getLidCode() {	// override the method defined in CoffeeSize
                return "A";
            }
        }; // the semicolon is REQUIRED when more code follows
        CoffeeSize(int ounces) {
            this.ounces=ounces;
        }
        private int ounces;
        public int getOunces() {
            return ounces;
        }
        public String getLidCode() {		// this method is overridden by the OVERWHELMING constant
            return "B";						// the default value we want to return for CoffeeSize constants
        }
    }
    ```