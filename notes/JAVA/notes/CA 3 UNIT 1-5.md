Okay, Scholar! Let's buckle down and cram this Java knowledge. We'll approach this systematically, unit by unit, focusing on understanding the concepts and illustrating them with clear, concise examples. Think of this as your condensed, high-yield study guide.

---

## Unit I: Foundations of Java

This unit lays the groundwork. Get these fundamentals right, and everything else builds upon them.

### 1. Introduction to Java

*   **History & Features:**
    *   **History:** Originated at Sun Microsystems (now Oracle) in the early 90s (Project Green, James Gosling). Initially for consumer electronics, pivoted to the web.
    *   **Key Features:**
        *   **Platform Independent (WORA):** Write Once, Run Anywhere. Java code compiles to bytecode (`.class` files), which runs on any machine with a Java Virtual Machine (JVM).
        *   **Object-Oriented:** Organizes code around objects (data and methods). Promotes modularity, reusability (more in Unit II/III).
        *   **Simple:** Relatively easier to learn compared to C++ (e.g., no explicit pointers, automatic memory management).
        *   **Robust:** Strong memory management, exception handling (Unit IV), type checking prevent many common errors.
        *   **Secure:** Security features built into the language and JVM (e.g., Security Manager, bytecode verification).
        *   **Multithreaded:** Built-in support for concurrent execution of tasks.
        *   **High Performance:** Just-In-Time (JIT) compilers in JVMs convert bytecode to native machine code for speed.

*   **Java Program Structure:**
    *   A typical Java program consists of one or more classes.
    *   Execution starts from the `main` method.

    ```java
    // This is a single-line comment
    /*
     * This is a
     * multi-line comment.
     */

    package com.example.study; // Optional: Organizes classes into namespaces

    import java.util.Scanner; // Optional: Imports classes from other packages

    public class HelloWorld { // Class declaration (must match file name: HelloWorld.java)

        // The main method: entry point of the program
        public static void main(String[] args) {
            // Code inside the main method executes first
            System.out.println("Hello, Java Scholar!"); // Prints output to the console

            // Example using an imported class
            Scanner input = new Scanner(System.in);
            System.out.print("Enter your name: ");
            String name = input.nextLine();
            System.out.println("Welcome, " + name + "!");
            input.close(); // Good practice to close resources
        }
    } // End of class HelloWorld
    ```

*   **Writing Simple Java Class and `main()` Method:**
    *   `public class ClassName { ... }`: Defines a class accessible from anywhere. The file name *must* be `ClassName.java`.
    *   `public static void main(String[] args)`: The special method where execution begins.
        *   `public`: Accessible from anywhere (needed by the JVM to start).
        *   `static`: Belongs to the class itself, not an object instance. The JVM calls it without creating an object.
        *   `void`: Doesn't return any value.
        *   `main`: The specific name the JVM looks for.
        *   `String[] args`: An array of Strings to receive command-line arguments.

*   **Command-Line Arguments:**
    *   Values passed to the program when it's run from the terminal/command prompt.
    *   They are stored in the `args` array within the `main` method.

    ```java
    // File: ShowArgs.java
    public class ShowArgs {
        public static void main(String[] args) {
            System.out.println("Number of arguments: " + args.length);
            if (args.length > 0) {
                System.out.println("Arguments received:");
                for (int i = 0; i < args.length; i++) {
                    System.out.println("Arg " + i + ": " + args[i]);
                }
            } else {
                System.out.println("No arguments provided.");
            }
        }
    }
    ```
    *   **Compilation & Running:**
        1.  `javac ShowArgs.java` (Compiles to `ShowArgs.class`)
        2.  `java ShowArgs arg1 "second arg" 123` (Runs the program, passing arguments)
    *   **Output:**
        ```
        Number of arguments: 3
        Arguments received:
        Arg 0: arg1
        Arg 1: second arg
        Arg 2: 123
        ```

*   **Understanding JDK, JRE, and JVM:**
    *   **JVM (Java Virtual Machine):**
        *   The *engine* that runs Java bytecode (`.class` files).
        *   Abstract machine, platform-dependent (different JVMs for Windows, Linux, Mac).
        *   Provides memory management (garbage collection), security, etc.
        *   *Analogy:* The specific interpreter/player needed to understand and execute the compiled Java instructions.
    *   **JRE (Java Runtime Environment):**
        *   Contains the JVM + Java Class Libraries (core APIs like `java.lang`, `java.util`, etc.).
        *   Everything needed to *run* compiled Java applications.
        *   *Analogy:* The JVM plus the standard library of tools/parts the program might need while running. You need this to *use* Java software.
    *   **JDK (Java Development Kit):**
        *   Contains the JRE + Development Tools (compiler `javac`, debugger `jdb`, documentation generator `javadoc`, etc.).
        *   Everything needed to *develop* (write, compile, debug) Java applications.
        *   *Analogy:* The JRE plus the workshop tools (compiler, etc.) needed to *create* Java software.
    *   **Relationship:** JDK contains JRE, which contains JVM. (JDK > JRE > JVM)

### 2. Data In the Cart

*   **Primitive Data Types:** Fundamental building blocks for data. Stored directly in memory.
    *   **Integer Types:**
        *   `byte`: 8 bits, -128 to 127 (Default: 0)
        *   `short`: 16 bits, -32,768 to 32,767 (Default: 0)
        *   `int`: 32 bits, approx -2.1 billion to 2.1 billion (Default: 0) - *Most common integer type.*
        *   `long`: 64 bits, very large range (suffix `L` or `l` needed for literals). (Default: 0L)
    *   **Floating-Point Types:** For numbers with decimal points.
        *   `float`: 32 bits, single-precision (suffix `F` or `f` needed for literals). (Default: 0.0f)
        *   `double`: 64 bits, double-precision (Default: 0.0d or 0.0) - *More precise, generally preferred.*
    *   **Character Type:**
        *   `char`: 16 bits, Unicode character (single quotes `' '` for literals). (Default: `\u0000`)
    *   **Boolean Type:**
        *   `boolean`: Represents `true` or `false` (size is JVM-dependent, logically 1 bit). (Default: `false`)

    ```java
    public class PrimitivesDemo {
        public static void main(String[] args) {
            byte age = 30;
            short year = 2024;
            int population = 1_000_000; // Underscores allowed for readability
            long nationalDebt = 30_000_000_000_000L; // Note the 'L'

            float price = 19.99f; // Note the 'f'
            double pi = 3.1415926535;

            char grade = 'A';
            char newline = '\n'; // Special character literal

            boolean isJavaFun = true;

            System.out.println("Age: " + age);
            System.out.println("PI: " + pi);
            System.out.println("Grade: " + grade);
            System.out.println("Is Java Fun? " + isJavaFun);
        }
    }
    ```

*   **Type Conversion (Casting):**
    *   **Implicit Conversion (Widening):** Automatic conversion from a smaller type to a larger type (no data loss).
        *   `byte -> short -> int -> long -> float -> double`
        *   `char -> int`
    *   **Explicit Conversion (Narrowing / Casting):** Manual conversion from a larger type to a smaller type. Requires `(targetType)` syntax. *Potential data loss!*

    ```java
    public class TypeConversion {
        public static void main(String[] args) {
            // Implicit (Widening)
            int myInt = 100;
            long myLong = myInt; // int to long (OK)
            double myDouble = myLong; // long to double (OK)
            // float myFloat = myDouble; // Error! Cannot implicitly narrow double to float

            System.out.println("Implicit: myInt=" + myInt + ", myLong=" + myLong + ", myDouble=" + myDouble);

            // Explicit (Narrowing / Casting)
            double pi = 3.14159;
            int approxPi = (int) pi; // double to int (fractional part lost)

            long bigNum = 1_000_000_000_000L;
            int smallerNum = (int) bigNum; // long to int (potential overflow/data corruption!)

            byte b = (byte) 300; // int literal 300 is too large for byte, wraps around

            System.out.println("Explicit: pi=" + pi + ", approxPi=" + approxPi);
            System.out.println("Explicit: bigNum=" + bigNum + ", smallerNum=" + smallerNum); // Value might be unexpected
            System.out.println("Explicit: byte b from 300 = " + b); // Value will be 44 (300 % 256)
        }
    }
    ```

*   **Keywords:** Reserved words with special meaning in Java. Cannot be used as identifiers (variable names, class names, etc.). Examples: `public`, `class`, `static`, `void`, `int`, `if`, `else`, `for`, `while`, `new`, `this`, `super`, `return`, `true`, `false`, `null`, etc. (Around 50 keywords).

*   **Identifiers:** Names given to classes, methods, variables, etc.
    *   **Rules:**
        *   Must start with a letter, underscore (`_`), or dollar sign (`$`).
        *   Subsequent characters can be letters, digits, `_`, or `$`.
        *   Cannot be a Java keyword.
        *   Case-sensitive (`myVar` is different from `myvar`).
    *   **Conventions (Best Practices):**
        *   `ClassName`: UpperCamelCase.
        *   `variableName`, `methodName`: lowerCamelCase.
        *   `CONSTANT_NAME`: ALL_CAPS_WITH_UNDERSCORES (for `static final` variables).
        *   Package names: `lowercase.with.dots`.

    ```java
    // Good Identifiers
    int studentCount;
    String firstName;
    class MyDataProcessor {}
    final double PI = 3.14159;

    // Bad Identifiers (will cause compile errors)
    // int 1stPlace; // Cannot start with a digit
    // String first-name; // Hyphen not allowed
    // double static; // 'static' is a keyword
    ```

*   **Variables:** Named memory locations that hold data. Must be declared with a type before use.
    *   **Declaration:** `type variableName;` (e.g., `int score;`)
    *   **Initialization:** Assigning an initial value. `variableName = value;` (e.g., `score = 100;`)
    *   **Declaration + Initialization:** `type variableName = value;` (e.g., `int score = 100;`)

*   **Access Modifiers:** Control the visibility/accessibility of classes, methods, and variables.
    *   `public`: Accessible from any other class.
    *   `private`: Accessible only within the declaring class. (Encapsulation)
    *   `protected`: Accessible within the declaring class, its package, and its subclasses (even if in different packages).
    *   `default` (no keyword): Accessible only within the same package. (Package-private)
    *   *(More detail in OOP/Inheritance units)*

