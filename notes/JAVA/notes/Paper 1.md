Okay, Instructor, here is a new, unique 15-question Java assessment paper following the requested format and requirements, complete with explanations for each question.

---

**Sample Paper - Internal Assessment III**

**Test Summary**
*   No. of Sections: 1
*   Total Questions: 15
*   Total Duration: 40 mins

**Section 1 - Core Java Concepts**

**Section Summary**
*   No. of Questions: 15
*   Duration: 40 mins

---

**Q1)** Fill in the blank in the `main` method to correctly print the *second* command-line argument passed to the program (assuming at least two arguments are provided).

```java
public class CommandLineArgs {
    public static void main(String[] args) {
        String secondArg = "";
        if (args.length >= 2) {
            // Blank 1: Access the correct element for the second argument
            secondArg = args[1];
        } else {
            secondArg = "Not enough arguments";
        }
        System.out.println("Second argument: " + secondArg);
    }
}
// How to compile and run to test:
// javac CommandLineArgs.java
// java CommandLineArgs First Second Third
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Accessing command-line arguments (Unit I).
*   **Logic:** Command-line arguments are passed into the `main` method as a `String` array named `args`. Array indices are 0-based, so the first argument is `args[0]`, the second is `args[1]`, and so on. The `if` statement ensures we don't try to access an index that doesn't exist, preventing an `ArrayIndexOutOfBoundsException`.
*   **Answer:** `args[1]`

---

**Q2)** What is the output of this program which demonstrates operator precedence and side effects?

```java
public class PrecedenceTest {
    public static void main(String[] args) {
        int a = 5;
        int b = 10;
        int c = ++a * b--; // Pre-increment 'a', use 'b' then post-decrement 'b'

        // Values after calculation: a=6, b=9
        // Calculation: c = 6 * 10; (b is decremented AFTER its value is used)

        System.out.println("a=" + a + ", b=" + b + ", c=" + c);
    }
}
```
**Options**
1) a=6, b=9, c=50
2) a=6, b=9, c=60
3) a=5, b=9, c=50
4) a=6, b=10, c=60

**Explanation:**
*   **Concept:** Operator precedence and pre/post-increment/decrement operators (Unit I).
*   **Logic:**
    *   `++a` (pre-increment): `a` becomes 6 *before* its value is used in the multiplication.
    *   `b--` (post-decrement): The *current* value of `b` (10) is used in the multiplication. After the expression is evaluated, `b` becomes 9.
    *   Multiplication (`*`) has higher precedence than assignment (`=`).
    *   The calculation performed is `c = 6 * 10`, so `c` becomes 60.
    *   The final values printed are the updated `a` (6), the updated `b` (9), and the calculated `c` (60).
*   **Correct Answer:** **2) a=6, b=9, c=60**

---

**Q3)** Which of the following correctly demonstrates initializing a two-dimensional array where the second row has a different number of columns than the first?

```java
// Goal: Create a jagged array int[][] data = { {1, 2}, {3, 4, 5} };
```
**Options**
1) `int[][] data = new int[][2]{ {1, 2}, {3, 4, 5} };`
2) `int[][] data = new int[2][*]; data[0] = {1, 2}; data[1] = {3, 4, 5};`
3) `int[][] data = {{1, 2}, {3, 4, 5}};`
4) `int data[][] = new int[2][]; data[0] = new int(2); data[1] = new int(3);`

**Explanation:**
*   **Concept:** Multi-dimensional array initialization, specifically "jagged" arrays (Unit II).
*   **Logic:**
    *   Option 1: Syntax `new int[][2]` is invalid for specifying varying column sizes during initialization.
    *   Option 2: `[*]` is not valid Java syntax for array dimensions. Literal array initializers `{...}` cannot be used in assignment after declaration without `new type[]{...}`.
    *   Option 3: This is the direct array literal syntax for initializing a 2D array with specific values, automatically creating rows of the required lengths. This is the standard way to initialize jagged arrays with known values.
    *   Option 4: Uses invalid constructor syntax `new int(2)`. Array initialization requires square brackets `new int[2]`.
*   **Correct Answer:** **3) `int[][] data = {{1, 2}, {3, 4, 5}};`**

---

**Q4)** Predict the output of the following code, considering static and instance initializer blocks.

```java
public class InitializerOrder {

