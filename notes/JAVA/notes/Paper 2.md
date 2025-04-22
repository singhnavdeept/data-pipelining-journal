Alright, Instructor, let's ramp up the complexity slightly for this assessment, digging into more nuanced applications of the syllabus concepts.

---

**Sample Paper - Internal Assessment IV (Advanced)**

**Test Summary**
*   No. of Sections: 1
*   Total Questions: 15
*   Total Duration: 40 mins

**Section 1 - Core Java Concepts (Advanced Application)**

**Section Summary**
*   No. of Questions: 15
*   Duration: 40 mins

---

**Q1)** What is the output of the following code involving bitwise shifts and integer limits?

```java
public class ShiftEdgeCase {
    public static void main(String[] args) {
        int value = -1; // All bits are 1 in two's complement
        // Right shift with sign extension (>>) vs unsigned right shift (>>>)
        int signedShift = value >> 16;   // Fills with sign bit (1)
        int unsignedShift = value >>> 16; // Fills with zero bit (0)

        // -1 = 0xFFFFFFFF (32 ones)
        // signedShift   -> 0xFFFFFFFF (still -1)
        // unsignedShift -> 0x0000FFFF (positive 65535)

        System.out.println(signedShift + ", " + unsignedShift);
    }
}
```
**Options**
1) 0, 65535
2) -1, 65535
3) -1, -1
4) 0, 0

**Explanation:**
*   **Concept:** Bitwise shift operators (`>>` vs `>>>`), two's complement representation of negative numbers (Unit I).
*   **Logic:** `int value = -1;` means all 32 bits are set to 1.
    *   `>> 16` (signed right shift): Shifts bits right by 16 positions. Since the number is negative (sign bit is 1), the vacated bits on the left are filled with the sign bit (1). The result remains `0xFFFFFFFF`, which is -1.
    *   `>>> 16` (unsigned right shift): Shifts bits right by 16 positions. The vacated bits on the left are *always* filled with 0, regardless of the sign. The result becomes `0x0000FFFF`, which is the positive integer 65535.
*   **Correct Answer:** **2) -1, 65535**

---

**Q2)** The following code attempts to count negative numbers in each row of a 2D array. Identify the correction needed for the marked issue.

```java
public class CountNegatives {
    static int countRowNegatives(int[] row) {
        int count = 0;
        for (int val : row) {
            if (val < 0) {
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        int[][] data = {{1, -2, 3}, {-4, -5}, {6, 7, -8, -9}};
        int totalNegatives = 0;

        for (int i = 0; i <= data.length; i++) { // Issue: Loop boundary
             // Should only process existing rows: data[0], data[1], data[2]
             if (i < data.length) { // Redundant check if loop is correct
                 totalNegatives += countRowNegatives(data[i]);
             }
        }
        // Expected totalNegatives = 1 (row 0) + 2 (row 1) + 2 (row 2) = 5
        System.out.println("Total Negatives: " + totalNegatives);
    }
}
```
**Options**
1) Change `int[][] data` to `int[] data`.
2) Replace `i <= data.length` with `i < data.length`.
3) Replace `totalNegatives += countRowNegatives(data[i]);` with `totalNegatives = countRowNegatives(data[i]);`.
4) Change `if (val < 0)` to `if (val <= 0)`.

**Explanation:**
*   **Concept:** Array indexing and loop boundaries, `ArrayIndexOutOfBoundsException` (Unit II).
*   **Logic:** Arrays are 0-indexed. A 2D array `data` with `data.length` rows has valid row indices from `0` to `data.length - 1`. The loop `for (int i = 0; i <= data.length; i++)` attempts to access `data[data.length]`, which is out of bounds and will cause an `ArrayIndexOutOfBoundsException`. The condition should be `i < data.length` to iterate only through valid indices.
*   **Correct Answer:** **2) Replace `i <= data.length` with `i < data.length`.**

---