*   **`static` Keyword:**
    *   Indicates that a member (variable or method) belongs to the *class itself*, rather than to any specific *object (instance)* of the class.
    *   **Static Variables (Class Variables):** Shared among all instances of the class. Only one copy exists.
    *   **Static Methods:** Can be called directly on the class name (`ClassName.staticMethod()`) without creating an object. Cannot directly access instance variables or instance methods (as there's no specific object associated with the call). Can access other static members. `main` is always static.

    ```java
    public class Counter {
        static int staticCount = 0; // Class variable - shared by all Counter objects
        int instanceCount = 0;     // Instance variable - each object gets its own copy

        public Counter() {
            staticCount++;
            instanceCount++;
        }

        public static void printStaticCount() {
            System.out.println("Static Count: " + staticCount);
            // System.out.println(instanceCount); // Error! Cannot access instance variable from static context
        }

        public void printInstanceCount() {
            System.out.println("Instance Count for this object: " + instanceCount);
            System.out.println("Static Count (accessible from instance method): " + staticCount);
        }

        public static void main(String[] args) {
            Counter.printStaticCount(); // Call static method on class

            Counter c1 = new Counter();
            Counter c2 = new Counter();
            Counter c3 = new Counter();

            System.out.println("--- After creating 3 objects ---");
            Counter.printStaticCount(); // Static count is now 3

            c1.printInstanceCount(); // Instance count is 1 for c1
            c2.printInstanceCount(); // Instance count is 1 for c2
            c3.printInstanceCount(); // Instance count is 1 for c3
        }
    }
    ```

*   **Wrapper Classes:**
    *   Provide object representations for primitive data types. Found in `java.lang` package.
    *   Needed when you need to treat primitives as objects (e.g., in Collections like `ArrayList<Integer>`).
    *   Provide utility methods (e.g., `Integer.parseInt()`, `Double.toString()`).
    *   **Primitives & Wrappers:**
        *   `byte` -> `Byte`
        *   `short` -> `Short`
        *   `int` -> `Integer`
        *   `long` -> `Long`
        *   `float` -> `Float`
        *   `double` -> `Double`
        *   `char` -> `Character`
        *   `boolean` -> `Boolean`
    *   **Autoboxing:** Automatic conversion from primitive to wrapper object (e.g., `Integer i = 100;`).
    *   **Unboxing:** Automatic conversion from wrapper object to primitive (e.g., `int j = i;`).

    ```java
    import java.util.ArrayList;
    import java.util.List;

    public class WrapperDemo {
        public static void main(String[] args) {
            // Autoboxing
            Integer iObject = 100; // int 100 is autoboxed to Integer object
            Double dObject = 3.14; // double 3.14 is autoboxed to Double object
            List<Integer> numbers = new ArrayList<>();
            numbers.add(1); // Autoboxing: int 1 -> Integer object
            numbers.add(2); // Autoboxing: int 2 -> Integer object

            // Unboxing
            int iPrimitive = iObject; // Integer object unboxed to int primitive
            double dPrimitive = dObject; // Double object unboxed to double primitive
            int firstNum = numbers.get(0); // Unboxing: Integer object -> int primitive

            System.out.println("iPrimitive: " + iPrimitive);
            System.out.println("dPrimitive: " + dPrimitive);
            System.out.println("First number in list: " + firstNum);

            // Utility methods
            String numStr = "12345";
            int parsedInt = Integer.parseInt(numStr);
            System.out.println("Parsed Integer: " + parsedInt);

            String doubleStr = Double.toString(dPrimitive);
            System.out.println("Double as String: " + doubleStr);

            System.out.println("Max Integer value: " + Integer.MAX_VALUE);
            System.out.println("Is 'A' a digit? " + Character.isDigit('A')); // false
            System.out.println("Is '7' a digit? " + Character.isDigit('7')); // true
        }
    }
    ```

### 3. Operators

Symbols that perform operations on operands (variables or values).

*   **Arithmetic Operators:** `+` (addition), `-` (subtraction), `*` (multiplication), `/` (division), `%` (modulo/remainder).
    *   Integer division `/` truncates decimals (e.g., `5 / 2` is `2`).
    *   Use `double` or `float` for floating-point division (e.g., `5.0 / 2.0` is `2.5`).
    *   `%` gives the remainder (e.g., `5 % 2` is `1`).

*   **Relational Operators:** Compare two values, result is `boolean` (`true` or `false`).
    *   `==` (equal to)
    *   `!=` (not equal to)
    *   `>` (greater than)
    *   `<` (less than)
    *   `>=` (greater than or equal to)
    *   `<=` (less than or equal to)

*   **Logical Operators:** Combine boolean expressions.
    *   `&&` (Logical AND): `true` if *both* operands are `true`. (Short-circuiting: if left is `false`, right is not evaluated).
    *   `||` (Logical OR): `true` if *at least one* operand is `true`. (Short-circuiting: if left is `true`, right is not evaluated).
    *   `!` (Logical NOT): Inverts boolean value (`!true` is `false`, `!false` is `true`).

*   **Bitwise Operators:** Operate on the individual bits of integer types (`byte`, `short`, `int`, `long`).
    *   `&` (Bitwise AND): Sets bit to 1 if *both* corresponding bits are 1.
    *   `|` (Bitwise OR): Sets bit to 1 if *at least one* corresponding bit is 1.
    *   `^` (Bitwise XOR): Sets bit to 1 if corresponding bits are *different*.
    *   `~` (Bitwise Complement): Flips all bits (0s become 1s, 1s become 0s). Unary operator.
    *   `<<` (Left Shift): Shifts bits left, fills with 0s on the right (`x << n` is like `x * 2^n`).
    *   `>>` (Signed Right Shift): Shifts bits right, fills with the sign bit (leftmost bit) on the left. Preserves sign (`x >> n` is like `x / 2^n`).
    *   `>>>` (Unsigned Right Shift): Shifts bits right, fills with 0s on the left. Treats number as unsigned.

    ```java
    // Example: Bitwise AND
    // 5 = 0101
    // 3 = 0011
    // --------
    // 1 = 0001 (5 & 3)
    int resultAnd = 5 & 3; // resultAnd will be 1
    ```

*   **Assignment Operators:** Assign values to variables.
    *   `=` (Simple Assignment): Assigns right-hand value to left-hand variable.
    *   Compound Assignment: Combine arithmetic/bitwise op with assignment.
        *   `+=`, `-=`, `*=`, `/=`, `%=`
        *   `&=`, `|=`, `^=`
        *   `<<=`, `>>=`, `>>>=`
        *   Example: `x += 5;` is shorthand for `x = x + 5;`

*   **Unary Operators:** Operate on a single operand.
    *   `+` (Unary Plus): Indicates positive value (often implicit).
    *   `-` (Unary Minus): Negates a value.
    *   `++` (Increment): Increases value by 1.
        *   *Prefix* `++x`: Increments `x` *before* its value is used in the expression.
        *   *Postfix* `x++`: Uses the *current* value of `x` in the expression, then increments `x`.
    *   `--` (Decrement): Decreases value by 1 (Prefix `--x`, Postfix `x--`).
    *   `!` (Logical NOT - already mentioned).
    *   `~` (Bitwise Complement - already mentioned).

    ```java
    int a = 5;
    int b = ++a; // a becomes 6, b becomes 6 (prefix)
    int c = 5;
    int d = c++; // d becomes 5, c becomes 6 (postfix)
    ```

*   **Ternary Operator:** `condition ? value_if_true : value_if_false`
    *   A shorthand for a simple `if-else` statement that produces a value.

    ```java
    int score = 75;
    String result = (score >= 60) ? "Pass" : "Fail"; // result will be "Pass"
    System.out.println(result);
    ```

*   **Operator Precedence:** The order in which operators are evaluated in an expression.
    *   Highest: Postfix (`x++`, `x--`), Unary (`++x`, `--x`, `+`, `-`, `!`, `~`)
    *   Multiplicative (`*`, `/`, `%`)
    *   Additive (`+`, `-`)
    *   Shift (`<<`, `>>`, `>>>`)
    *   Relational (`<`, `>`, `<=`, `>=`, `instanceof`)
    *   Equality (`==`, `!=`)
    *   Bitwise AND (`&`)
    *   Bitwise XOR (`^`)
    *   Bitwise OR (`|`)
    *   Logical AND (`&&`)
    *   Logical OR (`||`)
    *   Ternary (`? :`)
    *   Lowest: Assignment (`=`, `+=`, `-=`, etc.)
    *   **Rule of Thumb:** Use parentheses `()` to explicitly control the order of evaluation and improve readability, even if you know the precedence.

    ```java
    int x = 5 + 3 * 2; // Multiplication has higher precedence: 5 + 6 = 11
    int y = (5 + 3) * 2; // Parentheses evaluated first: 8 * 2 = 16
    boolean check = x > 10 && y < 20; // Relational > Logical AND. (11 > 10) && (16 < 20) -> true && true -> true
    ```

### 4. Conditional Statements

Control the flow of execution based on conditions.

*   **`if` / `else if` / `else` Construct:**
    *   Executes blocks of code based on boolean conditions.
    *   `if`: Executes if the condition is `true`.
    *   `else if`: Checked only if the preceding `if` (or `else if`) was `false`. Executes if its condition is `true`. Can have multiple `else if` blocks.
    *   `else`: Executes if *all* preceding `if` and `else if` conditions were `false`. Optional.

    ```java
    int score = 85;
    char grade;

    if (score >= 90) {
        grade = 'A';
    } else if (score >= 80) { // score is < 90 here
        grade = 'B';
    } else if (score >= 70) { // score is < 80 here
        grade = 'C';
    } else if (score >= 60) { // score is < 70 here
        grade = 'D';
    } else { // score is < 60 here
        grade = 'F';
    }
    System.out.println("Grade: " + grade); // Output: Grade: B
    ```

*   **`switch-case` Statement:**
    *   Evaluates an expression and executes code blocks matching specific `case` values.
    *   Often more readable than long `if-else if` chains for specific value checks.
    *   Works with: `byte`, `short`, `char`, `int`, `String` (since Java 7), `Enum` types.
    *   `case value:`: Label for a specific value.
    *   `break;`: Exits the `switch` statement. **Crucial!** Without `break`, execution "falls through" to the next `case`.
    *   `default:`: Optional block that executes if no `case` matches.

    ```java
    int dayOfWeek = 3; // 1=Sun, 2=Mon, ..., 7=Sat
    String dayName;

    switch (dayOfWeek) {
        case 1:
            dayName = "Sunday";
            break; // Exit switch
        case 2:
            dayName = "Monday";
            break;
        case 3:
            dayName = "Tuesday";
            break; // <--- Execution stops here for dayOfWeek = 3
        case 4:
            dayName = "Wednesday";
            break;
        case 5:
            dayName = "Thursday";
            break;
        case 6:
            dayName = "Friday";
            break;
        case 7:
            dayName = "Saturday";
            break;
        default:
            dayName = "Invalid day";
            break; // Good practice to include break in default too
    }
    System.out.println("Day: " + dayName); // Output: Day: Tuesday

    // Example with fall-through (less common, use carefully)
    char grade = 'B';
    System.out.print("Your grade " + grade + " means: ");
    switch (grade) {
        case 'A':
            System.out.print("Excellent! ");
            // No break - fall through
        case 'B':
            System.out.print("Good job! ");
            // No break - fall through
        case 'C':
            System.out.print("Passed. ");
            break; // Stop here for A, B, C
        case 'D':
            System.out.print("Barely passed. ");
            break;
        default: // Handles 'F' or invalid grades
            System.out.print("Failed. ");
    }
    System.out.println(); // Output for grade 'B': Your grade B means: Good job! Passed.
    ```

---

Okay, take a breath. That's Unit I. Solidify these concepts – data types, operators, control flow – they are the absolute bedrock. Next up: Loops, Arrays, and the start of OOP! Let me know when you're ready for Unit II.


---
---
Alright, Scholar! Let's intensify the cramming for Unit II. We'll dissect loops, arrays, enums, basic OOP, and the crucial String class, packing in more examples and highlighting common mistakes and edge cases.

---

## Unit II: Control Flow, Data Structures, and OOP Basics

This unit builds directly on Unit I, introducing more complex control structures and the fundamental concepts of Object-Oriented Programming.

### 1. Loops

Loops allow executing a block of code repeatedly.

*   **`for` loop:** Best when the number of iterations is known beforehand.
    *   **Syntax:** `for (initialization; condition; update) { // code block }`
    *   **Execution Flow:**
        1.  `initialization` runs once at the beginning.
        2.  `condition` is checked. If `true`, the code block runs. If `false`, the loop terminates.
        3.  `update` runs after the code block.
        4.  Go back to step 2.

    ```java
    public class ForLoopDemo {
        public static void main(String[] args) {
            System.out.println("Counting up:");
            for (int i = 0; i < 5; i++) { // i goes from 0 to 4
                System.out.println("i = " + i);
            }

            System.out.println("\nCounting down:");
            for (int j = 10; j >= 0; j -= 2) { // j goes 10, 8, 6, 4, 2, 0
                System.out.println("j = " + j);
            }

            // Loop with multiple variables (less common but possible)
            System.out.println("\nMultiple vars:");
            for (int x = 0, y = 5; x <= 5; x++, y--) {
                 System.out.println("x=" + x + ", y=" + y);
            }
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Off-by-One Errors:** Using `<` vs. `<=` incorrectly, or starting/ending at the wrong index. If you need to iterate 5 times, `i < 5` (0, 1, 2, 3, 4) is common, but `i <= 4` also works. Be careful!
        *   **Infinite Loop:** If the `condition` never becomes `false` (e.g., `for(int k=0; k >= 0; k++)` if `k` never wraps around, or forgetting the `update` statement like `for(int k=0; k < 5; ) { System.out.println(k); }`).
        *   **Scope:** The loop control variable (`i`, `j`, `x`, `y` above) exists *only* within the `for` loop's scope (including its header and body). You cannot access `i` after the first loop finishes.

*   **`while` loop:** Best when the number of iterations is unknown, depends on a condition that changes *inside* the loop.
    *   **Syntax:** `while (condition) { // code block }`
    *   **Execution Flow:**
        1.  `condition` is checked. If `true`, the code block runs. If `false`, the loop terminates.
        2.  Go back to step 1.
        *   *Crucial:* The condition must eventually become false, usually due to changes within the loop body.

    ```java
    import java.util.Scanner;

    public class WhileLoopDemo {
        public static void main(String[] args) {
            int count = 0;
            System.out.println("While loop (count < 5):");
            while (count < 5) {
                System.out.println("Count is: " + count);
                count++; // MUST update the variable used in the condition
            }
            System.out.println("Loop finished. Final count: " + count);

            // Example: Reading input until a specific value is entered
            Scanner scanner = new Scanner(System.in);
            String input = "";
            while (!input.equalsIgnoreCase("quit")) { // Loop until user types "quit"
                System.out.print("Enter command (or 'quit' to exit): ");
                input = scanner.nextLine();
                System.out.println("You entered: " + input);
            }
            System.out.println("Exiting program.");
            scanner.close();
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Infinite Loop:** The most common `while` loop error. Happens if the condition *always* evaluates to `true` because the variable(s) controlling it are never updated correctly inside the loop. (e.g., forgetting `count++` in the first example).
        *   **Condition Never Met:** If the condition is `false` initially, the loop body *never* executes.

*   **`do-while` loop:** Similar to `while`, but the condition is checked *after* the loop body executes. Guarantees the body runs at least once.
    *   **Syntax:** `do { // code block } while (condition);` (Note the semicolon at the end!)
    *   **Execution Flow:**
        1.  The code block runs.
        2.  `condition` is checked. If `true`, go back to step 1. If `false`, the loop terminates.

    ```java
    import java.util.Scanner;

    public class DoWhileDemo {
        public static void main(String[] args) {
            int counter = 10; // Start with a value that makes the condition initially false

            System.out.println("Do-While loop (counter < 5):");
            do {
                System.out.println("Counter is: " + counter); // This WILL print once
                counter++;
            } while (counter < 5); // Condition (11 < 5) is false, loop terminates
            System.out.println("Loop finished. Final counter: " + counter);

            // Example: Menu that repeats until user chooses to exit
            Scanner scanner = new Scanner(System.in);
            int choice;
            do {
                System.out.println("\n--- MENU ---");
                System.out.println("1. Option A");
                System.out.println("2. Option B");
                System.out.println("0. Exit");
                System.out.print("Enter your choice: ");
                choice = scanner.nextInt(); // Potential InputMismatchException if user enters non-integer

                switch (choice) {
                    case 1: System.out.println("Executing Option A..."); break;
                    case 2: System.out.println("Executing Option B..."); break;
                    case 0: System.out.println("Exiting..."); break;
                    default: System.out.println("Invalid choice. Try again.");
                }
            } while (choice != 0); // Repeat as long as choice is not 0
            scanner.close();
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Unintended First Execution:** Since the body runs before the first check, make sure this initial execution is always desired or harmless, even if the condition might be false from the start.
        *   **Infinite Loop:** Same risk as `while` if the condition never becomes false.
        *   **Missing Semicolon:** Forgetting the `;` after `while(condition)` is a syntax error.

*   **`for-each` loop (Enhanced `for` loop):** Provides a simpler way to iterate over elements of an array or a collection.
    *   **Syntax:** `for (Type element : arrayOrCollection) { // code block using element }`
    *   Reads as: "For each `element` of type `Type` in `arrayOrCollection`..."

    ```java
    import java.util.ArrayList;
    import java.util.List;

    public class ForEachDemo {
        public static void main(String[] args) {
            // Iterating over an array
            String[] names = {"Alice", "Bob", "Charlie", "David"};
            System.out.println("Names in array:");
            for (String name : names) {
                System.out.println("- " + name.toUpperCase());
            }

            // Iterating over a Collection (ArrayList)
            List<Integer> numbers = new ArrayList<>();
            numbers.add(10);
            numbers.add(20);
            numbers.add(30);
            System.out.println("\nNumbers in list:");
            int sum = 0;
            for (int number : numbers) {
                System.out.println("Processing: " + number);
                sum += number;
            }
            System.out.println("Sum: " + sum);
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Read-Only Access:** The loop variable (`name`, `number` above) is a *copy* of the element (for primitives) or a copy of the *reference* (for objects). Modifying the loop variable inside the loop does *not* change the original array/collection element itself (unless the variable is an object reference and you modify the object's *state* via its methods).
        *   **No Index Access:** You don't get the index (0, 1, 2...) directly like in a standard `for` loop. If you need the index, use a traditional `for` loop.
        *   **Cannot Modify Collection Structure:** You generally cannot add or remove elements from a collection *while* iterating over it using a `for-each` loop. Doing so often results in a `ConcurrentModificationException`. Use an `Iterator` explicitly if you need to remove elements during iteration.

        ```java
        // Example of ConcurrentModificationException (PITFALL!)
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");

        try {
            for (String fruit : fruits) {
                if (fruit.equals("Banana")) {
                    // fruits.remove(fruit); // THIS WILL LIKELY THROW ConcurrentModificationException
                    System.out.println("Found Banana, but cannot remove it safely here.");
                }
            }
        } catch (java.util.ConcurrentModificationException e) {
            System.err.println("Error: Cannot modify list while iterating with for-each: " + e);
        }
        ```

### 2. Arrays and Enums

*   **Arrays:** Fixed-size, ordered collections of elements of the *same* data type.
    *   **Declaration:** `dataType[] arrayName;` or `dataType arrayName[];` (first is preferred)
    *   **Initialization:**
        *   `arrayName = new dataType[size];` (Creates array with default values: 0 for numbers, `false` for boolean, `null` for objects)
        *   `dataType[] arrayName = {value1, value2, ...};` (Declaration and initialization with values)
        *   `dataType[] arrayName = new dataType[]{value1, value2, ...};` (Anonymous array initialization)
    *   **Access:** `arrayName[index]` (Indices are 0-based: 0 to `length - 1`)
    *   **Length:** `arrayName.length` (Provides the number of elements the array can hold)

    ```java
    public class ArrayDemo {
        public static void main(String[] args) {
            // Declaration and Initialization
            int[] scores = new int[5]; // Array of 5 ints, initialized to 0
            String[] names = {"Alice", "Bob", "Charlie"}; // Size 3, initialized with values
            double[] values; // Declaration only
            values = new double[]{1.1, 2.2, 3.3, 4.4}; // Initialization later

            // Accessing elements
            scores[0] = 95;
            scores[1] = 88;
            // scores[5] = 100; // PITFALL: ArrayIndexOutOfBoundsException (valid indices are 0-4)

            System.out.println("First score: " + scores[0]);
            System.out.println("Second name: " + names[1]);
            System.out.println("Length of scores array: " + scores.length); // Output: 5
            System.out.println("Length of names array: " + names.length);   // Output: 3

            // Iterating using standard for loop (useful for index)
            System.out.println("\nScores (standard for):");
            for (int i = 0; i < scores.length; i++) {
                System.out.println("Index " + i + ": " + scores[i]);
            }

            // Iterating using for-each loop
            System.out.println("\nNames (for-each):");
            for (String name : names) {
                System.out.println("- " + name);
            }

            // Default values
            boolean[] flags = new boolean[3]; // Initialized to {false, false, false}
            String[] texts = new String[2];   // Initialized to {null, null}
            System.out.println("\nDefault boolean: " + flags[0]);
            System.out.println("Default String: " + texts[0]);

            // Trying to access element of null array (PITFALL!)
            int[] nullArray = null;
            try {
                 System.out.println(nullArray.length); // Throws NullPointerException
            } catch (NullPointerException e) {
                 System.err.println("\nError: Cannot access length of a null array: " + e);
            }
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **`ArrayIndexOutOfBoundsException`:** Accessing an index less than 0 or greater than or equal to `array.length`. This is extremely common. Always check bounds, especially in loops (`i < length`, not `i <= length`).
        *   **`NullPointerException`:** Declaring an array variable (`int[] data;`) but not initializing it (`data = new int[10];`) before trying to access its elements or length (`data[0]` or `data.length`). The variable holds `null`.
        *   **Fixed Size:** Once created, an array's size cannot be changed. If you need a dynamic size, use `ArrayList` (from `java.util`).
        *   **Comparing Arrays:** Using `array1 == array2` checks if they are the *same object* in memory, not if they have the same *contents*. To compare contents, use `java.util.Arrays.equals(array1, array2)`.

        ```java
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        int[] arr3 = arr1;

        System.out.println(arr1 == arr2); // false (different objects)
        System.out.println(arr1 == arr3); // true (same object)
        System.out.println(java.util.Arrays.equals(arr1, arr2)); // true (contents are equal)
        ```

*   **Multi-dimensional Arrays:** Arrays of arrays.
    *   **Declaration:** `dataType[][] arrayName;`
    *   **Initialization:**
        *   `arrayName = new dataType[rows][columns];` (Rectangular array)
        *   `dataType[][] arrayName = {{r1c1, r1c2}, {r2c1, r2c2}, ...};`
        *   Can be "jagged" (rows have different lengths): `arrayName = new dataType[rows][]; arrayName[0] = new dataType[3]; arrayName[1] = new dataType[5];`

    ```java
    public class MultiDimArrayDemo {
        public static void main(String[] args) {
            // Rectangular array (3 rows, 4 columns)
            int[][] matrix = new int[3][4];
            matrix[0][0] = 1;
            matrix[1][2] = 5;
            // matrix[3][0] = 9; // PITFALL: ArrayIndexOutOfBoundsException (rows are 0-2)
            // matrix[0][4] = 7; // PITFALL: ArrayIndexOutOfBoundsException (cols are 0-3)

            System.out.println("Matrix element [1][2]: " + matrix[1][2]); // Output: 5
            System.out.println("Number of rows: " + matrix.length);       // Output: 3
            System.out.println("Number of columns in row 0: " + matrix[0].length); // Output: 4

            // Initializing with values
            String[][] users = {
                {"ID1", "Alice", "Admin"},
                {"ID2", "Bob", "User"},
                {"ID3", "Charlie", "User"}
            };

            System.out.println("\nUser Data:");
            for (int row = 0; row < users.length; row++) {
                for (int col = 0; col < users[row].length; col++) { // Use users[row].length for columns
                    System.out.print(users[row][col] + "\t");
                }
                System.out.println();
            }

            // Jagged array
            System.out.println("\nJagged Array:");
            int[][] jagged = new int[3][];
            jagged[0] = new int[]{1, 2};       // Row 0 has 2 columns
            jagged[1] = new int[]{3, 4, 5, 6}; // Row 1 has 4 columns
            jagged[2] = new int[]{7};          // Row 2 has 1 column

            for (int row = 0; row < jagged.length; row++) {
                System.out.print("Row " + row + ": ");
                if (jagged[row] != null) { // PITFALL: Check if inner array is initialized!
                    for (int col = 0; col < jagged[row].length; col++) {
                        System.out.print(jagged[row][col] + " ");
                    }
                } else {
                    System.out.print(" (not initialized)");
                }
                System.out.println();
            }
             // Accessing uninitialized inner array (PITFALL!)
            int[][] badJagged = new int[2][];
            try {
                 System.out.println(badJagged[0].length); // Throws NullPointerException because badJagged[0] is null
            } catch(NullPointerException e) {
                 System.err.println("\nError: Inner array not initialized: " + e);
            }
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Index Out of Bounds:** Errors can occur on either dimension (`matrix[row][col]`).
        *   **`NullPointerException` with Jagged Arrays:** If you declare `int[][] jagged = new int[3][];` but don't initialize a specific row (e.g., `jagged[1] = new int[4];`), then accessing `jagged[1][0]` or `jagged[1].length` will cause a `NullPointerException`. Always initialize inner arrays before use.
        *   **Confusion in Iteration:** Remember `array.length` gives the number of rows, and `array[row].length` gives the number of columns *for that specific row*.

*   **`varargs` (Variable Arguments):** Allows a method to accept zero or more arguments of a specified type.
    *   Treated as an array inside the method.
    *   Must be the *last* parameter in the method signature.
    *   **Syntax:** `returnType methodName(Type... variableName)`

    ```java
    public class VarargsDemo {

        // Method accepting variable number of integers
        public static int sum(int... numbers) { // 'numbers' is treated as int[] inside
            System.out.println("Number of arguments received: " + numbers.length);
            int total = 0;
            if (numbers.length == 0) {
                System.out.println("Warning: No numbers provided to sum.");
                // return 0; // Or throw exception, depending on requirements
            }
            for (int number : numbers) {
                total += number;
            }
            return total;
        }

        // Can have other parameters before varargs
        public static void printMessages(String prefix, String... messages) {
             System.out.print(prefix + ": ");
             if (messages.length == 0) {
                 System.out.println(" (No messages)");
                 return;
             }
             for(int i=0; i < messages.length; i++) {
                 System.out.print(messages[i] + (i < messages.length - 1 ? ", " : ""));
             }
             System.out.println();
        }

        // PITFALL: Cannot have multiple varargs or varargs before other params
        // public static void wrongMethod(String... s, int... i) {} // ERROR
        // public static void wrongMethod2(int... i, String s) {} // ERROR

        public static void main(String[] args) {
            System.out.println("Sum(1, 2): " + sum(1, 2));             // 2 arguments
            System.out.println("Sum(5, 10, 15, 20): " + sum(5, 10, 15, 20)); // 4 arguments
            System.out.println("Sum(): " + sum());                   // 0 arguments
            System.out.println("Sum(10): " + sum(10));                 // 1 argument

            // Can also pass an existing array
            int[] data = {100, 200, 300};
            System.out.println("Sum(data array): " + sum(data));

            printMessages("Log", "Started", "Processing", "Finished");
            printMessages("Error"); // Varargs part is empty
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Ambiguity:** If method overloading involves varargs, it can sometimes be ambiguous which method to call. The compiler prefers exact matches or widening conversions over varargs if possible.
        *   **Null Array vs. Empty Varargs:** Calling `sum()` passes an empty array (`numbers.length == 0`). Calling `sum(null)` passes `null` for the array reference, which would cause a `NullPointerException` inside the loop if not checked. Be mindful of how `null` is handled.

*   **Enumerations (`enum`):** A special data type that defines a set of named constants. Type-safe and more readable than using `static final int` constants.
    *   **Syntax:** `enum EnumName { CONSTANT1, CONSTANT2, ... }`
    *   Can have constructors, methods, and variables (more advanced).

    ```java
    // Define an enum for days of the week
    enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    }

    // Define an enum with associated values (more advanced)
    enum Status {
        PENDING("P"), PROCESSING("IP"), COMPLETED("C"), FAILED("F"); // Constants

        private final String shortCode; // Variable associated with each constant

        // Constructor (implicitly private)
        Status(String code) {
            this.shortCode = code;
        }

        // Method to get the associated value
        public String getShortCode() {
            return shortCode;
        }
    }

    public class EnumDemo {
        public static void main(String[] args) {
            // Using the Day enum
            Day today = Day.WEDNESDAY;
            System.out.println("Today is: " + today); // Prints the name: WEDNESDAY

            // Enums can be used in switch statements
            switch (today) {
                case MONDAY:
                case TUESDAY:
                case WEDNESDAY:
                case THURSDAY:
                case FRIDAY:
                    System.out.println("It's a weekday.");
                    break;
                case SATURDAY:
                case SUNDAY:
                    System.out.println("It's the weekend!");
                    break;
                // No default needed if all enum constants are covered (compiler might warn if not)
            }

            // Comparing enum constants
            Day tomorrow = Day.THURSDAY;
            System.out.println("Is today == Day.WEDNESDAY? " + (today == Day.WEDNESDAY)); // true (Use == for enums)
            System.out.println("Is today == tomorrow? " + (today == tomorrow));       // false
            // System.out.println(today == Status.PENDING); // PITFALL: Compile error - incompatible types

            // Iterating over enum constants
            System.out.println("\nAll days:");
            for (Day d : Day.values()) { // .values() returns an array of all constants
                System.out.println("- " + d + " (ordinal: " + d.ordinal() + ")"); // ordinal() gives 0-based position
            }

            // Getting an enum constant from a String
            try {
                Day parsedDay = Day.valueOf("FRIDAY"); // Case-sensitive
                System.out.println("\nParsed day: " + parsedDay);
            } catch (IllegalArgumentException e) {
                 System.err.println("\nError: Invalid day name provided to valueOf(): " + e);
            }
            // Day badParse = Day.valueOf("friday"); // PITFALL: Throws IllegalArgumentException

            // Using the Status enum with values
            Status currentStatus = Status.PROCESSING;
            System.out.println("\nCurrent Status: " + currentStatus); // PROCESSING
            System.out.println("Short Code: " + currentStatus.getShortCode()); // IP
            System.out.println("Status Name: " + currentStatus.name()); // PROCESSING (same as toString())
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Comparing with Strings:** Don't compare enum constants directly with strings using `==` or `.equals()`. Compare enum variables with enum constants (`today == Day.WEDNESDAY`) or use `today.name().equals("WEDNESDAY")` if you must compare with a string representation.
        *   **`valueOf()` Case Sensitivity:** `Enum.valueOf("CONSTANT_NAME")` is case-sensitive and throws `IllegalArgumentException` if the string doesn't exactly match a constant name.
        *   **`NullPointerException`:** An enum variable can be `null`. Trying to call methods like `.ordinal()`, `.name()`, or use it in a `switch` statement will cause a `NullPointerException` if it's `null`.

### 3. OOP Concepts (Basics)

Organizing code around "objects" which have state (data/variables) and behavior (methods).

*   **Class:** A blueprint or template for creating objects. Defines the properties (instance variables) and actions (methods) that objects of that type will have.
*   **Object:** An instance of a class. Created using the `new` keyword. Each object has its own copy of instance variables (state).

    ```java
    // Blueprint for a Dog
    class Dog {
        // Instance variables (state) - each Dog object gets its own copy
        String name;
        String breed;
        int age;
        boolean isSleeping = false; // Default state

        // Method (behavior) - defines what a Dog can do
        void bark() {
            if (isSleeping) {
                System.out.println(name + " murmurs in its sleep...");
            } else {
                System.out.println(name + " says: Woof! Woof!");
            }
        }

        void sleep() {
            isSleeping = true;
            System.out.println(name + " is now sleeping.");
        }

        void wakeUp() {
            isSleeping = false;
            System.out.println(name + " woke up!");
        }

        void displayInfo() {
             System.out.println("Dog Info - Name: " + name + ", Breed: " + breed + ", Age: " + age + ", Sleeping: " + isSleeping);
        }
    } // End of Dog class

    public class OopBasicsDemo {
        public static void main(String[] args) {
            // Create Dog objects (instances) using the 'new' keyword
            Dog dog1 = new Dog(); // Creates a Dog object in memory
            Dog dog2 = new Dog();

            // Access and modify instance variables using the dot (.) operator
            dog1.name = "Buddy";
            dog1.breed = "Golden Retriever";
            dog1.age = 3;

            dog2.name = "Lucy";
            dog2.breed = "Poodle";
            dog2.age = 5;
            dog2.sleep(); // Change Lucy's state

            // Call methods on the objects
            System.out.println("Dog 1 actions:");
            dog1.displayInfo();
            dog1.bark();
            dog1.sleep();
            dog1.bark(); // Barking while sleeping

            System.out.println("\nDog 2 actions:");
            dog2.displayInfo();
            dog2.bark();
            dog2.wakeUp();
            dog2.bark();

            // PITFALL: NullPointerException if object reference is null
            Dog dog3 = null; // dog3 doesn't refer to any object yet
            try {
                dog3.name = "Rex"; // Throws NullPointerException
                dog3.bark();       // Throws NullPointerException
            } catch (NullPointerException e) {
                System.err.println("\nError: Cannot access members of a null object reference: " + e);
            }

             // PITFALL: Forgetting 'new'
             // Dog dog4; // Declared but not initialized (holds null)
             // dog4.name = "Spot"; // Would cause NullPointerException
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **`NullPointerException`:** The most frequent OOP error. Occurs when you try to access a member (variable or method) using an object reference variable that currently holds `null` (doesn't point to an actual object). Always ensure objects are created (`new`) before use, or check for `null`.
        *   **Forgetting `new`:** Just declaring `Dog myDog;` doesn't create an object, it only creates a variable that *can* hold a reference to a Dog object. You must use `myDog = new Dog();` to instantiate it.

*   **Constructors:** Special methods used to initialize objects when they are created (`new`).
    *   Have the same name as the class.
    *   Have no return type (not even `void`).
    *   Called automatically when `new` is used.
    *   **Default Constructor:** If you don't define *any* constructor, Java provides a default, no-argument constructor that does nothing (and initializes instance variables to their default values: 0, false, null). If you *do* define any constructor, the default one is *not* provided automatically.
    *   **Parameterized Constructor:** Accepts arguments to initialize instance variables with specific values during creation.

    ```java
    class Car {
        String make;
        String model;
        int year;
        boolean engineOn;

        // 1. Default-like Constructor (explicitly defined)
        // If we defined ONLY the parameterized one below, this one wouldn't exist implicitly.
        public Car() {
            System.out.println("Car object created using no-arg constructor.");
            // Instance variables get default values (null, null, 0, false)
            // We could add default initializations here if needed:
            // this.make = "Unknown";
        }

        // 2. Parameterized Constructor
        public Car(String carMake, String carModel, int carYear) {
            System.out.println("Car object created using parameterized constructor.");
            make = carMake;   // Assign parameter value to instance variable
            model = carModel;
            year = carYear;
            engineOn = false; // Explicitly set initial state
        }

        void startEngine() {
            if (!engineOn) {
                engineOn = true;
                System.out.println(year + " " + make + " " + model + " engine started.");
            } else {
                System.out.println("Engine is already running.");
            }
        }

        void displayInfo() {
            System.out.println("Car: " + year + " " + make + " " + model + " (Engine On: " + engineOn + ")");
        }
    }

    public class ConstructorDemo {
        public static void main(String[] args) {
            // Using the no-arg constructor
            Car car1 = new Car();
            car1.make = "Toyota"; // Need to set fields manually
            car1.model = "Camry";
            car1.year = 2021;
            car1.displayInfo();

            // Using the parameterized constructor
            Car car2 = new Car("Honda", "Civic", 2022);
            car2.displayInfo();
            car2.startEngine();

            // Car car3 = new Car("Ford", "Mustang"); // PITFALL: Compile Error!
            // No constructor matches these arguments (String, String).
            // We only defined Car() and Car(String, String, int).
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Losing Default Constructor:** If you define *any* constructor (e.g., a parameterized one), Java *stops* providing the automatic no-arg default constructor. If you still need a no-arg constructor, you must define it explicitly.
        *   **Incorrect Argument Matching:** When calling `new`, the arguments must match the parameter types and order of one of the available constructors.

*   **Methods:** Define the behavior of objects. Can access and modify the object's instance variables.
    *   **Syntax:** `accessModifier returnType methodName(parameterList) { // method body }`
    *   `returnType`: The data type of the value the method returns (or `void` if it returns nothing).
    *   `parameterList`: Input values the method accepts (optional).

*   **Overloading (Methods and Constructors):** Defining multiple methods or constructors in the same class with the *same name* but *different parameter lists* (different number, type, or order of parameters). Allows providing different ways to perform an action or create an object.
    *   The return type alone is *not* sufficient to overload a method.

    ```java
    class Calculator {
        // Overloaded add methods
        int add(int a, int b) {
            System.out.println("Adding two ints");
            return a + b;
        }

        double add(double a, double b) {
            System.out.println("Adding two doubles");
            return a + b;
        }

        int add(int a, int b, int c) {
            System.out.println("Adding three ints");
            return a + b + c;
        }

        // String add(int a, int b) { // PITFALL: Compile Error! Cannot overload based only on return type.
        //     return "Sum: " + (a+b);
        // }

        // Overloaded constructors (already seen in Car example)
    }

    public class OverloadingDemo {
        public static void main(String[] args) {
            Calculator calc = new Calculator();

            System.out.println("Result 1: " + calc.add(5, 10));       // Calls add(int, int)
            System.out.println("Result 2: " + calc.add(3.5, 2.1));    // Calls add(double, double)
            System.out.println("Result 3: " + calc.add(1, 2, 3));     // Calls add(int, int, int)

            // Implicit conversion works too
            System.out.println("Result 4: " + calc.add(5, 10.5)); // Calls add(double, double) - int 5 is promoted to double 5.0
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Return Type Only:** Trying to overload by changing only the return type is a compile error. The parameter list *must* differ.
        *   **Ambiguous Calls:** If a call could match multiple overloaded methods equally well (e.g., through type promotion), the compiler might issue an error. `calc.add(5, 5)` clearly matches `add(int, int)`. `calc.add(5.0f, 5.0f)` would match `add(double, double)` because float can be widened to double.

*   **`this` Keyword:** A reference variable that refers to the *current object* (the object whose method or constructor is being called).
    *   **Uses:**
        1.  **Disambiguate Instance Variables:** When a parameter or local variable has the same name as an instance variable (shadowing), use `this.instanceVariable` to refer to the instance variable.
        2.  **Call Another Constructor:** From within a constructor, `this(...)` can be used to call another overloaded constructor *in the same class*. If used, it *must* be the very first statement in the constructor.

    ```java
    class Rectangle {
        private int width; // Instance variable
        private int height; // Instance variable

        // Constructor using 'this' to disambiguate
        public Rectangle(int width, int height) { // Parameters shadow instance variables
            System.out.println("Rectangle(int, int) called.");
            this.width = width;   // this.width refers to instance var, width refers to parameter
            this.height = height; // this.height refers to instance var, height refers to parameter
        }

        // Overloaded constructor calling another constructor using 'this()'
        public Rectangle(int side) {
            // Calls the Rectangle(int, int) constructor
            this(side, side); // MUST be the first statement
            System.out.println("Rectangle(int) called (creates a square).");
            // Cannot add code before this(...) call
        }

        // Default constructor calling the square constructor
        public Rectangle() {
            this(1); // Calls Rectangle(int) constructor with side = 1
            System.out.println("Rectangle() no-arg called (creates 1x1 square).");
        }

        public int getArea() {
            // 'this' is implicit here: return this.width * this.height;
            return width * height;
        }

        public void setWidth(int width) { // Parameter shadows instance variable
            if (width > 0) {
                this.width = width; // Use 'this' to assign to instance variable
            } else {
                System.err.println("Width must be positive.");
            }
        }

         // Method returning the current object instance
         public Rectangle grow(int amount) {
             this.width += amount;
             this.height += amount;
             return this; // Return the modified current object
         }
    }

    public class ThisKeywordDemo {
        public static void main(String[] args) {
            Rectangle r1 = new Rectangle(10, 5); // Calls Rectangle(int, int)
            System.out.println("R1 Area: " + r1.getArea());

            Rectangle r2 = new Rectangle(7); // Calls Rectangle(int), which calls Rectangle(int, int)
            System.out.println("R2 Area: " + r2.getArea());

            Rectangle r3 = new Rectangle(); // Calls Rectangle(), which calls Rectangle(int), which calls Rectangle(int, int)
            System.out.println("R3 Area: " + r3.getArea());

            // PITFALL: Forgetting 'this' when names collide
            // If setWidth was: void setWidth(int width) { width = width; }
            // This would just assign the parameter 'width' to itself, having no effect
            // on the instance variable 'this.width'.
            r1.setWidth(12);
            System.out.println("R1 Area after setWidth: " + r1.getArea());

            // Chaining method calls using 'return this'
            r1.grow(2).grow(3); // Grows by 2, then grows by 3
            System.out.println("R1 Area after growing: " + r1.getArea());
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Shadowing without `this`:** If a parameter or local variable has the same name as an instance variable, using the name directly refers to the parameter/local variable. Forgetting `this.` when you intend to access the instance variable is a common logic error (the instance variable won't be updated).
        *   **`this()` Call Position:** Calling another constructor using `this(...)` *must* be the absolute first statement in the calling constructor. Putting any code before it is a compile error.
        *   **Recursive Constructor Calls:** Avoid creating loops where constructor A calls constructor B using `this()`, and constructor B calls constructor A using `this()`. This leads to a compile error (recursive constructor invocation).

*   **Initializer Blocks:** Blocks of code within a class, outside any method or constructor. Used for initialization logic.
    *   **Instance Initializer Block:** Runs *every time* an object of the class is created. Executes *after* superclass constructor calls and *before* the class's own constructor body.
    *   **Static Initializer Block:** Marked with `static`. Runs *only once*, when the class is first loaded into the JVM (before any objects are created or static members are accessed). Used for initializing static variables.

    ```java
    public class InitializerBlocksDemo {

        // Instance variable
        private String message;
        private static int staticCounter;
        private int instanceId;
        private static final java.util.List<String> VALID_CODES; // Static final variable

        // Static Initializer Block
        static {
            System.out.println("Static Initializer Block: Runs ONCE when class is loaded.");
            staticCounter = 0;
            VALID_CODES = new java.util.ArrayList<>();
            VALID_CODES.add("A1");
            VALID_CODES.add("B2");
            // Cannot access instance variables like 'message' or 'instanceId' here (no object exists yet)
            // System.out.println(message); // Compile Error!
            System.out.println("Static counter initialized. Valid codes loaded.");
        }

        // Instance Initializer Block 1
        {
            System.out.println("Instance Initializer Block 1: Runs for EVERY object creation.");
            this.message = "Default Message";
            this.instanceId = ++staticCounter; // Access static variable
            System.out.println("Instance ID assigned: " + this.instanceId);
        }

        // Constructor 1
        public InitializerBlocksDemo() {
            System.out.println("Constructor (no-arg): Runs AFTER instance initializers.");
            // message is already "Default Message" from the initializer block
            System.out.println("Message in no-arg constructor: " + this.message);
        }

        // Constructor 2
        public InitializerBlocksDemo(String msg) {
            // Instance initializers have already run here! message is "Default Message"
            System.out.println("Constructor (String): Runs AFTER instance initializers.");
            this.message = msg; // Overwrite the value set by the initializer
            System.out.println("Message set by String constructor: " + this.message);
        }

        // Instance Initializer Block 2 (Order matters among instance initializers)
        {
             System.out.println("Instance Initializer Block 2: Runs AFTER Block 1, before constructor.");
        }

        public void display() {
            System.out.println("Displaying - ID: " + instanceId + ", Message: " + message);
        }

        public static void main(String[] args) {
            System.out.println("--- Main method started ---");
            System.out.println("Creating obj1:");
            InitializerBlocksDemo obj1 = new InitializerBlocksDemo(); // Static block runs (if not already), then instance blocks, then constructor

            System.out.println("\nCreating obj2:");
            InitializerBlocksDemo obj2 = new InitializerBlocksDemo("Custom Message"); // Instance blocks run again, then constructor

            System.out.println("\nDisplaying objects:");
            obj1.display();
            obj2.display();

            System.out.println("\nAccessing static member:");
            System.out.println("Final Static Counter: " + InitializerBlocksDemo.staticCounter); // Access static member
            System.out.println("Valid Codes: " + InitializerBlocksDemo.VALID_CODES);
        }
    }
    /* Expected Output Order:
        Static Initializer Block: Runs ONCE when class is loaded.
        Static counter initialized. Valid codes loaded.
        --- Main method started ---
        Creating obj1:
        Instance Initializer Block 1: Runs for EVERY object creation.
        Instance ID assigned: 1
        Instance Initializer Block 2: Runs AFTER Block 1, before constructor.
        Constructor (no-arg): Runs AFTER instance initializers.
        Message in no-arg constructor: Default Message

        Creating obj2:
        Instance Initializer Block 1: Runs for EVERY object creation.
        Instance ID assigned: 2
        Instance Initializer Block 2: Runs AFTER Block 1, before constructor.
        Constructor (String): Runs AFTER instance initializers.
        Message set by String constructor: Custom Message

        Displaying objects:
        Displaying - ID: 1, Message: Default Message
        Displaying - ID: 2, Message: Custom Message

        Accessing static member:
        Final Static Counter: 2
        Valid Codes: [A1, B2]
    */
    ```
    *   **Potential Pitfalls:**
        *   **Order of Execution:** Understanding the exact order is crucial:
            1.  Static initializers (once, when class loads).
            2.  Superclass constructor.
            3.  Instance initializers (in order of appearance).
            4.  Constructor body.
        *   **Static Context:** Static initializers cannot access instance members (non-static variables/methods) directly, as no object exists yet. They can only access static members.
        *   **Exceptions:** If an exception occurs in a static initializer, it becomes an `ExceptionInInitializerError`, which can prevent the class from being used at all. Instance initializers can also throw exceptions, which propagate to the constructor call.
        *   **Over-Reliance:** While useful for complex static setup or shared instance logic, overuse can make code harder to follow than putting logic directly in constructors or helper methods.

### 4. String Class (`java.lang.String`)

Represents sequences of characters. One of the most commonly used classes in Java.

*   **Immutability:** String objects are *immutable*. Once created, their character sequence cannot be changed. Any method that appears to modify a String (like `toUpperCase()`, `replace()`, `substring()`) actually creates and returns a *new* String object with the modified content, leaving the original unchanged.

*   **Constructors & Literals:**
    *   **String Literal:** `String s1 = "Hello";` (Most common way. Java often pools these literals for efficiency).
    *   `new String("Hello");`: Explicitly creates a *new* String object in memory, even if "Hello" already exists in the pool.
    *   `new String(char[] array);`
    *   `new String(byte[] bytes);`

*   **Key Methods:**
    *   `int length()`: Returns the number of characters.
    *   `char charAt(int index)`: Returns the character at the specified index (0-based).
    *   `String substring(int beginIndex)`: Returns a new string from `beginIndex` to the end.
    *   `String substring(int beginIndex, int endIndex)`: Returns a new string from `beginIndex` up to (but *not including*) `endIndex`.
    *   `boolean equals(Object anotherObject)`: Compares the *content* of the strings for equality. **Use this for comparing string values!**
    *   `boolean equalsIgnoreCase(String anotherString)`: Compares content, ignoring case differences.
    *   `int indexOf(String str)` / `int indexOf(char ch)`: Returns the index of the first occurrence of the substring/char, or -1 if not found. Overloaded versions take a starting index.
    *   `int lastIndexOf(String str)` / `int lastIndexOf(char ch)`: Returns the index of the last occurrence.
    *   `boolean startsWith(String prefix)` / `boolean endsWith(String suffix)`: Checks if the string begins/ends with the given sequence.
    *   `String replace(char oldChar, char newChar)` / `String replace(CharSequence target, CharSequence replacement)`: Returns a *new* string with replacements made.
    *   `String toLowerCase()` / `String toUpperCase()`: Returns a *new* string in the specified case.
    *   `String trim()`: Returns a *new* string with leading and trailing whitespace removed.
    *   `String[] split(String regex)`: Splits the string around matches of the given regular expression, returning an array of strings.
    *   `static String valueOf(...)`: Converts various types (primitives, objects) to their string representation.
    *   `static String format(String format, Object... args)`: Creates a formatted string (similar to C's `printf`).

    ```java
    public class StringDemo {
        public static void main(String[] args) {
            String s1 = "Hello"; // Literal - likely pooled
            String s2 = "Hello"; // Literal - likely refers to the SAME pooled object as s1
            String s3 = new String("Hello"); // Explicitly creates a NEW object
            String s4 = "World";
            String s5 = "   Lots of Space   ";
            String s6 = "Java is fun, Java is powerful";
            String s7 = null; // Null reference

            // --- Comparisons (PITFALL ALERT!) ---
            System.out.println("s1 == s2: " + (s1 == s2)); // true (likely same object due to pooling)
            System.out.println("s1 == s3: " + (s1 == s3)); // false (s3 is a distinct object)
            System.out.println("s1.equals(s2): " + s1.equals(s2)); // true (content is the same)
            System.out.println("s1.equals(s3): " + s1.equals(s3)); // true (content is the same) - USE .equals()!

            String sUpper = "HELLO";
            System.out.println("s1.equals(sUpper): " + s1.equals(sUpper)); // false (case-sensitive)
            System.out.println("s1.equalsIgnoreCase(sUpper): " + s1.equalsIgnoreCase(sUpper)); // true

            // --- Basic Methods ---
            System.out.println("Length of s1: " + s1.length()); // 5
            System.out.println("Char at index 1 in s1: " + s1.charAt(1)); // 'e'
            // System.out.println(s1.charAt(5)); // PITFALL: StringIndexOutOfBoundsException (indices 0-4)

            // --- Substrings (New Strings Created) ---
            String sub1 = s1.substring(2); // "llo" (from index 2 to end)
            String sub2 = s1.substring(1, 4); // "ell" (from index 1 up to, not including, 4)
            System.out.println("Substring(2): " + sub1);
            System.out.println("Substring(1, 4): " + sub2);
            System.out.println("Original s1 is unchanged: " + s1); // Still "Hello"

            // --- Searching ---
            System.out.println("Index of 'l' in s1: " + s1.indexOf('l')); // 2 (first occurrence)
            System.out.println("Index of 'l' starting from 3: " + s1.indexOf('l', 3)); // 3
            System.out.println("Index of 'Java' in s6: " + s6.indexOf("Java")); // 0
            System.out.println("Last index of 'Java' in s6: " + s6.lastIndexOf("Java")); // 14
            System.out.println("Index of 'z' in s1: " + s1.indexOf('z')); // -1 (not found)

            // --- Modification (Creates New Strings) ---
            String s1Upper = s1.toUpperCase(); // Creates "HELLO"
            String s5Trimmed = s5.trim(); // Creates "Lots of Space"
            String s6Replaced = s6.replace("Java", "Python"); // Creates "Python is fun, Python is powerful"
            System.out.println("s1 to upper: " + s1Upper);
            System.out.println("s5 trimmed: '" + s5Trimmed + "'");
            System.out.println("s6 replaced: " + s6Replaced);
            System.out.println("Original s6 is unchanged: " + s6); // Still "Java is fun, Java is powerful"

            // --- Splitting ---
            String data = "one,two,three,four";
            String[] parts = data.split(","); // Split by comma
            System.out.println("Split data:");
            for (String part : parts) {
                System.out.println("- " + part);
            }

            // --- Null Handling (PITFALL!) ---
            try {
                System.out.println(s7.length()); // Throws NullPointerException
            } catch (NullPointerException e) {
                System.err.println("Error: Cannot call methods on a null String: " + e);
            }
            // Safer check:
            if (s7 != null && s7.equals("something")) {
                 System.out.println("This won't run.");
            } else {
                 System.out.println("s7 is null or not 'something'.");
            }
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **`==` vs. `.equals()`:** Using `==` compares object references, not content. It might sometimes work for pooled literals, but it's unreliable for comparing string values. **Always use `.equals()` (or `equalsIgnoreCase()`) to compare string content.** This is a very common beginner mistake.
        *   **Immutability Misunderstanding:** Forgetting that methods like `replace`, `substring`, `trim`, `toUpperCase` do *not* change the original string. You must assign the result to a variable (often the same variable) if you want to use the modified version: `myString = myString.trim();`.
        *   **`NullPointerException`:** Calling any method (like `.length()`, `.equals()`, `.substring()`) on a String variable that holds `null` will throw a `NullPointerException`. Always check for `null` before calling methods if a string variable might be null.
        *   **`StringIndexOutOfBoundsException`:** Accessing `charAt()` or `substring()` with an index that is negative or greater than or equal to the string's length.
        *   **Performance with Concatenation in Loops:** Repeatedly concatenating strings inside a loop using `+` (e.g., `result = result + nextPart;`) is inefficient because it creates many intermediate String objects. Use `StringBuilder` for this.

*   **`StringBuilder` Class (`java.lang.StringBuilder`):**
    *   Provides a *mutable* sequence of characters.
    *   Use when you need to perform many modifications (appends, inserts, deletes) to a string of characters efficiently.
    *   Not thread-safe (faster than `StringBuffer`). If thread safety is needed, use `StringBuffer` (which has similar methods but is synchronized).
    *   **Key Methods:**
        *   `append(...)`: Adds content to the end (overloaded for various types). Returns `this` for chaining.
        *   `insert(int offset, ...)`: Inserts content at the specified position. Returns `this`.
        *   `delete(int start, int end)`: Removes characters from `start` to `end-1`. Returns `this`.
        *   `deleteCharAt(int index)`: Removes character at `index`. Returns `this`.
        *   `replace(int start, int end, String str)`: Replaces characters with the given string. Returns `this`.
        *   `reverse()`: Reverses the sequence. Returns `this`.
        *   `int length()`: Current length.
        *   `int capacity()`: Current allocated capacity (can grow automatically).
        *   `String toString()`: Converts the `StringBuilder`'s content back to an immutable `String` object.

    ```java
    public class StringBuilderDemo {
        public static void main(String[] args) {
            // Inefficient String concatenation in a loop (AVOID THIS)
            String resultBad = "";
            String[] items = {"A", "B", "C", "D", "E"};
            long startBad = System.nanoTime();
            for (String item : items) {
                resultBad += item; // Creates new String object in each iteration
            }
            long endBad = System.nanoTime();
            System.out.println("Bad concatenation result: " + resultBad);
            System.out.println("Time taken (bad): " + (endBad - startBad) + " ns");


            // Efficient way using StringBuilder
            StringBuilder sb = new StringBuilder(); // Start with default capacity
            // StringBuilder sb = new StringBuilder(100); // Or specify initial capacity
            long startGood = System.nanoTime();
            for (String item : items) {
                sb.append(item); // Modifies the internal buffer - much faster
            }
            String resultGood = sb.toString(); // Convert to String only once at the end
            long endGood = System.nanoTime();
            System.out.println("Good concatenation result: " + resultGood);
            System.out.println("Time taken (good): " + (endGood - startGood) + " ns"); // Usually much smaller


            // Other StringBuilder operations (chaining)
            StringBuilder message = new StringBuilder("Hello");
            message.append(" ").append("World") // Append space and "World"
                   .insert(6, "Beautiful ")    // Insert at index 6
                   .replace(0, 5, "Goodbye")   // Replace "Hello" with "Goodbye"
                   .deleteCharAt(7)             // Delete char at index 7 ('a')
                   .reverse();                  // Reverse the whole thing

            System.out.println("\nFinal message: " + message.toString()); // Output: dlroW lufitueB eyebdooG

            // PITFALL: Forgetting toString() when needed
            // String finalStr = message; // Compile Error! Cannot assign StringBuilder to String directly
            String finalStr = message.toString(); // Correct
        }
    }
    ```
    *   **Potential Pitfalls:**
        *   **Mutability Side Effects:** Since `StringBuilder` is mutable, passing it to a method allows that method to change the original object's content. Be aware of this if you expect string-like immutability.
        *   **Forgetting `toString()`:** When you need a standard `String` object (e.g., to pass to a method expecting `String`, or for final output), you must call `.toString()` on the `StringBuilder`.
        *   **Thread Safety:** Using a single `StringBuilder` instance across multiple threads without external synchronization can lead to corrupted data. Use `StringBuffer` or manage synchronization yourself if needed.

---

---
---
---

Okay, Scholar! Let's dive into Unit III, focusing on the core pillars of Object-Oriented Programming beyond the basics: Inheritance, Polymorphism, and Abstraction. We'll format this using Obsidian-friendly Markdown.

```markdown
# Unit III: Inheritance, Polymorphism, and Abstraction

This unit explores how classes can relate to each other, enabling code reuse, flexibility, and robust design patterns.

---

## Inheritance

Inheritance is a fundamental OOP mechanism where a new class (subclass or derived class) acquires the properties (fields) and behaviors (methods) of an existing class (superclass or base class). It represents an **"is-a"** relationship.

-   **Keyword:** `extends`
-   **Purpose:**
    -   **Code Reuse:** Avoid duplicating code by inheriting common attributes and methods from a superclass.
    -   **Hierarchy:** Create logical classifications (e.g., `Dog` *is an* `Animal`).
    -   **Polymorphism:** Enables treating objects of subclasses as objects of their superclass type (more later).

### Example: Animal Hierarchy

```java
// File: Animal.java
package study.unit3;

public class Animal {
    protected String name; // Accessible by subclasses
    private int age;     // Private, not directly accessible by subclasses

    public Animal(String name, int age) {
        System.out.println("Animal constructor called");
        this.name = name;
        this.age = age;
    }

    public void eat() {
        System.out.println(name + " is eating.");
    }

    public void sleep() {
        System.out.println(name + " is sleeping.");
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }

    // Getter for private field
    public int getAge() {
        return age;
    }
}

// File: Dog.java
package study.unit3;

// Dog inherits from Animal
public class Dog extends Animal {
    private String breed;

    // Constructor must call superclass constructor (implicitly or explicitly)
    public Dog(String name, int age, String breed) {
        super(name, age); // Explicit call to Animal's constructor
        System.out.println("Dog constructor called");
        this.breed = breed;
        // this.name = name; // Can access protected 'name' directly
        // this.age = age; // ERROR: 'age' is private in Animal
    }

    // Dog-specific method
    public void bark() {
        // Accessing inherited protected member 'name'
        System.out.println(name + " the " + breed + " says: Woof!");
    }

    // Method accessing inherited public getter
    public void showAge() {
         System.out.println(name + " is " + getAge() + " years old."); // Uses inherited getAge()
    }

    // We'll override displayInfo later
}

// File: InheritanceDemo.java
package study.unit3;

public class InheritanceDemo {
    public static void main(String[] args) {
        System.out.println("Creating Animal object:");
        Animal genericAnimal = new Animal("Creature", 5);
        genericAnimal.eat();
        genericAnimal.displayInfo();

        System.out.println("\nCreating Dog object:");
        Dog myDog = new Dog("Buddy", 3, "Golden Retriever");
        myDog.eat();    // Inherited method
        myDog.sleep();  // Inherited method
        myDog.bark();   // Dog-specific method
        myDog.displayInfo(); // Inherited method (currently uses Animal's version)
        myDog.showAge(); // Uses inherited getter
    }
}
```

> **Potential Pitfalls:**
>
> -   **Tight Coupling:** Changes in the superclass can break subclasses unexpectedly (Fragile Base Class problem).
> -   **Complexity:** Deep inheritance hierarchies can become hard to understand and maintain.
> -   **Private Members:** Subclasses cannot directly access `private` members of the superclass. They must use `public` or `protected` methods (like getters/setters) if access is needed.
> -   **Constructors:** Constructors are *not* inherited. Subclass constructors *must* call a superclass constructor (using `super()`), either explicitly or implicitly (Java adds an implicit `super();` call if the superclass has a no-arg constructor and you don't explicitly call one). If the superclass *only* has parameterized constructors, the subclass *must* explicitly call one using `super(...)`.

---

## Method Overriding

Method overriding allows a subclass to provide a specific implementation for a method that is already defined in its superclass. The overridden method in the subclass *replaces* the superclass's version for objects of the subclass type.

-   **Annotation:** `@Override` (optional but highly recommended - helps catch errors at compile time).
-   **Rules:**
    1.  **Same Signature:** Method name and parameter list (number, type, order) must be exactly the same.
    2.  **Compatible Return Type:** Return type must be the same or a *subtype* (covariant return type).
    3.  **Access Modifier:** Cannot be *more* restrictive than the superclass method (e.g., if superclass is `public`, override cannot be `protected` or `private`). Can be *less* restrictive (e.g., `protected` -> `public`).
    4.  **Exception Handling:** Cannot throw *new* or *broader* checked exceptions than the superclass method. Can throw narrower checked exceptions, any unchecked exceptions, or no exceptions.
    5.  `final` methods cannot be overridden.
    6.  `static` methods cannot be overridden (they can be *hidden* - see below).

### Example: Overriding `displayInfo`

```java
// Add this method inside the Dog class from the previous example

    @Override // Good practice! Compiler checks if this actually overrides something.
    public void displayInfo() {
        // Call the superclass version first using 'super'
        System.out.print("Dog Info -> ");
        super.displayInfo(); // Calls Animal's displayInfo()
        // Add Dog-specific info
        System.out.println("   Breed: " + breed);
    }

    // Let's try overriding eat() too
    @Override
    public void eat() {
        System.out.print(name + " the " + breed + " is eating. ");
        // Maybe add specific behavior
        if (getAge() < 1) {
            System.out.println("Eating puppy food!");
        } else {
            System.out.println("Eating regular dog food.");
        }
    }

    // Attempting to override a static method (HIDING, not overriding)
    // Add to Animal class:
    // public static void staticMethod() { System.out.println("Static method in Animal"); }
    // Add to Dog class:
    // @Override // COMPILE ERROR! Static methods cannot be overridden.
    // public static void staticMethod() { System.out.println("Static method in Dog"); }
    // If you remove @Override, it compiles, but it's method HIDING.
    // Animal.staticMethod() calls Animal's version.
    // Dog.staticMethod() calls Dog's version.
    // Animal ref = new Dog(); ref.staticMethod(); // Calls Animal's version (resolved at compile time based on reference type)
```

> **Potential Pitfalls:**
>
> -   **Accidental Overloading:** If the signature (parameters) is slightly different, you create a *new*, overloaded method instead of overriding. `@Override` prevents this.
> -   **Breaking Liskov Substitution Principle (LSP):** An overridden method should still fulfill the contract of the superclass method. Subtypes should be substitutable for their base types without altering the correctness of the program. Changing the fundamental meaning or constraints in an override can violate LSP.
> -   **Access Modifier Errors:** Trying to make an overridden method more private (e.g., `public` in superclass to `protected` in subclass) causes a compile error.
> -   **Static Method Confusion:** Static methods belong to the class, not the object. They are resolved at compile time based on the *reference type*, not the *object type*. This is called **hiding**, not overriding. Using `@Override` on a static method is an error.

---

## `super` Keyword

The `super` keyword is a reference variable used to refer to the immediate parent class object.

-   **Uses:**
    1.  **`super()`:** Calls the constructor of the immediate superclass.
        -   Must be the *very first statement* in the subclass constructor.
        *   Used to initialize the inherited parts of the object.
    2.  **`super.methodName()`:** Calls a method from the immediate superclass.
        -   Useful when overriding a method but still wanting to execute the superclass's logic.
    3.  **`super.fieldName`:** Accesses a field from the immediate superclass.
        -   Less common, especially if fields are private. Usually preferred to use inherited getters/setters. Only works for `public` or `protected` fields (or default access within the same package).

### Example: Using `super`

```java
// See the Dog constructor in the first example:
// super(name, age); // Calls Animal(String, int) constructor

// See the overridden displayInfo method in the second example:
// super.displayInfo(); // Calls Animal's displayInfo() method

class Vehicle {
    protected int speed;
    public Vehicle(int speed) { this.speed = speed; }
    public void displaySpeed() { System.out.println("Vehicle Speed: " + speed); }
}

class Car extends Vehicle {
    private int speed; // Shadowing the superclass 'speed' field

    public Car(int vehicleSpeed, int carSpeed) {
        super(vehicleSpeed); // Call Vehicle constructor
        this.speed = carSpeed; // Set Car's own 'speed' field
    }

    @Override
    public void displaySpeed() {
        System.out.println("Car Speed: " + this.speed); // Access Car's speed
        System.out.println("Vehicle Speed (from super): " + super.speed); // Access Vehicle's speed using super.fieldName
        super.displaySpeed(); // Call Vehicle's displaySpeed method
    }

    public static void main(String[] args) {
         Car myCar = new Car(60, 120);
         myCar.displaySpeed();
    }
}
/* Output:
Car Speed: 120
Vehicle Speed (from super): 60
Vehicle Speed: 60
*/
```

> **Potential Pitfalls:**
>
> -   **`super()` Call Position:** Calling `super()` anywhere other than the first line of a constructor is a compile error.
> -   **Missing `super()` Call:** If the superclass lacks a no-arg constructor and the subclass constructor doesn't explicitly call a parameterized `super(...)` constructor, it's a compile error.
> -   **Confusing `this.field` and `super.field`:** When instance variables are shadowed (same name in sub and superclass), be careful to use `this` or `super` correctly to access the intended variable. Shadowing is often discouraged for clarity.

---

## `Object` Class (`java.lang.Object`)

The `Object` class is the ultimate root of *every* class hierarchy in Java. All classes, including arrays and enums, implicitly extend `Object` if they don't explicitly extend another class. It provides fundamental methods inherited by all objects.

-   **Key Methods:**
    -   `String toString()`: Returns a string representation of the object. Default implementation provides class name and hash code (e.g., `study.unit3.Dog@15db9742`). **Should be overridden** to provide a meaningful representation.
    -   `boolean equals(Object obj)`: Compares this object to the specified object for equality. Default implementation checks for reference equality (`==`). **Should be overridden** to define logical equality based on object state.
    -   `int hashCode()`: Returns a hash code value (an integer) for the object. Used by hash-based collections like `HashMap`, `HashSet`. **Must be overridden** whenever `equals()` is overridden to maintain the contract.
    -   `Class<?> getClass()`: Returns the runtime class of the object.
    -   `protected Object clone()`: Creates and returns a copy of the object (complex topic involving `Cloneable` interface).
    -   `protected void finalize()`: Called by the garbage collector before reclaiming an object (rarely used, unpredictable).
    -   `wait()`, `notify()`, `notifyAll()`: Used for thread synchronization (concurrency topic).

### Overriding `toString()` and `equals()` (and `hashCode()`)

```java
// File: Point.java
package study.unit3;

import java.util.Objects; // Helper class for equals/hashCode

public class Point /* implicitly extends Object */ {
    private int x;
    private int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    // --- Overriding toString() ---
    @Override
    public String toString() {
        // Provide a meaningful representation
        return "Point[x=" + x + ", y=" + y + "]";
    }

    // --- Overriding equals() ---
    @Override
    public boolean equals(Object obj) {
        // 1. Reference equality check (optimization)
        if (this == obj) {
            return true;
        }
        // 2. Null check and type check
        if (obj == null || getClass() != obj.getClass()) {
            // getClass() check ensures obj is a Point, not a subclass (strict equality)
            // Alternatively, use 'instanceof Point' for broader compatibility (allows subclasses)
            // if (!(obj instanceof Point)) { return false; }
            return false;
        }
        // 3. Cast the object to the correct type
        Point other = (Point) obj;
        // 4. Compare relevant fields for equality
        return this.x == other.x && this.y == other.y;
    }

    // --- Overriding hashCode() ---
    // **CONTRACT:** If two objects are equal according to equals(),
    // they MUST have the same hashCode().
    @Override
    public int hashCode() {
        // Use Objects.hash() utility for easy and good hash code generation
        return Objects.hash(x, y);

        // Manual calculation (example):
        // int result = 17; // Start with a non-zero prime
        // result = 31 * result + x; // 31 is a commonly used prime multiplier
        // result = 31 * result + y;
        // return result;
    }

    public static void main(String[] args) {
        Point p1 = new Point(10, 20);
        Point p2 = new Point(10, 20);
        Point p3 = new Point(5, 15);
        Point p4 = p1; // p4 refers to the same object as p1

        // toString() Demo
        System.out.println("p1: " + p1); // Uses overridden toString() -> Point[x=10, y=20]
        System.out.println("p3: " + p3.toString()); // Explicit call -> Point[x=5, y=15]

        // equals() Demo
        System.out.println("\nEquality Checks:");
        System.out.println("p1 == p2: " + (p1 == p2));     // false (different objects)
        System.out.println("p1.equals(p2): " + p1.equals(p2)); // true (overridden equals checks state)
        System.out.println("p1 == p4: " + (p1 == p4));     // true (same object)
        System.out.println("p1.equals(p4): " + p1.equals(p4)); // true (same object)
        System.out.println("p1.equals(p3): " + p1.equals(p3)); // false (different state)
        System.out.println("p1.equals(null): " + p1.equals(null)); // false (handled in equals)
        System.out.println("p1.equals(\"text\"): " + p1.equals("text")); // false (handled in equals)

        // hashCode() Demo
        System.out.println("\nHash Codes:");
        System.out.println("p1 hashCode: " + p1.hashCode());
        System.out.println("p2 hashCode: " + p2.hashCode()); // Must be same as p1 because p1.equals(p2)
        System.out.println("p3 hashCode: " + p3.hashCode()); // Likely different
        System.out.println("p4 hashCode: " + p4.hashCode()); // Must be same as p1

        // Example using HashMap (relies on equals/hashCode)
        java.util.Map<Point, String> map = new java.util.HashMap<>();
        map.put(p1, "Point One");
        // If hashCode wasn't overridden correctly, this might fail!
        System.out.println("Value for p2 in map: " + map.get(p2)); // Should find "Point One"
    }
}
```

> **Potential Pitfalls:**
>
> -   **Forgetting `toString()`:** Objects print cryptic default representations, making debugging harder.
> -   **Incorrect `equals()` Implementation:** Must satisfy the contract:
>     -   *Reflexive:* `x.equals(x)` must be true.
>     -   *Symmetric:* `x.equals(y)` must be true if and only if `y.equals(x)` is true.
>     -   *Transitive:* If `x.equals(y)` and `y.equals(z)`, then `x.equals(z)` must be true.
>     -   *Consistent:* Multiple calls to `x.equals(y)` must consistently return the same result (unless state changes).
>     -   `x.equals(null)` must be false.
> -   **Violating `equals()`/`hashCode()` Contract:** If `equals()` is overridden, `hashCode()` *must* also be overridden such that equal objects produce the same hash code. Failure to do so breaks hash-based collections (`HashMap`, `HashSet`, `Hashtable`). Unequal objects *may* have the same hash code (collision), but equal objects *must*.

---

## `final` Keyword

The `final` keyword is a non-access modifier used to restrict modifications.

-   **Uses:**
    1.  **`final` variable:** Creates a constant. Its value cannot be changed after initialization.
        -   Must be initialized either at declaration or in the constructor (for instance variables) or static initializer block (for static variables).
    2.  **`final` method:** Cannot be overridden by subclasses. Ensures specific behavior cannot be altered down the hierarchy.
    3.  **`final` class:** Cannot be extended (subclassed). Prevents inheritance. Useful for security or ensuring immutability (like `String`).

### Example: Using `final`

```java
// File: FinalDemo.java
package study.unit3;

class BaseClass {
    final double PI = 3.14159; // Final instance variable (constant per object)
    static final int MAX_USERS = 100; // Final static variable (class constant)

    final String config; // Blank final - must be initialized in constructor

    public BaseClass(String config) {
        this.config = config; // Initialize blank final
        // PI = 3.1; // ERROR: Cannot reassign final variable PI
    }

    public final void finalMethod() { // Cannot be overridden
        System.out.println("This is a final method in BaseClass.");
    }

    public void regularMethod() {
        System.out.println("This is a regular method in BaseClass.");
    }
}

final class FinalClass extends BaseClass { // This class cannot be extended further

    public FinalClass(String config) {
        super(config);
    }

    // @Override
    // public void finalMethod() { // ERROR: Cannot override final method
    //     System.out.println("Trying to override final method.");
    // }

    @Override
    public void regularMethod() { // OK to override non-final methods
        System.out.println("Overridden regular method in FinalClass.");
    }
}

// class SubFinal extends FinalClass { // ERROR: Cannot inherit from final FinalClass
// }

public class FinalDemo {
    public static void main(String[] args) {
        FinalClass fc = new FinalClass("AppConfig");
        System.out.println("PI: " + fc.PI);
        System.out.println("Max Users: " + BaseClass.MAX_USERS); // Access static final via class name
        System.out.println("Config: " + fc.config);

        fc.finalMethod();
        fc.regularMethod();
    }
}
```

> **Potential Pitfalls:**
>
> -   **Over-restriction:** Using `final` on classes or methods can limit flexibility and reuse if inheritance or overriding might be genuinely useful later.
> -   **Blank Finals:** Forgetting to initialize a `final` instance variable in all constructors (or at declaration) results in a compile error. Similarly for `static final` variables and static initializers.

---

## Polymorphism and `instanceof` Operator

**Polymorphism** (from Greek, meaning "many forms") is the ability of an object reference variable to refer to objects of its own type *or* any of its subtypes. The specific method implementation that gets executed is determined at **runtime** based on the *actual type of the object* being referred to, not the type of the reference variable. This is also known as **dynamic method dispatch** or late binding.

-   **Requirement:** Inheritance (or interface implementation) and method overriding.

**`instanceof` Operator:** A binary operator used to test if an object is an instance of a particular class, a subclass of that class, or an instance of a class that implements a particular interface.

-   **Syntax:** `objectReference instanceof Type`
-   **Returns:** `boolean` (`true` if the object is compatible with `Type`, `false` otherwise).
-   **`null` Check:** `null instanceof Type` always returns `false`.

### Example: Polymorphism and `instanceof`

```java
// Using Animal and Dog classes from earlier examples
// Add a Cat class:
// File: Cat.java
package study.unit3;

public class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println(name + " the cat is delicately eating.");
    }

    // Cat-specific method
    public void meow() {
        System.out.println(name + " says: Meow!");
    }
}


// File: PolymorphismDemo.java
package study.unit3;

public class PolymorphismDemo {
    public static void main(String[] args) {
        // Polymorphic references: Animal reference holding different Animal subtypes
        Animal myPet; // Reference of superclass type

        myPet = new Dog("Buddy", 3, "Retriever"); // Holds a Dog object
        System.out.println("--- Pet is a Dog ---");
        myPet.displayInfo(); // Calls Dog's overridden displayInfo()
        myPet.eat();         // Calls Dog's overridden eat()
        // myPet.bark(); // ERROR: bark() is not defined in the Animal class (reference type)

        System.out.println("\n--- Pet is now a Cat ---");
        myPet = new Cat("Whiskers", 2); // Holds a Cat object
        myPet.displayInfo(); // Calls Animal's displayInfo() (Cat didn't override it)
        myPet.eat();         // Calls Cat's overridden eat()
        // myPet.meow(); // ERROR: meow() is not defined in the Animal class

        System.out.println("\n--- Processing Animals ---");
        Animal[] zoo = new Animal[3];
        zoo[0] = new Dog("Rex", 5, "German Shepherd");
        zoo[1] = new Cat("Snowball", 1);
        zoo[2] = new Animal("Generic", 10); // Base Animal object

        // Polymorphism in action: loop treats all as Animals,
        // but specific overridden methods are called.
        for (Animal animal : zoo) {
            System.out.println("Processing: " + animal.name);
            animal.eat(); // Dynamic dispatch: Calls Dog's, Cat's, or Animal's eat()

            // --- Using instanceof for specific actions ---
            if (animal instanceof Dog) {
                System.out.println("   It's a Dog!");
                // Safe to cast now to access Dog-specific methods
                Dog specificDog = (Dog) animal;
                specificDog.bark();
            } else if (animal instanceof Cat) {
                System.out.println("   It's a Cat!");
                Cat specificCat = (Cat) animal;
                specificCat.meow();
            } else {
                System.out.println("   It's just a generic Animal.");
            }
            System.out.println("-----");
        }

        // instanceof with null
        Animal nullAnimal = null;
        System.out.println("null instanceof Animal: " + (nullAnimal instanceof Animal)); // false
    }
}
```

> **Potential Pitfalls:**
>
> -   **Compile Errors with Specific Methods:** Trying to call a subclass-specific method using a superclass reference results in a compile error because the compiler only knows about methods defined in the reference type (`Animal` in the example).
> -   **`ClassCastException`:** Attempting to cast an object to an incompatible type (e.g., casting an `Animal` reference holding a `Cat` object to a `Dog`) throws a `ClassCastException` at runtime. `instanceof` should be used *before* casting to prevent this.
> -   **Overuse of `instanceof`:** While necessary sometimes, excessive `if/else if` chains based on `instanceof` can indicate a design problem. Often, the behavior differences should be handled by overriding methods in the subclasses, letting polymorphism do the work naturally.

---

## Abstract Class and Interface

Both abstract classes and interfaces are used to achieve **abstraction**, hiding implementation details and defining contracts. They cannot be instantiated directly.

### Abstract Method & Abstract Class

-   **Abstract Method:** A method declared with the `abstract` keyword and no implementation (no `{}` body, ends with `;`).
    -   `public abstract void draw();`
-   **Abstract Class:** A class declared with the `abstract` keyword.
    -   **Cannot be instantiated** using `new`.
    -   **Can contain:**
        -   Abstract methods (must be implemented by concrete subclasses).
        -   Concrete (non-abstract) methods (with implementation, inherited by subclasses).
        -   Instance variables (state).
        -   Constructors (called via `super()` from subclass constructors).
        -   Static methods, static fields.
    -   If a class contains even *one* abstract method, the class itself *must* be declared `abstract`.
    -   A class that extends an abstract class must either implement *all* inherited abstract methods or be declared `abstract` itself.
    -   Represents an "is-a" relationship with a focus on providing a common base with potentially some default implementation.

### Example: Abstract Shape Class

```java
// File: Shape.java
package study.unit3.abstractpkg;

// Abstract class - cannot be instantiated
public abstract class Shape {
    private String color;
    private static int shapeCount = 0;

    public Shape(String color) {
        this.color = color;
        shapeCount++;
        System.out.println("Shape constructor called (Color: " + color + ")");
    }

    // Abstract method - no implementation, must be overridden by concrete subclasses
    public abstract double getArea();

    // Abstract method
    public abstract void draw();

    // Concrete method - provides implementation, inherited by all subclasses
    public String getColor() {
        return color;
    }

    // Static method
    public static int getShapeCount() {
        return shapeCount;
    }
}

// File: Circle.java
package study.unit3.abstractpkg;

// Concrete subclass - MUST implement all abstract methods from Shape
public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color); // Call abstract class constructor
        this.radius = radius;
        System.out.println("Circle constructor called");
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a " + getColor() + " circle with radius " + radius);
    }
}

// File: Rectangle.java
package study.unit3.abstractpkg;

public class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(String color, double width, double height) {
        super(color);
        this.width = width;
        this.height = height;
        System.out.println("Rectangle constructor called");
    }

    @Override
    public double getArea() {
        return width * height;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a " + getColor() + " rectangle with width " + width + " and height " + height);
    }
}

// File: AbstractDemo.java
package study.unit3.abstractpkg;

public class AbstractDemo {
    public static void main(String[] args) {
        // Shape myShape = new Shape("Red"); // ERROR: Cannot instantiate abstract class Shape

        Shape circle = new Circle("Red", 5.0);
        Shape rectangle = new Rectangle("Blue", 4.0, 6.0);

        System.out.println("\n--- Processing Shapes ---");
        Shape[] shapes = {circle, rectangle};

        for (Shape s : shapes) {
            s.draw(); // Polymorphic call to draw()
            System.out.println("   Color: " + s.getColor()); // Call concrete method from Shape
            System.out.println("   Area: " + s.getArea());   // Polymorphic call to getArea()
            System.out.println("-----");
        }

        System.out.println("Total shapes created: " + Shape.getShapeCount()); // Call static method
    }
}
```

### Interface

-   An `interface` defines a **contract** of what implementing classes *must* do. It specifies method signatures but (traditionally) not implementations.
-   **Cannot be instantiated** using `new`.
-   **Can contain:**
    -   Abstract methods (implicitly `public abstract` before Java 8; `public` is still implicit).
    -   Constants (implicitly `public static final`).
    -   **Java 8+:** `default` methods (implicitly `public`, have an implementation, inherited by implementing classes, can be overridden). Provide default behavior without breaking existing implementations.
    -   **Java 8+:** `static` methods (implicitly `public`, belong to the interface, must be called using `InterfaceName.staticMethod()`). Utility methods related to the interface.
    -   **Java 9+:** `private` methods (static or instance) to help organize code within the interface (helper methods for default/static methods).
-   A class uses the `implements` keyword to implement an interface.
-   A class can implement **multiple** interfaces (unlike `extends`, which is limited to one class).
-   Represents a "can-do" or "has-a" capability relationship (e.g., a `Bird` *can* `Fly`, a `Plane` *can* `Fly`).

### Example: `Drawable` and `Resizable` Interfaces

```java
// File: Drawable.java
package study.unit3.ifacepkg;

public interface Drawable {
    // Constant (implicitly public static final)
    String DEFAULT_COLOR = "Black";

    // Abstract method (implicitly public abstract)
    void draw();

    // Default method (Java 8+) - provides implementation
    default void printInfo() {
        System.out.println("Drawable object. Default Color: " + DEFAULT_COLOR);
        // privateHelper(); // Can call private methods (Java 9+)
    }

    // Static method (Java 8+)
    static void staticUtilityMethod() {
        System.out.println("Static utility method in Drawable interface.");
    }

    // Private method (Java 9+) - helper for default/static methods
    // private void privateHelper() {
    //     System.out.println("Private helper method in Drawable.");
    // }
}

// File: Resizable.java
package study.unit3.ifacepkg;

public interface Resizable {
    void resize(double factor);
}

// File: Square.java
package study.unit3.ifacepkg;

// Square implements BOTH Drawable and Resizable
public class Square implements Drawable, Resizable {
    private double side;
    private String color = Drawable.DEFAULT_COLOR; // Use interface constant

    public Square(double side) {
        this.side = side;
    }

    @Override // From Drawable
    public void draw() {
        System.out.println("Drawing a " + color + " square with side " + side);
    }

    @Override // From Resizable
    public void resize(double factor) {
        System.out.println("Resizing square by factor " + factor);
        this.side *= factor;
    }

    // Optionally override the default method
    @Override
    public void printInfo() {
        System.out.println("Square Info - Side: " + side + ", Color: " + color);
    }

    public double getArea() {
        return side * side;
    }
}

// File: Button.java
package study.unit3.ifacepkg;

// Button only implements Drawable
public class Button implements Drawable {
    private String label;

    public Button(String label) {
        this.label = label;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a button with label: [" + label + "]");
    }
    // Inherits the default printInfo() method from Drawable
}


// File: InterfaceDemo.java
package study.unit3.ifacepkg;

public class InterfaceDemo {
    public static void main(String[] args) {
        // Call static method on interface
        Drawable.staticUtilityMethod();

        Square square = new Square(10.0);
        Button button = new Button("Submit");

        System.out.println("\n--- Processing Drawable Objects ---");
        Drawable[] drawables = {square, button};

        for (Drawable d : drawables) {
            d.draw();      // Polymorphic call to draw()
            d.printInfo(); // Calls Square's override or Button's inherited default

            // Check if it's also Resizable
            if (d instanceof Resizable) {
                System.out.println("   Object is Resizable.");
                Resizable r = (Resizable) d; // Safe cast
                r.resize(1.5);
                // After resize, call draw again to see effect (if applicable)
                d.draw();
            } else {
                 System.out.println("   Object is NOT Resizable.");
            }
             System.out.println("-----");
        }
    }
}
```

### Abstract Class vs. Interface

| Feature             | Abstract Class                     | Interface                          |
| :------------------ | :--------------------------------- | :--------------------------------- |
| **Instantiation**   | Cannot be instantiated             | Cannot be instantiated             |
| **Methods**         | Abstract & Concrete                | Abstract, `default`, `static`      |
| **Variables**       | Instance & Static (any modifier)   | Constants (`public static final`)  |
| **Constructors**    | Can have constructors              | Cannot have constructors           |
| **Inheritance**     | `extends` (Single class)           | `implements` (Multiple interfaces) |
| **Relationship**    | "is-a" (Stronger type relation)    | "can-do" / "has-a" (Capability)    |
| **Purpose**         | Share common code/state            | Define a contract/API              |
| **When to Use**     | Base for closely related classes   | Define capabilities for unrelated classes |

> **Potential Pitfalls:**
>
> -   **Forgetting Implementation:** A concrete class extending an abstract class or implementing an interface *must* provide implementations for all inherited abstract methods, or it must itself be declared abstract.
> -   **Multiple Inheritance Issues (Diamond Problem):** If a class implements two interfaces that have `default` methods with the *same signature*, the implementing class *must* explicitly override that method to resolve the ambiguity.
> -   **Confusion:** Choosing between an abstract class and an interface depends on the design goal. Use abstract classes for object blueprints with shared state/implementation, interfaces for defining capabilities/contracts.


---
---
---
---
Okay, Scholar! Let's delve into Unit IV. This unit introduces more advanced concepts like nested classes, functional programming with lambdas, essential utilities like the Date/Time API, and robust error handling with exceptions and assertions. We'll focus on the *why* and *where things go wrong*.

```markdown
# Unit IV: Nested Classes, Lambdas, Utilities, and Error Handling

This unit moves into more sophisticated Java features that enhance code organization, enable modern programming paradigms, provide essential tools, and ensure program robustness.

---

## 1. Nested Classes

Nested classes are classes defined *within* another class. They allow logical grouping of classes used in one place, increase encapsulation, and can lead to more readable and maintainable code.

**Core Concept:** A class defined inside another class.

**Types & Theory:**

1.  **Static Nested Class:**
    -   **Declared:** Using the `static` keyword within the outer class.
        ```java
        class Outer {
            static class StaticNested { /* ... */ }
        }
        ```
    -   **Behavior:** Behaves much like a regular top-level class but is namespaced within the outer class.
    -   **Access:**
        -   *Cannot* directly access non-static (instance) members (variables or methods) of the outer class. It doesn't have an implicit reference to an outer class instance.
        -   *Can* access static members of the outer class directly (including private ones).
        -   Can be instantiated without an instance of the outer class: `Outer.StaticNested nestedObj = new Outer.StaticNested();`
    -   **Use Case:** Grouping utility classes or helper classes closely related to the outer class, where they don't need access to the outer class's instance state (e.g., `Map.Entry` is conceptually like a static nested class within `Map`).

2.  **Non-Static Nested Class (Inner Class):**
    -   **Declared:** Without the `static` keyword.
    -   **Behavior:** Each instance of an inner class is *implicitly associated* with an instance of the outer class.
    -   **Access:**
        -   *Can* access *all* members (static and non-static, including private) of the enclosing outer class instance directly.
        -   Holds an implicit reference to the outer class instance that created it.
    -   **Instantiation:** Requires an instance of the outer class: `Outer outerObj = new Outer(); Outer.Inner innerObj = outerObj.new Inner();`
    -   **Subtypes:**
        *   **Member Inner Class:** The most common type, declared directly within the outer class body (like `Inner` above). Use case: When an object needs an intimate connection to an instance of another class (e.g., an `Iterator` implementation specific to a collection).
        *   **Local Inner Class:** Declared *inside a method body*.
            ```java
            class Outer {
                void someMethod() {
                    class LocalInner { /* ... */ }
                    LocalInner li = new LocalInner();
                    // ... use li ...
                }
            }
            ```
            -   Scope is limited to the method.
            -   Can access local variables of the method *only if* they are `final` or *effectively final* (their value doesn't change after initialization).
            -   Use Case: When a helper class is needed only within a single method. Less common than member or anonymous classes.
        *   **Anonymous Inner Class:** A local inner class *without a name*, declared and instantiated simultaneously, typically to implement an interface or extend a class on the fly.
            ```java
            interface Greeter { void greet(); }

            class Outer {
                void sayHello() {
                    // Declare and instantiate an anonymous class implementing Greeter
                    Greeter englishGreeting = new Greeter() { // Note the syntax: new InterfaceName() { ... }
                        @Override
                        public void greet() {
                            System.out.println("Hello!");
                        }
                    }; // Semicolon needed here!
                    englishGreeting.greet();
                }
            }
            ```
            -   Very concise syntax for creating simple, one-off implementations.
            -   Often used for event listeners in GUIs or simple callbacks.
            -   Can also access `final` or effectively final local variables of the enclosing method.
            -   Replaced largely by Lambda Expressions (see next section) for functional interfaces.

**Importance:**
-   **Logical Grouping:** Keeps related helper classes together with the class they serve.
-   **Encapsulation:** A nested class can be made `private` to the outer class, hiding it completely. Inner classes have privileged access to the outer class's private members, enhancing encapsulation possibilities.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Static vs. Non-Static Access Rules:** Forgetting that `static` nested classes *cannot* access outer class instance members is a frequent error. Conversely, trying to instantiate a non-static inner class without an outer class instance (`new Outer.Inner()`) fails.
2.  **`this` Keyword Ambiguity:** Inside a non-static inner class, `this` refers to the *inner class instance*. To refer to the *outer class instance*, use the qualified syntax: `OuterClassName.this`. Forgetting this leads to accessing the wrong members if names collide.
    ```java
    class Outer {
        int x = 10;
        class Inner {
            int x = 20;
            void printX() {
                System.out.println("Inner x: " + this.x); // 20
                System.out.println("Outer x: " + Outer.this.x); // 10
            }
        }
    }
    ```
3.  **Serialization:** Serializing non-static inner classes (especially anonymous/local) can be tricky because they implicitly contain a reference to the outer class instance. This means the outer instance (and potentially a large object graph) might also get serialized, which is often unintended. Static nested classes are generally safer to serialize.
4.  **Memory Leaks (Non-Static Inner Classes):** Because a non-static inner class instance holds a reference to its outer class instance, the outer instance cannot be garbage collected as long as the inner instance exists. If an inner class object has a longer lifecycle than intended (e.g., registered as a listener but never unregistered), it can prevent the outer object from being collected, leading to a memory leak. Static nested classes avoid this issue.
5.  **Local/Anonymous Class Variable Access:** Forgetting that local/anonymous classes can only access `final` or *effectively final* local variables from the enclosing scope. Trying to modify such a variable from within the inner class results in a compile error.

---

## 2. Lambda Expressions

Lambda expressions provide a concise syntax for representing anonymous functions (functions without a name). They are primarily used to provide implementations for **functional interfaces**.

**Core Concept:** An anonymous function that can be treated as a value.

**Functional Interface:**
-   An interface that contains **exactly one abstract method** (SAM - Single Abstract Method).
-   May contain `default` and `static` methods, but only one abstract method is allowed.
-   The `@FunctionalInterface` annotation is optional but recommended. It causes the compiler to verify that the interface meets the SAM requirement.
    ```java
    @FunctionalInterface // Good practice
    interface MyFunctionalInterface {
        void execute(String param); // The single abstract method
        // default void log() { /* ... */ } // OK
        // static void utility() { /* ... */ } // OK
    }
    ```

**Lambda Syntax:**
`(parameters) -> { body }`
-   **`parameters`:** A list of parameters matching the abstract method's parameters. Type declarations are often optional (inferred by the compiler). Parentheses `()` are required even for zero parameters. For a single parameter with inferred type, parentheses are optional.
-   **`->`:** The arrow token, separating parameters from the body.
-   **`body`:**
    -   For a single expression, curly braces `{}` and the `return` keyword (if applicable) can be omitted. The expression's result is implicitly returned.
    -   For multiple statements, curly braces `{}` are required, and `return` must be used explicitly if the method returns a value.

**Examples:**

```java
// Implementing MyFunctionalInterface from above
MyFunctionalInterface impl1 = (String s) -> { System.out.println("Executing with: " + s); };
MyFunctionalInterface impl2 = (s) -> System.out.println("Shorter: " + s); // Type inferred, {} omitted
MyFunctionalInterface impl3 = s -> System.out.println("Shortest: " + s); // () omitted for single param

// Example with return value
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);
}

Calculator adder = (a, b) -> a + b; // Single expression, implicit return
Calculator multiplier = (int x, int y) -> { // Explicit types, {} and return
    System.out.println("Multiplying " + x + " and " + y);
    return x * y;
};

System.out.println("Sum: " + adder.operate(5, 3));       // Output: Sum: 8
System.out.println("Product: " + multiplier.operate(5, 3)); // Output: Multiplying 5 and 3 \n Product: 15
```

**Target Typing:** The compiler determines the type of a lambda expression based on the context in which it's used (e.g., the type of the variable it's assigned to, or the type of the method parameter it's passed to). The target type *must* be a functional interface.

**Variable Capture:** Lambdas can access variables from their enclosing scope (local variables, instance variables, static variables).
-   Local variables must be `final` or *effectively final* (cannot be reassigned after initialization). The lambda captures the *value* of the variable at the time the lambda is created.

**Importance:**
-   **Conciseness:** Drastically reduces boilerplate code compared to anonymous inner classes for functional interfaces.
-   **Functional Programming:** Enables passing behavior (code) as data, facilitating functional programming styles (e.g., using Streams API).
-   **Readability:** Can make code clearer by keeping the implementation logic close to where it's used, especially for simple operations.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Target Type Must Be Functional Interface:** Trying to assign a lambda to a variable whose type is not a functional interface (or has more/less than one abstract method) is a compile error.
2.  **Syntax Variations:** The different ways to write parameters (`(int x)`, `(x)`, `x`) and bodies (`{ return x; }`, `x`) can be initially confusing.
3.  **`this` Keyword Behavior:** Inside a lambda expression, `this` refers to the instance of the *enclosing class* (lexical scoping), just like in the surrounding method. This is *different* from anonymous inner classes, where `this` refers to the instance of the anonymous class itself. This difference is crucial and often trips up developers transitioning from anonymous classes.
4.  **Effectively Final Restriction:** Forgetting that local variables accessed by a lambda must be final or effectively final. Attempting to modify such a variable either before or inside the lambda after its initial assignment leads to a compile error. This ensures the lambda captures a fixed value.
5.  **Checked Exceptions:** If the functional interface's abstract method declares checked exceptions using `throws`, the lambda body must either handle them with `try-catch` or the lambda itself must be compatible with the `throws` clause. Unhandled checked exceptions are a compile error.
6.  **Ambiguity with Overloading:** If a method is overloaded to accept different functional interfaces, the compiler might sometimes be unable to determine the correct target type for a lambda, leading to an ambiguity error. Explicit casting of the lambda can resolve this: `process((MyInterfaceType) s -> System.out.println(s));`

---

## 3. Utility Classes: Working with Dates (`java.time`)

Handling dates and times correctly is notoriously complex. Java 8 introduced the `java.time` package (JSR-310) to replace the problematic legacy `java.util.Date` and `java.util.Calendar` classes.

**Core Concept:** A modern, immutable, thread-safe, and more intuitive API for handling date and time.

**Legacy Issues (`Date`, `Calendar`) - Why `java.time` is better:**
-   **Mutability:** `Date` objects were mutable, leading to bugs in concurrent environments or when passed around.
-   **Confusing API:** `Calendar` API was cumbersome and unintuitive (e.g., month indexing started from 0).
-   **Poor Separation:** `Date` represented both date and time down to milliseconds, often leading to timezone issues. `Calendar` mixed concerns.
-   **Not Thread-Safe:** Formatting classes (`SimpleDateFormat`) were not thread-safe.

**Key `java.time` Classes:**

-   **Date/Time Representation:**
    -   `LocalDate`: Represents a date only (year, month, day), no time or timezone (e.g., `2024-03-15`). **Immutable.**
    -   `LocalTime`: Represents a time only (hour, minute, second, nanosecond), no date or timezone (e.g., `10:30:55.123456789`). **Immutable.**
    -   `LocalDateTime`: Represents both date and time, no timezone (e.g., `2024-03-15T10:30:55`). **Immutable.**
    -   `ZonedDateTime`: Represents date and time *with* a specific timezone (e.g., `2024-03-15T10:30:55+01:00[Europe/Paris]`). **Immutable.** Handles daylight saving rules.
    -   `Instant`: Represents a specific point on the timeline (nanoseconds since the epoch: 1970-01-01T00:00:00Z), independent of timezone (usually UTC). Machine-friendly. **Immutable.**
-   **Duration & Period:**
    -   `Duration`: Represents a time-based amount (seconds, nanoseconds). Useful for measuring machine time between `Instant`s or `LocalTime`s.
    -   `Period`: Represents a date-based amount (years, months, days). Useful for differences between `LocalDate`s.
-   **Formatting & Parsing:**
    -   `DateTimeFormatter`: Used to convert date/time objects to strings (`format`) and parse strings into date/time objects (`parse`). **Immutable and thread-safe.** Provides predefined formatters (e.g., `ISO_DATE_TIME`) and allows custom patterns.

**Example Snippets:**

```java
import java.time.*;
import java.time.format.*;
import java.time.temporal.ChronoUnit;

// Creating instances
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.of(2024, Month.MARCH, 15, 10, 30);
ZonedDateTime zoned = ZonedDateTime.now(ZoneId.of("Europe/London"));
Instant instant = Instant.now();

// Immutability: Methods return NEW objects
LocalDate tomorrow = today.plusDays(1);
LocalDateTime earlier = dateTime.minusHours(2);

// Calculating differences
Period period = Period.between(today, tomorrow); // P1D (Period of 1 Day)
Duration duration = Duration.between(now, now.plusSeconds(65)); // PT1M5S (Duration of 1 Minute 5 Seconds)
long daysBetween = ChronoUnit.DAYS.between(today, LocalDate.of(2025, 1, 1));

// Formatting and Parsing
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm");
String formatted = dateTime.format(formatter); // "15/03/2024 10:30"
LocalDateTime parsed = LocalDateTime.parse("20/04/2023 14:00", formatter);
```

**Importance:**
-   **Clarity & Correctness:** Provides clear, specific classes for different needs (date, time, datetime, zoned, instant).
-   **Immutability & Thread Safety:** Prevents accidental modification and makes the API safe for concurrent use.
-   **Fluent API:** Methods like `plusDays`, `minusHours`, `withMonth` make manipulation intuitive.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Mixing Legacy and Modern APIs:** Accidentally using `java.util.Date` where `java.time.LocalDate` is needed, or vice-versa. Conversion methods exist (`Date.toInstant()`, `Timestamp.toLocalDateTime()`) but require care.
2.  **Forgetting Immutability:** Expecting methods like `plusDays()` to modify the original object. You *must* capture the returned new object: `today = today.plusDays(1);`.
3.  **Choosing `Period` vs. `Duration`:** Using `Duration` to calculate the difference between `LocalDate`s or `Period` between `LocalTime`s is incorrect. Use `Period` for date-based amounts, `Duration` for time-based amounts.
4.  **Timezone Handling:** Assuming `LocalDateTime` has timezone information (it doesn't). For timezone-sensitive operations, use `ZonedDateTime` or `Instant`. Incorrectly handling timezones and daylight saving time is a major source of bugs.
5.  **Parsing/Formatting Patterns:** Providing an incorrect pattern string to `DateTimeFormatter.ofPattern()` that doesn't match the input string (for parsing) or desired output (for formatting) leads to `DateTimeParseException` or incorrect output. Case sensitivity matters (e.g., `MM` for month, `mm` for minute; `yyyy` for year, `YYYY` for week-based year).
6.  **Default Timezone:** Methods like `LocalDate.now()` use the system's default timezone. This can cause issues if the application runs on servers with different default timezones. It's often safer to explicitly provide a `ZoneId` or `Clock` where possible.

---

## 4. Exceptions and Assertions

Mechanisms for handling errors and validating assumptions during program execution.

**Core Concept (Exceptions):** An event that occurs during program execution that disrupts the normal flow of instructions. Java uses objects to represent exceptions.

**Exception Hierarchy:**
-   `Throwable`: Root class for all errors and exceptions.
    -   `Error`: Represents serious problems usually outside the application's control (e.g., `OutOfMemoryError`, `StackOverflowError`). Generally *not* caught or handled by applications.
    -   `Exception`: Represents conditions that applications *might* want to catch and handle.
        -   **Checked Exceptions:** Subclasses of `Exception` (but *not* subclasses of `RuntimeException`). The compiler *checks* that these are handled (caught or declared using `throws`). Indicate exceptional conditions that a well-written application should anticipate and recover from (e.g., `IOException`, `SQLException`, `ClassNotFoundException`).
        -   **Unchecked Exceptions (Runtime Exceptions):** Subclasses of `RuntimeException`. The compiler does *not* require handling. Often indicate programming errors (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`, `ClassCastException`) or unrecoverable runtime issues.

**Exception Handling Mechanisms:**

-   **`try-catch-finally`:**
    -   `try`: Encloses the code that might throw an exception.
    -   `catch (ExceptionType e)`: Catches and handles a specific type of exception. Multiple `catch` blocks can follow a `try`, ordered from most specific to most general type.
    -   `finally`: Optional block that *always* executes after `try` (and `catch`, if one ran), regardless of whether an exception occurred or was caught. Crucial for resource cleanup (closing files, network connections, database connections) in older code.
    ```java
    try {
        // Code that might throw IOException or NumberFormatException
        int number = Integer.parseInt(someInputString);
        writeToFile(number);
    } catch (IOException ioe) {
        System.err.println("Error writing file: " + ioe.getMessage());
        // Handle IO error
    } catch (NumberFormatException nfe) {
        System.err.println("Invalid number format: " + nfe.getMessage());
        // Handle format error
    } catch (Exception e) { // Catching broader Exception (use cautiously)
        System.err.println("An unexpected error occurred: " + e);
    } finally {
        System.out.println("Finally block always executes.");
        // closeResource(); // Cleanup (better done with try-with-resources now)
    }
    ```
-   **`throw`:** Manually throws an exception object. Used to signal an error condition.
    `throw new IllegalArgumentException("Input value must be positive.");`
-   **`throws`:** Declares that a method *might* throw one or more checked exceptions. Forces the caller of the method to either handle (using `try-catch`) or further declare the exception using `throws`.
    `public void readFile(String filename) throws IOException { /* ... */ }`
-   **Multi-catch (Java 7+):** Catch multiple exception types in a single block if the handling logic is the same.
    `catch (IOException | SQLException | NullPointerException e) { logError(e); }`
-   **Try-with-Resources (Java 7+):** Automatically closes resources declared in the `try` statement header. The resource must implement the `AutoCloseable` interface (e.g., `FileInputStream`, `Scanner`, `Connection`). This is the preferred way for resource management, replacing most uses of `finally` for closing.
    ```java
    try (FileInputStream fis = new FileInputStream("file.txt");
         Scanner scanner = new Scanner(fis)) { // Resources declared here
        // Use scanner to read from fis
    } catch (IOException e) {
        // Handle exception
    }
    // fis and scanner are automatically closed here, even if exceptions occur.
    ```

**Exception Propagation:** If an exception is thrown and not caught within the current method, it propagates up the call stack to the calling method. If it's not caught there, it continues up the stack. If it reaches the `main` method and isn't caught, the program terminates, typically printing the exception's stack trace.

**Custom Exceptions:** Define application-specific exception types by extending `Exception` (for checked) or `RuntimeException` (for unchecked). Allows more specific error handling.
```java
class InsufficientFundsException extends Exception { // Checked
    public InsufficientFundsException(String message) { super(message); }
}
```

**Assertions (`assert` keyword):**
-   **Purpose:** Validate assumptions about the program's state during development and testing. They check for conditions that *should* always be true if the code is correct.
-   **Syntax:**
    -   `assert boolean_expression;` (Throws `AssertionError` if expression is false)
    -   `assert boolean_expression : detail_message_expression;` (Includes a message in the `AssertionError`)
-   **Enabling/Disabling:** Assertions are **disabled by default**. They must be explicitly enabled at runtime using the `-enableassertions` or `-ea` JVM flag.
-   **Use Case:** Checking internal invariants, pre-conditions, post-conditions, or unreachable code sections during development. **Should NOT be used for input validation or application logic that must run in production**, as they can be disabled.

**Importance:**
-   **Robustness:** Gracefully handle errors instead of crashing.
-   **Maintainability:** Separates error handling logic from the main program flow.
-   **Debugging:** Stack traces pinpoint where exceptions occurred. Assertions help catch logical errors early.
-   **API Contracts:** Checked exceptions enforce handling of predictable external failures.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Ignoring Exceptions (Empty Catch Blocks):** `catch (Exception e) {}` or `catch (Exception e) { /* ignore */ }`. This swallows errors silently, making debugging extremely difficult. At the very least, log the exception.
2.  **Catching Too Broadly:** Catching `Exception` or `Throwable` when a more specific exception type could be caught. This can mask unrelated errors and make handling less precise. Catch the most specific exceptions first.
3.  **Checked vs. Unchecked Misuse:**
    -   Overusing checked exceptions for conditions that are essentially programming errors (which should be `RuntimeException`).
    -   Treating recoverable conditions as unchecked exceptions, forcing callers to guess potential failures.
    -   Wrapping checked exceptions in `RuntimeException` excessively can undermine the purpose of checked exceptions.
4.  **Resource Leaks:** Forgetting to close resources (files, streams, connections) in a `finally` block (pre-Java 7) or not using try-with-resources (Java 7+). This can exhaust system resources.
5.  **Swallowing Original Cause:** When catching an exception and throwing a new one, failing to include the original exception as the *cause* (`throw new MyException("Wrapper message", originalException);`). This loses valuable debugging information from the stack trace.
6.  **Using Assertions for Application Logic:** Relying on `assert` for things like validating user input or checking conditions required for correct program operation in production. Assertions can (and often are) disabled, so this logic will not run, leading to incorrect behavior or security vulnerabilities. Use regular `if` statements and exceptions for application logic checks.
7.  **Exception Handling in Lambdas/Streams:** Handling checked exceptions within lambda expressions used in streams can be awkward, often requiring wrapper methods or custom functional interfaces.
8.  **`finally` Block Behavior:** Code in `finally` runs *even if* a `return`, `break`, or `continue` statement is encountered in the `try` or `catch` block. If `finally` also throws an exception, it *supersedes* any exception thrown from the `try` or `catch`.

Okay, Scholar! Let's tackle the final unit, Unit V. This brings together concepts for interacting with the outside world (I/O) and writing more flexible, type-safe code (Generics). We'll maintain our focus on the underlying theory and common areas where mistakes happen.


# Unit V: I/O Fundamentals and Generics

This unit covers essential mechanisms for handling input and output operations, enabling interaction with files and other data sources, and introduces Generics for creating highly reusable and type-safe components.

---

## 1. I/O Fundamentals (`java.io` and `java.nio`)

**Core Concept:** Input/Output (I/O) in Java revolves around the concept of **streams**, which are sequences of data flowing from a source (input stream) or to a destination (output stream).

**Theory & Key Concepts:**

1.  **Stream Types:**
    *   **Byte Streams:** Handle data as raw bytes (8-bit). Suitable for binary data (images, executable files, serialized objects). Base abstract classes: `InputStream`, `OutputStream`.
    *   **Character Streams:** Handle data as characters (16-bit Unicode). Suitable for text data, automatically handling character encoding conversions between bytes and characters. Base abstract classes: `Reader`, `Writer`.
    *   **Choosing:** Use character streams for text, byte streams for everything else.

2.  **Decorator Pattern (Wrapper Streams):** The `java.io` package heavily uses the Decorator pattern. You start with a basic stream connected to a source/destination (e.g., `FileInputStream`, `FileOutputStream`) and wrap it with other streams that add functionality (e.g., buffering, data type conversion, character encoding).
    *   Example: `new BufferedReader(new InputStreamReader(new FileInputStream("file.txt")))`
        -   `FileInputStream`: Connects to the file (byte stream).
        -   `InputStreamReader`: Adapts the byte stream into a character stream (using a specified or default character encoding).
        -   `BufferedReader`: Adds buffering for efficient reading of characters, lines, etc.

3.  **Standard Streams:** Provided by the `System` class:
    *   `System.in`: Standard input stream (usually keyboard), an `InputStream`.
    *   `System.out`: Standard output stream (usually console), a `PrintStream` (subclass of `OutputStream`).
    *   `System.err`: Standard error stream (usually console), a `PrintStream`.

4.  **Key I/O Classes (Examples):**
    *   **Byte Streams:**
        -   `FileInputStream` / `FileOutputStream`: Read/write bytes from/to files.
        -   `BufferedInputStream` / `BufferedOutputStream`: Add buffering for performance.
        -   `DataInputStream` / `DataOutputStream`: Read/write primitive Java data types in binary format.
        -   `ObjectInputStream` / `ObjectOutputStream`: Read/write serialized objects (see Serialization).
    *   **Character Streams:**
        -   `FileReader` / `FileWriter`: Read/write characters from/to files (uses default encoding - often risky!). **Prefer `InputStreamReader`/`OutputStreamWriter` with explicit encoding.**
        -   `BufferedReader` / `BufferedWriter`: Add buffering for character streams (efficient line reading/writing).
        -   `PrintWriter`: Provides convenient `print`/`println` methods for writing formatted text representations (often wraps a `Writer`).
        -   `InputStreamReader` / `OutputStreamWriter`: Bridge between byte streams and character streams, specifying character encoding.

5.  **File Class (`java.io.File`):** Represents a file or directory path name. Used for operations like checking existence (`exists()`), creating directories (`mkdir()`, `mkdirs()`), deleting (`delete()`), renaming (`renameTo()`), getting file properties (size, last modified), but *not* for reading/writing content (that's what streams are for).

6.  **NIO (`java.nio` - New I/O):** Introduced later, offers more modern and performant I/O capabilities, especially for high-volume, non-blocking operations. Key concepts include Channels, Buffers, and Selectors. While powerful, the basic `java.io` streams are often sufficient and simpler for many common tasks. (Detailed NIO is often a separate, advanced topic).

7.  **Serialization:**
    *   **Theory:** The process of converting an object's state (its instance variables) into a byte stream, which can then be saved to a file, sent over a network, etc. **Deserialization** is the reverse process: reconstructing the object from the byte stream.
    *   **`Serializable` Interface:** A marker interface (no methods). A class *must* implement `Serializable` to indicate its objects can be serialized.
    *   **`ObjectOutputStream`:** Writes serialized objects to an `OutputStream`. (`writeObject()`)
    *   **`ObjectInputStream`:** Reads serialized objects from an `InputStream`. (`readObject()`)
    *   **`transient` Keyword:** Marks an instance variable to be *excluded* from the serialization process. Its value will not be saved and will be initialized to its default (`null`, 0, `false`) upon deserialization. Use for sensitive data (like passwords) or fields that can be easily recalculated.
    *   **`serialVersionUID`:** A static final long field used for version control during deserialization. If the `serialVersionUID` of the loaded class doesn't match the `serialVersionUID` stored in the serialized object data, an `InvalidClassException` is thrown. It's strongly recommended to explicitly declare this ID (`private static final long serialVersionUID = 1L;`) to avoid compatibility issues if the class structure changes slightly. If not declared, the JVM generates one based on the class structure, which can change unexpectedly.

**Importance:**
-   **Persistence:** Saving program state or data to files.
-   **Communication:** Sending data/objects over networks.
-   **Inter-Process Communication:** Exchanging data between different programs.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Resource Leaks:** **The #1 I/O mistake.** Failing to close streams (`close()`) after use. This ties up system resources (file handles, network sockets). **Always use the try-with-resources statement (Java 7+)** to ensure streams are closed automatically, even if exceptions occur.
    ```java
    // BAD: Potential leak if exception occurs before close()
    FileInputStream fis = new FileInputStream("file.txt");
    // ... read data ...
    fis.close();

    // GOOD: try-with-resources ensures closure
    try (FileInputStream fis = new FileInputStream("file.txt")) {
        // ... read data ...
    } catch (IOException e) { /* handle */ }
    ```
2.  **Character Encoding Issues:** Using `FileReader`/`FileWriter` relies on the system's default encoding, which varies across platforms (e.g., UTF-8 on Linux/macOS, often Cp1252 on Windows). This leads to corrupted text when files are moved between systems. **Always specify the encoding explicitly** using `InputStreamReader`/`OutputStreamWriter`:
    ```java
    // GOOD: Explicit encoding
    try (BufferedReader reader = new BufferedReader(
            new InputStreamReader(new FileInputStream("file.txt"), StandardCharsets.UTF_8))) {
        // ... read lines ...
    }
    ```
3.  **Byte vs. Character Stream Confusion:** Trying to read text data using byte streams without proper character decoding, or trying to read binary data using character streams, leads to corrupted data.
4.  **Path Issues:** Hardcoding absolute file paths (`C:\Users\...`) makes the application non-portable. Use relative paths or configure paths externally. Incorrectly handling path separators (`\` vs. `/`) - `File.separator` can help, but relative paths often work fine.
5.  **`FileNotFoundException`:** Trying to read from a file that doesn't exist. Always check `file.exists()` or handle the exception appropriately. Trying to write to a directory where the application lacks permissions.
6.  **Buffering:** Reading/writing files byte-by-byte or character-by-character without buffering (`BufferedInputStream`, `BufferedReader`, etc.) is extremely inefficient for large files.
7.  **Serialization Pitfalls:**
    *   **`NotSerializableException`:** Trying to serialize an object whose class (or one of its contained non-transient object fields) does not implement `Serializable`.
    *   **`serialVersionUID` Mismatches:** Changing a class (adding/removing fields) without updating or maintaining a consistent `serialVersionUID` breaks deserialization of old data. Explicitly declare it!
    *   **Class Evolution:** Handling changes to a class structure between serialization and deserialization requires careful planning (e.g., using custom `readObject`/`writeObject` methods, `serialPersistentFields`).
    *   **Security Risks:** Deserializing data from untrusted sources is dangerous. Maliciously crafted byte streams can potentially execute arbitrary code during deserialization (Deserialization Vulnerabilities). Use with extreme caution, validate data, or consider alternative formats like JSON/XML.
    *   **`transient` Misuse:** Forgetting to mark sensitive fields as `transient`, or marking fields as `transient` that are essential for the object's state and cannot be reconstructed.

---

## 2. Generics

**Core Concept:** Generics allow you to parameterize types. This means you can define classes, interfaces, and methods that operate on types specified as parameters, enabling code reuse while providing **compile-time type safety**.

**Theory & Key Concepts:**

1.  **Motivation:** Before generics, collections like `ArrayList` stored `Object`s. This required explicit casting when retrieving elements and offered no compile-time guarantee that only the correct type of object was added.
    ```java
    // Pre-Generics (Problematic)
    List list = new ArrayList();
    list.add("Hello");
    list.add(Integer.valueOf(123)); // No compile error!
    String s = (String) list.get(0); // Needs cast
    // String oops = (String) list.get(1); // Runtime ClassCastException!
    ```
2.  **Type Parameters:** Declared using angle brackets `<...>`. Conventionally use single uppercase letters (e.g., `T` for Type, `E` for Element, `K` for Key, `V` for Value).
    ```java
    // Generic Class
    public class Box<T> { // T is the type parameter
        private T item;
        public void set(T item) { this.item = item; }
        public T get() { return item; }
    }

    // Using the Generic Class
    Box<String> stringBox = new Box<>(); // Specify String as the type argument
    stringBox.set("World");
    String content = stringBox.get(); // No cast needed!
    // stringBox.set(123); // Compile Error! Type safety.
    ```
3.  **Type Inference (Diamond Operator `<>`):** Since Java 7, you can often omit the type argument in the constructor call if the compiler can infer it from the variable declaration.
    `Box<Integer> integerBox = new Box<>(); // Compiler infers Integer`
4.  **Generic Methods:** Methods (static or instance) that introduce their own type parameters, declared *before* the return type.
    ```java
    public class Util {
        public static <T> void printArray(T[] array) { // <T> declares type parameter for this method
            for (T element : array) {
                System.out.print(element + " ");
            }
            System.out.println();
        }
    }
    // Usage:
    // String[] names = {"A", "B"}; Util.printArray(names);
    // Integer[] nums = {1, 2}; Util.<Integer>printArray(nums); // Type witness (optional)
    ```
5.  **Type Erasure:** How generics are implemented in Java. The compiler uses the generic type information for type checking, but then *erases* it, replacing type parameters with their bounds (or `Object` if unbounded) in the generated bytecode. This ensures backward compatibility with older non-generic code but has consequences.
    -   `Box<String>` becomes `class Box { private Object item; ... }` in bytecode.
    -   `Box<T extends Number>` becomes `class Box { private Number item; ... }`.
    -   Casts are automatically inserted by the compiler where needed (e.g., in `get()`).

6.  **Bounded Type Parameters:** Restrict the types that can be used as arguments for a type parameter.
    *   **Upper Bound:** ` <T extends SuperType>` - `T` must be `SuperType` or a subclass of `SuperType`. Can extend *one* class but *multiple* interfaces (`<T extends ClassA & IfaceB & IfaceC>`).
        ```java
        public class NumberBox<T extends Number> { // Only Number or its subclasses (Integer, Double, etc.)
            private T num;
            public double doubleValue() { return num.doubleValue(); } // Can call Number methods
        }
        // NumberBox<String> box; // Compile Error! String doesn't extend Number.
        ```
    *   **Lower Bound:** Used only with wildcards (see below).

7.  **Wildcards (`?`):** Represent an unknown type. Used primarily to increase API flexibility when dealing with generic types as parameters or variables.
    *   **Unbounded Wildcard:** `<?>` - Represents any unknown type. Useful when the specific type doesn't matter (e.g., `printList(List<?> list)` if you only call methods like `size()` or `clear()` that don't depend on the element type). You can't safely *add* elements (except `null`) to a `List<?>`.
    *   **Upper-Bounded Wildcard:** `<? extends Type>` - Represents an unknown type that is `Type` or a subclass of `Type`. Use when you need to *read* (get) elements from a structure (Producer). You can safely read elements as `Type`, but you cannot safely *add* elements (except `null`).
        ```java
        // Can process lists of Number, Integer, Double, etc.
        public static double sumList(List<? extends Number> list) {
            double sum = 0.0;
            for (Number n : list) { // Safe to read as Number
                sum += n.doubleValue();
            }
            // list.add(Integer.valueOf(1)); // Compile Error! Don't know the exact type.
            return sum;
        }
        ```
    *   **Lower-Bounded Wildcard:** `<? super Type>` - Represents an unknown type that is `Type` or a superclass of `Type`. Use when you need to *write* (add) elements of type `Type` (or subtypes) to a structure (Consumer). You can safely add `Type` instances (or subtypes), but reading elements only guarantees they are `Object`.
        ```java
        // Can add Integers to lists of Integer, Number, Object, etc.
        public static void addIntegers(List<? super Integer> list, int count) {
            for (int i = 1; i <= count; i++) {
                list.add(Integer.valueOf(i)); // Safe to add Integer
            }
            // Object obj = list.get(0); // Reading only guarantees Object
        }
        ```
    *   **PECS Principle:** "Producer Extends, Consumer Super". A mnemonic for choosing bounds:
        -   If the generic structure is a **Producer** (you only *read* from it), use `<? extends T>`.
        -   If the generic structure is a **Consumer** (you only *write* to it), use `<? super T>`.
        -   If it's both, don't use a wildcard for that parameter (use the exact type `T`).

**Importance:**
-   **Type Safety:** Catches incompatible type errors at compile time, preventing `ClassCastException`s at runtime.
-   **Code Reusability:** Write algorithms and data structures once and use them with various types.
-   **Readability:** Eliminates the need for explicit casts, making code cleaner.

**Common Pitfalls / Areas Prone to Mistakes:**

1.  **Type Erasure Consequences:**
    *   **Cannot Instantiate Generic Types:** `new T()` is illegal because `T` is erased. You need workarounds like passing a `Class<T>` object or using supplier functions.
    *   **Cannot Create Generic Arrays:** `T[] array = new T[10];` is illegal due to erasure. The runtime wouldn't know what type of array to actually create. Common workarounds involve creating `Object[]` and casting, or using `Array.newInstance(clazz, size)`.
    *   **Cannot Use Primitives:** Type arguments must be reference types (e.g., `Integer`, `Double`), not primitives (`int`, `double`). Autoboxing helps but be aware of potential performance overhead or `NullPointerException`s with wrappers.
    *   **Static Context:** Cannot use a class's type parameter (`T`) in static fields or static methods (unless it's a generic static method declaring its *own* type parameter). Static members belong to the class, not instances, and erasure means there's only one class definition.
    *   **Overloading:** Cannot have two methods that only differ by their generic type parameter after erasure (e.g., `void process(List<String> list)` and `void process(List<Integer> list)` become `void process(List list)` after erasure, causing a compile error).

2.  **Understanding Wildcards and Bounds:** Choosing the wrong wildcard (`extends` vs. `super` vs. `?`) or bound restricts API usage unnecessarily or causes compile errors when trying to read/write elements. PECS is key here. Misunderstanding leads to errors like trying to add to an `<? extends T>` list or read a specific type from a `<? super T>` list.
3.  **Raw Types:** Using a generic class without specifying a type argument (e.g., `Box box = new Box();`). This opts out of generic type checking, essentially reverting to pre-generic behavior. **Avoid raw types.** They exist mainly for backward compatibility and suppress valuable compiler warnings.
4.  **Variance:** Java generics are *invariant* by default. This means `List<String>` is *not* considered a subtype of `List<Object>`, even though `String` is a subtype of `Object`. Wildcards (`<? extends ...>`, `<? super ...>`) are used to introduce *covariance* and *contravariance* where needed for API flexibility. Forgetting this leads to compile errors when trying to assign, e.g., a `List<Integer>` to a `List<Number>` variable (use `List<? extends Number>` instead).
5.  **Mixing Generics and Arrays:** Creating arrays of parameterized types (like `List<String>[]`) is generally discouraged and can lead to heap pollution warnings due to the conflict between array covariance and generic invariance. Prefer using generic collections like `List<List<String>>`.

