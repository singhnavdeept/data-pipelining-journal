Okay, Instructor! Based on the syllabus provided and the structure of the previous sample paper, here is a fresh, code-based Java internal assessment paper focusing on diverse topics across all units, with an emphasis on practical understanding and areas potentially less covered previously.

---

**Sample Paper - Internal Assessment II**

**Test Summary**
*   No. of Sections: 1
*   Total Questions: 15
*   Total Duration: 40 mins

**Section 1 - Core Java Concepts**

**Section Summary**
*   No. of Questions: 15
*   Duration: 40 mins

---

**Q1)** What is the output of the following code snippet?

```java
public class AutoboxingTest {
    public static void main(String[] args) {
        Integer i1 = 127;
        Integer i2 = 127;
        Integer i3 = 128;
        Integer i4 = 128;

        System.out.print(i1 == i2); // Compares objects from cache
        System.out.print(", ");
        System.out.print(i3 == i4); // Compares newly created objects
    }
}
```
**Options**
1) true, true
2) true, false
3) false, true
4) false, false

---

**Q2)** Predict the output of this code that uses an enum in a switch statement.

```java
enum Signal { GREEN, YELLOW, RED }

public class TrafficLight {
    public static void main(String[] args) {
        Signal currentSignal = Signal.YELLOW;
        String action = "";

        switch (currentSignal) {
            case RED:
                action = "Stop";
                break;
            case YELLOW:
                action = "Prepare";
                // Fall-through intentional? Assume yes for this question.
            case GREEN:
                action += "Go"; // Appends if YELLOW or GREEN
                break;
            default:
                action = "Error";
        }
        System.out.println(action);
    }
}
```
**Options**
1) Stop
2) Prepare
3) PrepareGo
4) Go

---

**Q3)** What will be printed when the following code is executed?

```java
class Box {
    String label;
    int items;

    Box() {
        this("Default Label"); // Calls Box(String)
        System.out.print("No-Arg ");
    }

    Box(String label) {
        this(label, 0); // Calls Box(String, int)
        System.out.print("One-Arg ");
    }

    Box(String label, int items) {
        this.label = label;
        this.items = items;
        System.out.print("Two-Arg ");
    }
}

public class ConstructorChain {
    public static void main(String[] args) {
        Box b = new Box();
        System.out.println("Created");
    }
}
```
**Options**
1) Two-Arg One-Arg No-Arg Created
2) No-Arg One-Arg Two-Arg Created
3) Two-Arg Created
4) Created Two-Arg One-Arg No-Arg

---

**Q4)** Fill in the blanks (marked // Blank X) to correctly serialize a `Product` object to "product.ser".

```java
import java.io.*;

class Product implements Serializable { // Required for serialization
    private static final long serialVersionUID = 1L; // Good practice
    String name = "Laptop";
    double price = 999.99;
}

public class SerializeProduct {
    public static void main(String[] args) {
        Product p = new Product();
        try (FileOutputStream fos = new FileOutputStream("product.ser");
             // Blank 1: Create the appropriate Output Stream wrapper
             ObjectOutputStream oos = new ObjectOutputStream(fos) )
        {
            // Blank 2: Write the object 'p' to the stream
            oos.writeObject(p);
            System.out.println("Product serialized.");
        } catch (IOException e) {
            // Blank 3: Print the stack trace for the exception 'e'
            e.printStackTrace();
        }
    }
}
```
*(This is a fill-in-the-blank question, no options provided in the final paper format)*

---

**Q5)** Identify the single change needed in class `Child`'s constructor to fix the compilation error.

```java
class Parent {
    String message;
    Parent(String msg) { // Only has a parameterized constructor
        this.message = msg;
        System.out.println("Parent Initialized");
    }
}

class Child extends Parent {
    int value;
    Child(int val) {
        // Issue: Implicit super() call fails as Parent has no no-arg constructor
        this.value = val;
        System.out.println("Child Initialized");
    }
}

public class SuperCall {
    public static void main(String[] args) {
        Child c = new Child(10);
    }
}
```
**Options**
1) Add `super();` as the first line in `Child` constructor.
2) Add a no-arg constructor `Parent() {}` to the `Parent` class.
3) Add `super("Default Message");` as the first line in `Child` constructor.
4) Remove the constructor from the `Child` class.