**Q3)** What output is produced by the following code that uses overloaded constructors and the `this` keyword?

```java
class Widget {
    String id = "Default";
    int version = 0;

    Widget(String id) {
        this.id = id;
        System.out.print("ID:" + this.id + " ");
    }

    Widget(int version) {
        this(); // Calls no-arg constructor first
        this.version = version;
        System.out.print("Ver:" + this.version + " ");
    }

    Widget() {
        // No explicit this() or super(), so super() is implicit
        System.out.print("Base:" + this.id + "/" + this.version + " "); // Uses initial default values
    }

    public static void main(String[] args) {
        Widget w = new Widget(5); // Starts chain from Widget(int)
    }
}
```
**Options:**
1) ID:Default Ver:5
2) Base:Default/0 Ver:5
3) Base:Default/5 Ver:5
4) ID:Default Base:Default/0 Ver:5

**Explanation:**
*   **Concept:** Constructor overloading, `this()` constructor calls, execution order (Unit II).
*   **Logic:**
    1.  `new Widget(5)` calls `Widget(int version)`.
    2.  The first line of `Widget(int version)` is `this();`, which calls the no-arg `Widget()` constructor.
    3.  The no-arg `Widget()` executes, printing `Base:Default/0 ` (using the initial field values before assignments in other constructors happen).
    4.  Control returns to `Widget(int version)`. It proceeds to assign `this.version = 5`.
    5.  It then prints `Ver:5 `.
*   **Combined Output:** `Base:Default/0 Ver:5 `
*   **Correct Answer:** **2) Base:Default/0 Ver:5**

---

**Q4)** A `Session` object contains a sensitive `sessionToken`. To prevent this token from being written during serialization, the `sessionToken` field is marked `transient`. How should the `userId` (which is *not* transient) be retrieved after deserializing the object `session.ser`? Fill in the blank.

```java
import java.io.*;

class Session implements Serializable {
    private static final long serialVersionUID = 1L; // Assume version matches
    String userId;
    transient String sessionToken; // Not saved during serialization

    Session(String id, String token) { this.userId = id; this.sessionToken = token; }

    @Override public String toString() { return "ID:" + userId + ", Token:" + sessionToken; }
}

public class DeserializeSession {
    public static void main(String[] args) {
        // Assume session.ser contains a serialized Session object with userId="User123"
        // but the sessionToken field was skipped due to 'transient'
        Session s = null;
        try (FileInputStream fis = new FileInputStream("session.ser");
             ObjectInputStream ois = new ObjectInputStream(fis))
        {
            // Blank: Read the object and cast it
            s = (Session) ois.readObject();

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return;
        }

        System.out.println("User ID: " + s.userId); // Should work
        // The token would be null after deserialization:
        // System.out.println(s.toString()); // Output: ID:User123, Token:null
    }
}
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Deserialization using `ObjectInputStream`, casting, effect of `transient` (Unit V).
*   **Logic:** `ObjectInputStream.readObject()` reads the serialized data and reconstructs the object. It returns an `Object` reference, which needs to be cast to the specific type (`Session`) to access its fields. The `transient` field (`sessionToken`) is not restored and will have its default value (`null` for objects), but non-transient fields like `userId` are restored.
*   **Answer:** `s = (Session) ois.readObject();`

---

**Q5)** Which `println` statement will execute in the following hierarchy involving hidden static methods and overridden instance methods?

```java
class Root {
    static void staticMethod() { System.out.println("Root Static"); }
    void instanceMethod() { System.out.println("Root Instance"); }
}

class Node extends Root {
    // Hides Root.staticMethod()
    static void staticMethod() { System.out.println("Node Static"); }
    // Overrides Root.instanceMethod()
    @Override
    void instanceMethod() { System.out.println("Node Instance"); }
}