    { System.out.print("I1 "); } // Instance Initializer 1

    static { System.out.print("S1 "); } // Static Initializer 1

    InitializerOrder() {
        System.out.print("C "); // Constructor
    }

    { System.out.print("I2 "); } // Instance Initializer 2

    static { System.out.print("S2 "); } // Static Initializer 2

    public static void main(String[] args) {
        System.out.print("Main ");
        new InitializerOrder();
        new InitializerOrder();
    }
}
```
**Options**
1) Main S1 S2 I1 I2 C I1 I2 C
2) S1 S2 Main I1 I2 C I1 I2 C
3) Main S1 I1 S2 I2 C S1 I1 S2 I2 C
4) S1 S2 I1 I2 C Main I1 I2 C

**Explanation:**
*   **Concept:** Execution order of static initializers, instance initializers, and constructors (Unit II).
*   **Logic:**
    1.  **Static Initializers:** Run *once* when the class is first loaded, in the order they appear. (`S1 S2`)
    2.  **`main` Method Starts:** The `main` method begins execution. (`Main `)
    3.  **First Object Creation (`new InitializerOrder()`):**
        *   Instance initializers run in the order they appear. (`I1 I2 `)
        *   The constructor body runs. (`C `)
    4.  **Second Object Creation (`new InitializerOrder()`):**
        *   Static initializers *do not* run again.
        *   Instance initializers run again in order. (`I1 I2 `)
        *   The constructor body runs again. (`C `)
*   **Combined Output:** `S1 S2 Main I1 I2 C I1 I2 C`
*   **Correct Answer:** **2) S1 S2 Main I1 I2 C I1 I2 C**

---

**Q5)** A `Book` class needs to prevent its `isbn` (International Standard Book Number) from being changed after a `Book` object is created. Which modifier should be applied to the `isbn` field declaration?

```java
class Book {
    // Which modifier makes isbn effectively constant after object creation?
    // ??? String isbn;
    String title;

    public Book(String isbn, String title) {
        this.isbn = isbn; // Initialized in constructor
        this.title = title;
    }

    public String getIsbn() { return isbn; }
    public String getTitle() { return title; }
    // No setIsbn() method intentionally
}
```
**Options**
1) static
2) transient
3) final
4) protected

**Explanation:**
*   **Concept:** Using the `final` keyword to create constants or prevent reassignment (Unit III).
*   **Logic:**
    *   `static` makes the field belong to the class, not the instance. Doesn't prevent changes.
    *   `transient` excludes the field from serialization. Doesn't prevent changes.
    *   `final` indicates that the variable can only be assigned a value *once*, either at declaration or within the constructor. After the constructor completes, a `final` instance variable cannot be reassigned.
    *   `protected` relates to access control (inheritance/package), not immutability.
*   **Correct Answer:** **3) final** (Making `isbn` final ensures it's set once in the constructor and cannot be modified thereafter).

---

**Q6)** Given the interface `Logger`, which lambda expression correctly implements it to print a message to the console prepended with "LOG: "?

```java
@FunctionalInterface
interface Logger {
    void logMessage(String message);
}

public class LambdaLog {
    public static void main(String[] args) {
        // How to create a Logger instance using a lambda?
        Logger myLogger = /* ??? Lambda Expression Here ??? */;

        myLogger.logMessage("System startup."); // Expected output: LOG: System startup.
    }
}

```
**Options**
1) `() -> System.out.println("LOG: ");`
2) `message -> System.out.println("LOG: " + message);`
3) `(String message) -> return "LOG: " + message;`
4) `(message) => System.out.println("LOG: " + message);`

**Explanation:**
*   **Concept:** Lambda expression syntax for implementing functional interfaces (Unit IV).
*   **Logic:**
    *   The `logMessage` method takes one `String` parameter (`message`) and returns `void`.
    *   Option 1: Takes no parameters, ignores the input message. Incorrect.
    *   Option 2: Correctly takes one parameter (`message`, type inferred), and its body uses `System.out.println` (void return) to print the desired output. Parentheses around `message` are optional here but shown for clarity.
    *   Option 3: Incorrectly uses `return` (method is `void`), and missing curly braces for a statement requiring `return`.
    *   Option 4: Uses `=>` which is not the Java lambda arrow token (`->`).
*   **Correct Answer:** **2) `message -> System.out.println("LOG: " + message);`**

---

**Q7)** What change is required to make the following code using `try-with-resources` compile and run correctly?

```java
import java.io.BufferedReader; // Incorrect import for FileReader
import java.io.IOException;
import java.io.InputStreamReader; // Needed for encoding
import java.io.FileInputStream; // Needed for file access
import java.nio.charset.StandardCharsets; // For explicit encoding