---

**Q6)** Consider the following method and list declarations. Which statement inside the `main` method will cause a compilation error?

```java
import java.util.*;

public class GenericsWildcard {

    // Processes lists of Number or its subtypes (Integer, Double, etc.)
    public static void processNumbers(List<? extends Number> list) {
        double sum = 0;
        for (Number n : list) { // OK: Can read elements as Number
            sum += n.doubleValue();
        }
        System.out.println("Sum: " + sum);
        // list.add(Integer.valueOf(10)); // Cannot safely add
    }

    public static void main(String[] args) {
        List<Integer> integers = new ArrayList<>(Arrays.asList(1, 2, 3));
        List<Double> doubles = new ArrayList<>(Arrays.asList(1.1, 2.2));
        List<String> strings = new ArrayList<>(Arrays.asList("a", "b"));

        // Statement 1:
        processNumbers(integers);

        // Statement 2:
        processNumbers(doubles);

        // Statement 3: (Attempting to add to the list inside the method - commented out above)
        // If the commented line inside processNumbers were uncommented, it would fail.

        // Statement 4:
        // processNumbers(strings); // Which statement causes a compile error here?
    }
}
```
**Options**
1) Statement 1 (`processNumbers(integers);`)
2) Statement 2 (`processNumbers(doubles);`)
3. Statement 3 (The conceptual attempt to add `Integer` inside `processNumbers`)
4. Statement 4 (`processNumbers(strings);`)

---

**Q7)** Fill in the blanks to efficiently build the string "Result: ABC" using `StringBuilder`.

```java
public class BuilderTest {
    public static void main(String[] args) {
        // Blank 1: Create a StringBuilder initialized with "Result: "
        StringBuilder sb = new StringBuilder("Result: ");
        String[] parts = {"A", "B", "C"};

        for (String part : parts) {
            // Blank 2: Append the current 'part' to the StringBuilder
            sb.append(part);
        }

        // Blank 3: Convert the StringBuilder to a String for printing
        String finalResult = sb.toString();
        System.out.println(finalResult); // Should print "Result: ABC"
    }
}
```
*(This is a fill-in-the-blank question, no options provided in the final paper format)*

---

**Q8)** Complete the `catch` block to handle both `FileNotFoundException` and `SQLException` using a single block (multi-catch).

```java
import java.io.*;
import java.sql.*; // For SQLException

public class MultiCatchDemo {
    public void processData(String file, Connection conn) {
        try {
            Reader reader = new FileReader(file); // Might throw FileNotFoundException
            Statement stmt = conn.createStatement(); // Might throw SQLException
            // ... process data ...
            reader.close();
            stmt.close();
        } catch ( /* Blank 1: Specify both exception types using | */ FileNotFoundException | SQLException e ) {
            System.err.println("Handling I/O or SQL error: " + e.getMessage());
            // Blank 2: Perform common error logging action, e.g., logError(e);
            logError(e);
        } catch (IOException e) { // Catch other IOExceptions separately if needed
             System.err.println("Other IO error: " + e.getMessage());
        }
    }
    // Helper method assumed to exist
    private static void logError(Exception e) { /* logs the exception */ }
}
```
*(This is a fill-in-the-blank question, no options provided in the final paper format)*

---

**Q9)** What is the primary reason the following code fails to compile?

```java
class BaseAction {
    public final void performBase() {
        System.out.println("Base Action");
    }
}

class DerivedAction extends BaseAction {
    // Issue is here
    @Override
    public void performBase() { // Attempting to override
        System.out.println("Derived Action attempting override");
    }
}

public class FinalMethodTest {
    public static void main(String[] args) {
        DerivedAction da = new DerivedAction();
        da.performBase();
    }
}
```
**Options**
1) The `@Override` annotation is incorrect.
2) `DerivedAction` cannot extend `BaseAction`.
3) The `performBase` method in `DerivedAction` has the wrong access modifier.
4) `final` methods (like `performBase` in `BaseAction`) cannot be overridden.