public class HidingVsOverriding {
    public static void main(String[] args) {
        Root r = new Node();
        r.staticMethod();  // Call determined by reference type (Root)
        r.instanceMethod(); // Call determined by object type (Node)
    }
}
```
**Options**
1) Root Static \n Root Instance
2) Node Static \n Node Instance
3) Root Static \n Node Instance
4) Node Static \n Root Instance

**Explanation:**
*   **Concept:** Difference between static method hiding and instance method overriding, polymorphism (Unit III).
*   **Logic:**
    *   **Static Methods:** Static method calls are resolved at *compile time* based on the *reference type*. `r` is a `Root` reference, so `r.staticMethod()` calls the method defined in the `Root` class, regardless of the object (`Node`) it points to. Output: `Root Static`.
    *   **Instance Methods:** Instance method calls are resolved at *runtime* based on the *actual object type* (polymorphism). `r` points to a `Node` object, and `Node` overrides `instanceMethod`. Therefore, `r.instanceMethod()` calls the method defined in the `Node` class. Output: `Node Instance`.
*   **Correct Answer:** **3) Root Static \n Node Instance**

---

**Q6)** What is the output of this code involving a non-static inner class accessing potentially shadowed variables?

```java
public class OuterAccess {
    private int value = 10;

    class Inner {
        private int value = 20; // Shadows Outer's value

        void printValues(int value) { // Parameter 'value' shadows inner's value
            System.out.print(value + ", ");         // Accesses parameter
            System.out.print(this.value + ", ");    // Accesses Inner's instance variable
            System.out.print(OuterAccess.this.value); // Accesses Outer's instance variable
        }
    }

    public static void main(String[] args) {
        OuterAccess outer = new OuterAccess();
        OuterAccess.Inner inner = outer.new Inner();
        inner.printValues(30);
    }
}
```
**Options**
1) 30, 20, 10
2) 10, 20, 30
3) 30, 30, 30
4) 20, 20, 10

**Explanation:**
*   **Concept:** Non-static (inner) classes, `this` keyword, accessing shadowed outer class members using `OuterClassName.this` (Unit IV).
*   **Logic:** Inside `printValues(int value)`:
    *   `value`: Refers to the method parameter, which is 30.
    *   `this.value`: Refers to the instance variable of the `Inner` class instance (`this` refers to the `Inner` object), which is 20.
    *   `OuterAccess.this.value`: Explicitly refers to the instance variable of the enclosing `OuterAccess` object instance, which is 10.
*   **Correct Answer:** **1) 30, 20, 10**

---

**Q7)** Complete the `main` method to filter a list of strings, keeping only those longer than 3 characters, convert them to uppercase, and join them with commas.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamChain {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("a", "bee", "cat", "deer", "eagle");

        // Blank 1: Start the stream pipeline on 'words'
        String result = words.stream()
                             // Blank 2: Filter words based on length > 3
                             .filter(s -> s.length() > 3)
                             // Blank 3: Map remaining words to uppercase
                             .map(String::toUpperCase) // Method reference for s -> s.toUpperCase()
                             // Blank 4: Collect the results into a single comma-separated String
                             .collect(Collectors.joining(","));

        System.out.println(result); // Expected Output: DEER,EAGLE
    }
}
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Java Streams API - intermediate operations (`filter`, `map`) and terminal operation (`collect`) (Unit IV - relies on Lambdas).
*   **Logic:**
    1.  `.stream()` creates a stream from the `List`.
    2.  `.filter(s -> s.length() > 3)` keeps only elements ("deer", "eagle") whose length satisfies the condition.
    3.  `.map(String::toUpperCase)` transforms each remaining element to its uppercase version ("DEER", "EAGLE").
    4.  `.collect(Collectors.joining(","))` gathers the elements from the resulting stream and concatenates them into a single String, separated by commas.
*   **Answer:**
    *   Blank 1: `words.stream()`
    *   Blank 2: `.filter(s -> s.length() > 3)`
    *   Blank 3: `.map(String::toUpperCase)` (or `.map(s -> s.toUpperCase())`)
    *   Blank 4: `.collect(Collectors.joining(","))`

---

**Q8)** If `loadConfig()` throws an `IOException` and `processConfig()` subsequently throws a `ConfigException` within the same `try` block, which exception's details will *primarily* be available to the caller of `processData` if it only declares `throws Exception`?

```java
import java.io.IOException;