public class ReadWithEncoding {
    public static void main(String[] args) {
        String path = "data.txt"; // Assume file exists
        try (BufferedReader reader = new BufferedReader(
                 // Issue: Using FileReader ignores explicit encoding control
                 new FileReader(path) // Should use InputStreamReader here
             ))
        {
            System.out.println(reader.readLine());
        } catch (IOException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
}
```
**Options**
1) Replace `BufferedReader` with `FileInputStream`.
2) Remove the `try-with-resources` and use a `finally` block to close the `FileReader`.
3) Replace `new FileReader(path)` with `new InputStreamReader(new FileInputStream(path), StandardCharsets.UTF_8)`.
4) Change `catch (IOException e)` to `catch (Exception e)`.

**Explanation:**
*   **Concept:** Using `try-with-resources` with character streams and specifying character encoding (Unit V, Unit IV).
*   **Logic:** The goal of using `InputStreamReader` often accompanies `BufferedReader` when reading files to *explicitly* control the character encoding (like UTF-8), preventing platform-dependent issues. `FileReader` uses the default system encoding. Option 3 correctly wraps a `FileInputStream` (byte stream) inside an `InputStreamReader` (byte-to-char bridge with specified encoding) which is then wrapped by `BufferedReader` (for efficient reading).
*   **Correct Answer:** **3) Replace `new FileReader(path)` with `new InputStreamReader(new FileInputStream(path), StandardCharsets.UTF_8)`**.

---

**Q8)** Arrange the following code snippets to define a custom *checked* exception `DataValidationException` and throw it from a method.

```java
// Code Lines (Arrange these)
1. } // End of Exception class
2. if (input == null || input.isEmpty()) {
3. } // End of processInput method
4. class DataValidationException extends Exception { // Define checked exception
5. public void processInput(String input) throws DataValidationException { // Method declares throws
6. throw new DataValidationException("Input cannot be empty.");
7. public DataValidationException(String message) { super(message); } // Constructor
8. } // End of if block
```
**Options**
1) 4, 7, 1, 5, 2, 6, 8, 3
2) 5, 2, 6, 8, 3, 4, 7, 1
3) 4, 1, 7, 5, 2, 6, 8, 3
4) 5, 3, 4, 7, 1, 2, 6, 8

**Explanation:**
*   **Concept:** Defining and throwing custom checked exceptions (Unit IV).
*   **Logic:**
    1.  Define the exception class (`class DataValidationException extends Exception { ... }`). This requires the class declaration (4), constructor (7), and closing brace (1).
    2.  Define the method that throws the exception. This requires the method signature declaring `throws` (5), the condition check (2), throwing the exception instance (6), the closing brace for the `if` (8), and the closing brace for the method (3).
*   **Correct Order:** (4, 7, 1) define the class, then (5, 2, 6, 8, 3) define the method using it.
*   **Correct Answer:** **1) 4, 7, 1, 5, 2, 6, 8, 3**

---

**Q9)** Which statement correctly uses the `transient` keyword in the context of Java serialization?

**Options**
1) `transient class SecureData { ... }` (Marks the entire class as non-serializable)
2) `public transient void process() { ... }` (Applied to a method)
3) `class User { private transient String password; ... }` (Applied to an instance field)
4) `public void login(transient User u) { ... }` (Applied to a method parameter)

**Explanation:**
*   **Concept:** The `transient` keyword and its usage in object serialization (Unit V).
*   **Logic:** The `transient` keyword is a modifier specifically for **instance variables**. It signals the serialization mechanism to ignore that field when writing the object's state to a stream. It cannot be applied to classes, methods, or parameters in this context. Option 3 correctly shows its use on the `password` field to prevent it from being serialized.
*   **Correct Answer:** **3) `class User { private transient String password; ... }` (Applied to an instance field)**

---

**Q10)** Consider the following generic method. What type can `T` represent based on the method's body?

```java
import java.util.List;

public class GenericMethodBound {

    // What can T be?
    public static <T extends Comparable<T>> T findMax(List<T> list) {
        if (list == null || list.isEmpty()) {
            return null;
        }
        T max = list.get(0);
        for (int i = 1; i < list.size(); i++) {
            // Calls compareTo method
            if (list.get(i).compareTo(max) > 0) {
                max = list.get(i);
            }
        }
        return max;
    }

    public static void main(String[] args) {
        List<String> names = List.of("Eve", "Adam", "Charlie");
        System.out.println(findMax(names)); // Works: String implements Comparable<String>

        List<Integer> numbers = List.of(10, 30, 20);
        System.out.println(findMax(numbers)); // Works: Integer implements Comparable<Integer>

        // List<Object> objects = List.of(new Object());
        // System.out.println(findMax(objects)); // Compile error if uncommented
    }
}

```
**Options**
1) Any class (`Object`)
2) Only `Number` or its subclasses
3) Any class that implements the `Comparable<T>` interface
4) Only primitive types

**Explanation:**
*   **Concept:** Bounded type parameters in generic methods (Unit V).
*   **Logic:** The method signature is `<T extends Comparable<T>>`. This constrains the type `T` to be only those types that implement the `Comparable` interface for their own type. This is necessary because the method body calls the `compareTo` method, which is defined in the `Comparable` interface. `String` and `Integer` implement `Comparable`, but `Object` does not. Primitive types cannot be used as generic type arguments directly.
*   **Correct Answer:** **3) Any class that implements the `Comparable<T>` interface**

---

**Q11)** Which keyword is used by a subclass constructor to explicitly call a specific constructor of its immediate superclass?

**Options**
1) this
2) new
3) instanceof
4) super

**Explanation:**
*   **Concept:** Calling superclass constructors from subclass constructors (Unit III).
*   **Logic:**
    *   `this()` is used to call another constructor within the *same* class.
    *   `new` is used to create new objects.
    *   `instanceof` is an operator to check an object's type.
    *   `super(...)` (with appropriate arguments) is used as the first statement in a subclass constructor to explicitly invoke a specific constructor of the immediate superclass. If omitted, `super()` (the no-arg superclass constructor) is called implicitly if available.
*   **Correct Answer:** **4) super**

---

**Q12)** Fill in the blanks to correctly implement the `Displayable` interface using an anonymous inner class.

```java
interface Displayable {
    void display();
}

public class AnonInnerDemo {
    public static void main(String[] args) {

        // Blank 1: Start the anonymous class declaration implementing Displayable
        Displayable myDisplay = new Displayable() {
            // Blank 2: Provide the implementation for the 'display' method
            @Override
            public void display() {
                System.out.println("Display from Anonymous Class");
            }
        // Blank 3: Close the anonymous class body and statement
        }; // Semicolon needed after class body/instantiation

        myDisplay.display();
    }
}
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Anonymous Inner Classes (Unit IV).
*   **Logic:** Anonymous classes are defined and instantiated in a single expression using `new InterfaceName() { ... class body ... };` or `new SuperClassName() { ... class body ... };`. Inside the braces, you must implement any abstract methods from the interface or override methods from the superclass. The expression requires a semicolon at the end.
*   **Answer:**
    *   Blank 1: `new Displayable() {`
    *   Blank 2: `@Override public void display() { System.out.println("Display from Anonymous Class"); }`
    *   Blank 3: `};`

---

**Q13)** What is the output of calling `execute()` on the `action` object?

```java
abstract class Action {
    abstract void perform(); // Abstract method

    void execute() { // Concrete method
        System.out.print("Prepare... ");
        perform(); // Calls the abstract method's implementation
    }
}

class ConcreteAction extends Action {
    @Override
    void perform() { // Provides implementation
        System.out.print("Performing! ");
    }
}

public class AbstractExecute {
    public static void main(String[] args) {
        Action action = new ConcreteAction();
        action.execute();
        System.out.print("Done.");
    }
}
```
**Options**
1) Performing! Done.
2) Prepare... Performing! Done.
3) Prepare... Done.
4) Compilation Error