---

**Q10)** What is the output of this code snippet involving bitwise operators?

```java
public class BitwiseOp {
    public static void main(String[] args) {
        int a = 13; // Binary: 1101
        int b = 9;  // Binary: 1001
        int result = a & b; // Bitwise AND
        // 1101
        // 1001
        // ----
        // 1001 (Decimal 9)
        System.out.println(result);
    }
}
```
**Options**
1) 13
2) 9
3) 1
4) 22

---

**Q11)** Consider the `calculate` method. What must be true about the local variable `factor` for this code to compile?

```java
public class LocalInnerAccess {

    public void calculate(int initialValue) {
        int factor = 10; // Local variable

        class Multiplier {
            int multiply() {
                // Accessing local variable 'factor'
                return initialValue * factor;
            }
        }

        // factor = 20; // If this line were added here, it would cause a problem

        Multiplier m = new Multiplier();
        System.out.println("Result: " + m.multiply());
    }

    public static void main(String[] args) {
        new LocalInnerAccess().calculate(5);
    }
}
```
**Options**
1) `factor` must be declared `static`.
2) `factor` must be declared `public`.
3. `factor` must be `final` or *effectively final*.
4. `factor` must be declared outside the `calculate` method.

---

**Q12)** What is the output of the following code?

```java
interface Movable { void move(); }
class Car implements Movable {
    @Override public void move() { System.out.println("Car moves"); }
}
class Bike implements Movable {
    @Override public void move() { System.out.println("Bike moves"); }
}

public class InstanceofInterface {
    public static void main(String[] args) {
        Movable m = new Bike();
        boolean isCar = m instanceof Car;
        boolean isBike = m instanceof Bike;
        boolean isMovable = m instanceof Movable;

        System.out.println(isCar + ", " + isBike + ", " + isMovable);
    }
}
```
**Options**
1) true, false, true
2) false, true, false
3) false, true, true
4) true, true, true

---

**Q13)** Fill in the blanks to access and print the element `8` from the `data` array.

```java
public class MultiDimAccess {
    public static void main(String[] args) {
        int[][] data = { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} };

        // Element 8 is at row index 2, column index 1

        // Blank 1: Specify the row index
        int rowIndex = 2;
        // Blank 2: Specify the column index
        int colIndex = 1;

        // Blank 3: Access the element using both indices
        int element = data[rowIndex][colIndex];

        System.out.println("Element: " + element); // Should print Element: 8
    }
}
```
*(This is a fill-in-the-blank question, no options provided in the final paper format)*

---

**Q14)** Arrange the following code lines in the correct order to get the current date, add 10 days to it, and print it in `dd-MM-yyyy` format.

```java
// Code Lines (Arrange these)
1. DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
2. LocalDate futureDate = currentDate.plusDays(10);
3. System.out.println(formattedDate);
4. LocalDate currentDate = LocalDate.now();
5. String formattedDate = futureDate.format(formatter);
```
**Options**
1) 4, 1, 2, 5, 3
2) 1, 4, 2, 5, 3
3) 4, 2, 1, 5, 3
4) 4, 2, 5, 1, 3

---

**Q15)** Arrange the following lines to define a simple `Person` class, create an object, and call its method.

```java
// Code Lines (Arrange these)
1. } // End of main method
2. person.display();
3. public static void main(String[] args) {
4. class Person { void display() { System.out.println("Person object"); } }
5. Person person = new Person();
6. public class SimpleClass {
7. } // End of SimpleClass
8. } // End of Person class (assuming display is the only method)
```
*(Note: Assume line 4 defines the complete Person class for simplicity)*

**Options**
1) 6, 4, 8, 3, 5, 2, 1, 7
2) 4, 8, 6, 3, 5, 2, 1, 7
3) 6, 3, 4, 8, 5, 2, 1, 7
4) 6, 4, 8, 7, 3, 5, 2, 1

---