class ConfigException extends Exception { // Custom exception
    ConfigException(String msg, Throwable cause) { super(msg, cause); }
}

public class ExceptionCause {

    String loadConfig() throws IOException {
        // Simulates failure
        throw new IOException("Failed to read config file");
    }

    void processConfig(String configData) throws ConfigException {
        // Simulates failure during processing
        throw new ConfigException("Invalid config format", null); // Cause not set here
    }

    // Method potentially throwing multiple exceptions sequentially
    public void processData() throws Exception { // Catches specific, throws generic
        String config = null;
        try {
            config = loadConfig();        // Step 1: Might throw IOException
            processConfig(config);    // Step 2: Might throw ConfigException
        } catch (IOException e) {
            // Wrap the original IOException in a new generic Exception
            throw new Exception("Setup failed", e); // Chaining: IOException is the cause
        } catch (ConfigException ce) {
            // Wrap ConfigException (but maybe we lost the IO cause)
            throw new Exception("Processing failed", ce); // Chaining: ConfigException is the cause
        }
    }

     public static void main(String[] args) {
         try {
             new ExceptionCause().processData();
         } catch (Exception finalException) {
             System.out.println("Caught: " + finalException.getMessage());
             // How to see the original exception if processData succeeded step 1 but failed step 2?
             if (finalException.getCause() != null) {
                  System.out.println("Original Cause: " + finalException.getCause().getClass().getSimpleName());
             }
         }
     }
}
```
**Options**
1) Only the `IOException` details.
2) Only the `ConfigException` details.
3) The details of whichever exception (IOException or ConfigException) occurred *last* inside the `try` block, wrapped as the cause of the `Exception` thrown by the `catch` block.
4) Both exceptions combined into a single stack trace automatically.

**Explanation:**
*   **Concept:** Exception handling, exception propagation, and exception chaining (preserving the original cause) (Unit IV).
*   **Logic:** If `loadConfig` throws `IOException`, the first `catch` block executes. It catches the `IOException`, wraps it inside a *new* `Exception` (preserving the `IOException` as the `cause`), and throws this new `Exception`. `processConfig` is never called. If `loadConfig` succeeds but `processConfig` throws `ConfigException`, the second `catch` block executes. It catches the `ConfigException`, wraps *it* in a *new* `Exception` (preserving `ConfigException` as the cause), and throws this new `Exception`. In either scenario, the caller catching the final `Exception` receives an object whose `cause` is the *specific exception caught* within `processData`. The question wording is slightly ambiguous ("details available"), but the direct cause accessible via `getCause()` on the final `Exception` will be the one from the `catch` block that executed. Option 3 reflects this most accurately.
*   **Correct Answer:** **3) The details of whichever exception (IOException or ConfigException) occurred *last* inside the `try` block, wrapped as the cause of the `Exception` thrown by the `catch` block.**

---

**Q9)** Identify the single statement within `main` that will **fail** to compile due to Generic wildcard constraints.

```java
import java.util.*;

public class WildcardSuper {

    // Accepts a list that can hold Number objects or any supertype (like Object)
    // We can ADD Numbers (or subtypes like Integer) to this list
    public static void addNumbers(List<? super Number> list) {
        list.add(Integer.valueOf(10)); // OK - Integer is a Number
        list.add(Double.valueOf(20.5)); // OK - Double is a Number
        // Number n = list.get(0); // NOT OK - Only guaranteed to be Object
        Object o = list.get(0);    // OK - Safe to read as Object
        System.out.println("Added numbers to list.");
    }