**Explanation:**
*   **Concept:** Interaction between concrete and abstract methods in an abstract class hierarchy (Unit III).
*   **Logic:**
    1.  `action.execute()` is called. `action` refers to a `ConcreteAction` object, but `execute()` is defined in the `Action` class (and not overridden).
    2.  The `execute()` method in `Action` runs. It first prints "Prepare... ".
    3.  It then calls `perform()`. Because this is a polymorphic call (`action`'s actual type is `ConcreteAction`), the overridden `perform()` method in `ConcreteAction` is executed, printing "Performing! ".
    4.  The `execute()` method finishes.
    5.  The `main` method then prints "Done.".
*   **Combined Output:** `Prepare... Performing! Done.`
*   **Correct Answer:** **2) Prepare... Performing! Done.**

---

**Q14)** Identify the potential issue with the following use of the `Assertion` feature in Java.

```java
import java.util.Scanner;

public class AssertDemo {
    // Simulates processing based on user role
    public void processUserData(String userRole) {
        // Using assertion to check critical input validity
        assert userRole != null && !userRole.equals("guest") : "Guest role cannot process data";

        // Proceed with sensitive data processing...
        System.out.println("Processing data for role: " + userRole);
    }

    public static void main(String[] args) {
         // Assume assertions might be disabled in production (-da or no flag)
        new AssertDemo().processUserData("admin");
        new AssertDemo().processUserData("guest"); // Potentially problematic
    }
}
```
**Options**
1) Assertions cannot have a detail message after the colon `:`.
2) The `assert` statement will cause a `NullPointerException` if `userRole` is null.
3) The condition `!userRole.equals("guest")` is invalid syntax.
4) If assertions are disabled (default), the check is skipped, potentially allowing "guest" to proceed with sensitive processing.