    public static void main(String[] args) {
        List<Integer> integerList = new ArrayList<>(); // Integer IS NOT a supertype of Number
        List<Number> numberList = new ArrayList<>();   // Number IS Number (supertype)
        List<Object> objectList = new ArrayList<>();   // Object IS a supertype of Number
        List<Double> doubleList = new ArrayList<>(); // Double IS NOT a supertype of Number

        // Which call FAILS compilation?
        // Call 1:
        addNumbers(numberList);

        // Call 2:
        addNumbers(objectList);

        // Call 3:
        // addNumbers(integerList); // Fails

        // Call 4:
        // addNumbers(doubleList); // Fails
    }
}
```
**Options**
1) Call 1: `addNumbers(numberList);`
2) Call 2: `addNumbers(objectList);`
3) Call 3: `addNumbers(integerList);` (or Call 4: `addNumbers(doubleList);`)
4) All calls compile successfully.

**Explanation:**
*   **Concept:** Generics Lower-Bounded Wildcards (`<? super T>`), PECS (Consumer Super) (Unit V).
*   **Logic:** The method `addNumbers` requires a `List<? super Number>`. This means the list must be capable of holding `Number` objects. Therefore, the list's actual type argument must be `Number` or one of its supertypes (`Object`).
    *   `List<Number>` is valid because `Number` is `Number`.
    *   `List<Object>` is valid because `Object` is a supertype of `Number`.
    *   `List<Integer>` is **invalid** because `Integer` is a *subtype*, not a supertype, of `Number`. You cannot guarantee that a `List<Integer>` can safely hold any arbitrary `Number` (like a `Double`).
    *   `List<Double>` is **invalid** for the same reason as `List<Integer>`.
*   **Correct Answer:** **3) Call 3: `addNumbers(integerList);` (or Call 4: `addNumbers(doubleList);`)**

---

**Q10)** What is the output of the following code involving a switch statement with fall-through?

```java
public class FallThrough {
    public static void main(String[] args) {
        int code = 2;
        String result = "Status: ";

        switch (code) {
            case 1:
                result += "Open ";
            case 2: // Starts executing here
                result += "Processing "; // Executes
                // No break, fall through!
            case 3:
                result += "Reviewing "; // Executes due to fall-through
                break;
            case 4:
                result += "Closed ";
            default:
                result += "Unknown"; // Skipped because break was hit in case 3
        }
        System.out.println(result);
    }
}
```
**Options**
1) Status: Processing
2) Status: Processing Reviewing
3) Status: Processing Reviewing Closed Unknown
4) Status: Open Processing Reviewing

**Explanation:**
*   **Concept:** `switch` statement execution flow, `case`, `break`, and fall-through behavior (Unit I).
*   **Logic:**
    1.  `code` is 2, so execution jumps to `case 2:`.
    2.  `result += "Processing ";` executes. `result` is now "Status: Processing ".
    3.  There is no `break` after `case 2`. Execution *falls through* to `case 3:`.
    4.  `result += "Reviewing ";` executes. `result` is now "Status: Processing Reviewing ".
    5.  A `break;` is encountered, so execution exits the `switch` statement.
    6.  The final `result` is printed.
*   **Correct Answer:** **2) Status: Processing Reviewing**

---

**Q11)** A class `Task` needs to implement both `Runnable` (from `java.lang`) and a custom `Loggable` interface. `Loggable` has a default method `log(String)`. Which statement is true if `Task` does not explicitly override `log(String)`?

```java
interface Loggable {
    default void log(String message) {
        System.out.println("LOG: " + message);
    }
    void setup(); // Abstract method
}

// Task must implement run() from Runnable and setup() from Loggable
class Task implements Runnable, Loggable {
    @Override
    public void run() {
        setup(); // Needs to be implemented
        log("Task running"); // Can call default method
    }

    @Override
    public void setup() {
        System.out.println("Task setup complete.");
    }

    // Does NOT override log(String message)
}

public class MultipleInterfaceDemo {
    public static void main(String[] args) {
        Task t = new Task();
        t.run(); // Will this call the default log method?
    }
}
```
**Options**
1) The code will not compile because `Task` must override all methods, including defaults.
2) The code will not compile because `Runnable` and `Loggable` clash.
3) The code compiles, and calling `log()` on a `Task` object will execute the default `log()` implementation from `Loggable`.
4) The code compiles, but calling `log()` will do nothing as default methods are optional.

**Explanation:**
*   **Concept:** Implementing multiple interfaces, `default` methods in interfaces (Unit III).
*   **Logic:** A class implementing an interface must provide implementations for all *abstract* methods of that interface. Default methods provide an implementation directly in the interface. If an implementing class does *not* provide its own overriding implementation for a default method, it simply inherits the default implementation from the interface. Since `Runnable` has no `log` method, there's no conflict here. `Task` implements `run()` and `setup()`, fulfilling the abstract method requirements. It can then call `log()` and will execute the version provided in `Loggable`.
*   **Correct Answer:** **3) The code compiles, and calling `log()` on a `Task` object will execute the default `log()` implementation from `Loggable`.**

---

**Q12)** Fill in the blank to create a `DateTimeFormatter` capable of parsing the date string "15/Mar/2024".

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.util.Locale; // Needed for month names usually

public class ParseCustomDate {
    public static void main(String[] args) {
        String dateStr = "15/Mar/2024";
        LocalDate date = null;
        try {
            // Blank: Define the formatter pattern
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MMM/yyyy", Locale.ENGLISH);
            date = LocalDate.parse(dateStr, formatter);
            System.out.println("Parsed Date: " + date);
        } catch (DateTimeParseException e) {
            System.err.println("Parsing failed: " + e.getMessage());
        }
    }
}
```
*(This is a fill-in-the-blank question, no options needed)*

**Explanation:**
*   **Concept:** Using `java.time.format.DateTimeFormatter` with custom patterns, parsing date strings (Unit IV).
*   **Logic:** The pattern string must match the input string's format:
    *   `dd`: Day of the month as two digits (15).
    *   `/`: Literal slash character.
    *   `MMM`: Abbreviated month name (Mar). Using `MMM` requires specifying a `Locale` (like `Locale.ENGLISH`) so Java knows which language's abbreviations to expect.
    *   `/`: Literal slash character.
    *   `yyyy`: Year with four digits (2024).
*   **Answer:** `DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MMM/yyyy", Locale.ENGLISH);`

---

**Q13)** Arrange the following code snippets to build a `Map` where keys are characters and values are their counts, based on an input string.

```java
// Code Lines (Arrange these)
1. Map<Character, Integer> counts = new HashMap<>();
2. System.out.println(counts);
3. char c = input.charAt(i);
4. String input = "aabbcda";
5. for (int i = 0; i < input.length(); i++) {
6. counts.put(c, counts.getOrDefault(c, 0) + 1);
7. } // End of loop
```
**Options**
1) 1, 4, 5, 3, 6, 7, 2
2) 4, 1, 5, 3, 6, 7, 2
3) 1, 5, 3, 6, 7, 4, 2
4) 4, 5, 3, 1, 6, 7, 2

**Explanation:**
*   **Concept:** Using `Map`, loops, character access, `getOrDefault` (Covered broadly by Collections/Loops/String concepts from syllabus).
*   **Logic:**
    1.  Define the input string (4).
    2.  Initialize the empty map (1).
    3.  Start the loop to iterate through the string (5).
    4.  Inside the loop, get the current character (3).
    5.  Update the count in the map for that character using `getOrDefault` to handle the first occurrence gracefully (6).
    6.  Close the loop (7).
    7.  Print the resulting map (2).