**Explanation:**
*   **Concept:** Proper usage and limitations of assertions (`assert`) (Unit IV).
*   **Logic:** Assertions are primarily for verifying internal logic and assumptions during development/testing. They are disabled by default at runtime and **must not** be used for enforcing business rules or validating input/conditions critical to the application's correct or secure functioning in production. If assertions are disabled, the `assert` statement is simply skipped. In this case, if the `processUserData("guest")` call happens in production where assertions are disabled, the check `!userRole.equals("guest")` will not execute, and the code might proceed incorrectly to process data for a guest role.
*   **Correct Answer:** **4) If assertions are disabled (default), the check is skipped, potentially allowing "guest" to proceed with sensitive processing.**

---

**Q15)** Fill in the blanks to complete the `switch` statement using String cases (Java 7+) to identify the protocol.

```java
public class StringSwitch {
    public static void main(String[] args) {
        String url = "https://example.com";
        String protocol = "unknown";

        int protocolEndIndex = url.indexOf("://");

        if (protocolEndIndex != -1) {
            // Blank 1: Extract the protocol part (e.g., "https")
            String scheme = url.substring(0, protocolEndIndex);

            // Blank 2: Use the extracted scheme in the switch
            switch (scheme) {
                // Blank 3: Define cases for "http" and "https"
                case "http":
                    protocol = "Hypertext Transfer Protocol";
                    break; // Don't forget break!
                case "https":
                    protocol = "Hypertext Transfer Protocol Secure";
                    break;
                case "ftp":
                    protocol = "File Transfer Protocol";
                    break;
                // Default case not strictly needed here as protocol initialized
            }
        }
        System.out.println("Protocol: " + protocol); // Should be Secure for the example url
    }
}
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Using `String` objects in `switch` statements (available since Java 7) (Unit I).
*   **Logic:**
    1.  We first extract the part of the URL before `://` using `substring`.
    2.  This extracted `scheme` string is used as the expression in the `switch` statement.
    3.  `case` labels use string literals (`"http"`, `"https"` etc.) to match against the `scheme`. Remember to use `break` to prevent fall-through.
*   **Answer:**
    *   Blank 1: `String scheme = url.substring(0, protocolEndIndex);`
    *   Blank 2: `switch (scheme)`
    *   Blank 3: `case "http": protocol = "Hypertext Transfer Protocol"; break; case "https": protocol = "Hypertext Transfer Protocol Secure"; break;` (and optionally `case "ftp": ... break;`)

---