*   **Correct Order:** 4, 1, 5, 3, 6, 7, 2
*   **Correct Answer:** **2) 4, 1, 5, 3, 6, 7, 2**

---

**Q14)** Fix the bug in the following code, which intends to read two different files using try-with-resources.

```java
import java.io.*;

public class MultipleResources {
    public static void main(String[] args) {
        // Assume "input.txt" and "config.cfg" exist
        try (FileInputStream fis = new FileInputStream("input.txt"); // Resource 1
             // Issue: Missing semicolon and resource separator
             BufferedReader cfgReader = new BufferedReader(new FileReader("config.cfg")) ) // Resource 2
        {
             System.out.println("Reading input byte: " + fis.read());
             System.out.println("Reading config line: " + cfgReader.readLine());

        } catch (IOException e) {
             e.printStackTrace();
        }
        System.out.println("Done.");
    }
}
```
**Options**
1) Replace `FileReader` with `FileInputStream`.
2) Remove the outer `try` block parentheses.
3) Place a semicolon `;` after the first resource declaration (`FileInputStream fis = ...;`).
4) Use two separate `try-with-resources` blocks.

**Explanation:**
*   **Concept:** Try-with-resources syntax for multiple resources (Unit IV, Unit V).
*   **Logic:** When declaring multiple resources within a single `try-with-resources` statement, each resource declaration must be separated by a semicolon `;`. The current code is missing this semicolon after the `FileInputStream` declaration. Option 4 (separate blocks) is also valid but less concise; the question asks to fix the *existing* structure.
*   **Correct Answer:** **3) Place a semicolon `;` after the first resource declaration (`FileInputStream fis = ...;`).**

---

**Q15)** What modification fixes the logical error so the `containsDigit` method correctly returns `true` if the input string contains *any* digit?

```java
public class FindDigit {
    // Intends to return true if str contains at least one digit, false otherwise
    public static boolean containsDigit(String str) {
        if (str == null || str.isEmpty()) {
            return false;
        }
        boolean found = false; // Flag to track if digit is found
        for (char c : str.toCharArray()) {
            if (Character.isDigit(c)) {
                 // Issue: Returns true immediately, doesn't check rest of string if needed
                 // Should signal that a digit WAS found and continue potentially,
                 // or simply set found = true and break.
                return true; // If the *first* char is a digit, it works. If not, it might return false prematurely.
            }
            // Incorrect logic below (if present):
            // else { return false; } // Error: Returns false if the FIRST char isn't a digit
        }
        // Need to return based on whether *any* digit was found during the loop
        return found; // Returns false currently because 'found' is never set to true
    }

    public static void main(String[] args) {
        System.out.println(containsDigit("abc1def")); // Expected: true
        System.out.println(containsDigit("abc"));    // Expected: false
    }
}
```
**Options**
1) Replace `boolean found = false;` with `boolean found = true;`.
2) Move the `return found;` statement inside the `if (Character.isDigit(c))` block.
3) Replace `return true;` inside the `if` block with `found = true; break;`.
4) Add `else { return false; }` immediately after the `if (Character.isDigit(c))` block.

**Explanation:**
*   **Concept:** Loop control flow, boolean flags, correct algorithm implementation (Unit I, Unit II).
*   **Logic:** The current code returns `true` the moment it finds the *first* digit. However, if it loops through characters that aren't digits, it finishes the loop and returns the initial value of `found`, which is `false`, even if a digit appeared later. Adding an `else { return false; }` (Option 4) is worse, returning `false` if the very first character isn't a digit. The correct approach is to set the flag `found` to `true` when a digit is encountered and then immediately `break` the loop (since we only care if *at least one* exists). The final `return found;` outside the loop will then correctly reflect whether any digit was seen during the iteration.
*   **Correct Answer:** **3) Replace `return true;` inside the `if` block with `found = true; break;`.** (Alternatively, removing the `break` and just having `found = true;` would also work, but `break` is slightly more efficient).

---