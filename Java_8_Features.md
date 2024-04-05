# The major features introduced in **Java 8**: #

1. **Lambda Expressions**:
   - Lambda expressions provide a concise way to represent a method of a functional interface using an expression.
   - They are particularly useful in collection libraries, where they facilitate iteration, filtering, and data extraction.
   - Here's an example of a lambda expression:
     ```java
     List<String> names = Arrays.asList("John", "Jane", "Adam", "Eve");
     names.forEach(name -> System.out.println(name));
     ```

2. **Functional Interfaces**:
   - A functional interface is an interface that contains only one abstract method.
   - It can also have any number of default and static methods.
   - Example of a functional interface:
     ```java
     @FunctionalInterface
     interface Greeting {
         void sayHello(String name);
     }
     ```

3. **Method References**:
   - Method references provide a shorthand notation for calling a method using lambda expressions.
   - There are four types of method references:
     - Static method reference
     - Instance method reference of a particular object
     - Instance method reference of an arbitrary object of a particular type
     - Constructor reference.
   - Example of a method reference:
     ```java
     List<String> names = Arrays.asList("John", "Jane", "Adam", "Eve");
     names.forEach(System.out::println);
     ```

4. **Streams**:
   - The Stream API is used to process collections of objects in a functional style using lambda expressions.
   - Example of using streams:
     ```java
     List<String> names = Arrays.asList("John", "Jane", "Adam", "Eve");
     names.stream()
          .filter(name -> name.startsWith("J"))
          .forEach(System.out::println);
     ```

5. **Optional Class**:
   - Java introduced the `Optional` class in Java 8 to handle `NullPointerException` scenarios in a more robust way.
   - Example of using `Optional`:
     ```java
     Optional<String> optional = Optional.of("John");
     optional.ifPresent(System.out::println);
     ```

6. **Date/Time API**:
   - Java 8 introduced a new Date and Time API, which provides improved functionality for working with dates and times.
   - Example of using the Date/Time API:
     ```java
     LocalDate date = LocalDate.now();
     System.out.println(date);
     ```

7. **Default Methods**:
   - Java allows creating default methods in interfaces, which provide a way to add new methods to existing interfaces without breaking backward compatibility.
   - Default methods have an implementation in the interface itself.
   - Example of a default method:
     ```java
     interface MyInterface {
         default void myDefaultMethod() {
             System.out.println("This is a default method.");
         }
     }
     ```



# Explanation with code #

## 1. Lambda Expressions

### Overview

Lambda expressions in Java are a concise way to express instances of functional interfaces. They allow you to define a short block of code that accepts input as parameters and returns a result. Introduced in Java 8, lambda expressions simplify coding by providing a more readable and straightforward syntax.

### Advantages of Lambda Expressions

1. **Conciseness**:
   - Lambda expressions enable clear and expressive code, improving readability and modularity.
   - They allow you to define behavior more concisely, particularly for small, single-purpose methods.

2. **Flexibility**:
   - Lambda expressions let you create code that can accept functions as parameters.
   - This flexibility makes your code more dynamic and adaptable.

### Example:

```java
// Before Java 8: Creating a new thread using an anonymous inner class
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("New thread created");
    }
}).start();

// Java 8 onwards: Creating a new thread using a lambda expression
new Thread(() -> System.out.println("New thread created")).start();
```

## 2. Functional Interfaces

### Overview

- A **functional interface** is an interface that contains only one abstract method.
- From Java 8 onwards, lambda expressions can represent instances of functional interfaces.
- Examples of functional interfaces include `Runnable`, `ActionListener`, and `Comparable`.

### Advantages:

1. **Abstraction**:
   - Functional interfaces allow you to create abstractions that multiple classes can use without duplicating code.
   - You can define complex abstractions with various methods and behaviors.

2. **Functional Programming**:
   - Functional interfaces enable functional programming paradigms in Java.
   - They allow you to pass behavior (methods) as arguments, making your code more modular.

### Example:

```java
@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();
}

// Usage
MyFunctionalInterface func = () -> System.out.println("Doing something");
func.doSomething();
```

## 3. Inheritance in Functional Interfaces

- Functional interfaces can extend other interfaces (interface inheritance).
- Inheritance ensures that the extended interface also remains functional (i.e., contains only one abstract method).

    Functional interfaces in Java are interfaces that have exactly one abstract method. They are a new feature introduced in Java 8 to support lambda expressions and make the code more readable and straightforward.

    Inheritance in functional interfaces works similarly to class inheritance, but with some differences. An interface can extend another interface, and in doing so, it inherits all of its parent interface's methods. Here's an example:

    ```java
    @FunctionalInterface
    interface Interface1 {
        void method1();
    }

    @FunctionalInterface
    interface Interface2 extends Interface1 {
        void method2();
    }
    ```

    In this example, `Interface2` extends `Interface1`, so any class that implements `Interface2` will have to provide implementations for both `method1` and `method2`.

    Java also supports multiple interface inheritance, where an interface extends more than one super interface⁵. Here's an example:

    ```java
    @FunctionalInterface
    interface Interface1 {
        void method1();
    }

    @FunctionalInterface
    interface Interface2 {
        void method2();
    }

    @FunctionalInterface
    interface Interface3 extends Interface1, Interface2 {
        void method3();
    }
    ```

    In this example, `Interface3` extends both `Interface1` and `Interface2`, so any class that implements `Interface3` will have to provide implementations for `method1`, `method2`, and `method3`.

    However, if two interfaces have default methods with the same signature, a class implementing both interfaces must override that method to resolve the conflict.


## 4. Default Methods Inside Interface

- Default methods allow you to add new methods to an interface without affecting implementing classes.
- They provide a default implementation, which can be overridden in implementing classes.
- Useful for backward compatibility and preserving existing implementations.

## 5. Static Methods Inside Interface

- Static methods in interfaces are used to define utility methods.
- They cannot be overridden in implementing classes.
- Useful for providing common utility methods related to the interface.

## 6. Functional Interface as a Type for Lambda Expressions

- Lambda expressions can be assigned to functional interface objects.
- The interface type acts as a blueprint for the lambda expression.


    A functional interface is an interface that has exactly one abstract method. This makes it a perfect candidate for being used as a type for lambda expressions¹. Lambda expressions are a feature introduced in Java 8 that allow you to write shorter and more readable code¹.

    Here's an example of a functional interface and a lambda expression:

    ```java
    @FunctionalInterface
    public interface SquareRoot {
        double findSquareRoot(int n);
    }

    SquareRoot squareRoot = (n) -> Math.sqrt(n);
    ```

    In this example, `SquareRoot` is a functional interface with a single abstract method `findSquareRoot(int n)`. The lambda expression `(n) -> Math.sqrt(n)` provides an implementation for this method¹.

    The `squareRoot` variable is of type `SquareRoot`, and its value is a lambda expression. This lambda expression is an instance of the `SquareRoot` functional interface¹.

    The lambda expression `(n) -> Math.sqrt(n)` takes an integer `n` as input and returns the square root of `n`. The left side of the `->` operator specifies the input parameters, and the right side specifies the body of the function¹.

    This is a very powerful feature of Java 8 and later, as it allows you to write more concise and readable code¹.


## 7. Creating Threads Using Lambda Expressions

- You can create threads using lambda expressions for `Runnable` or `Callable` tasks.

1. **Lambda Expressions in Java:**
   - Lambda expressions were introduced in **Java SE8**. They are designed for **functional interfaces**, which are interfaces with only one abstract method.
   - The syntax for a lambda expression is: `(argument1, argument2, ... argument n) -> { /* statements */ }`.

2. **Creating Threads with Lambda Expressions:**
   - We will demonstrate three examples of creating threads using lambda expressions.

   **Example 1: Basic Thread Creation**
   ```java
   public class Test {
       public static void main(String[] args) {
           Runnable myThread = () -> {
               Thread.currentThread().setName("myThread");
               System.out.println(Thread.currentThread().getName() + " is running");
           };
           Thread run = new Thread(myThread);
           run.start();
       }
   }
   ```
   Output:
   ```
   myThread is running
   ```

   **Example 2: Multiple Threads**
   ```java
   public class Test {
       public static void main(String[] args) {
           Runnable basic = () -> {
               String threadName = Thread.currentThread().getName();
               System.out.println("Running common task by " + threadName);
           };
           Thread thread1 = new Thread(basic);
           Thread thread2 = new Thread(basic);
           thread1.start();
           thread2.start();
       }
   }
   ```
   Output:
   ```
   Running common task by Thread-1
   Running common task by Thread-0
   ```

   **Example 3: Custom Thread Behavior**
   ```java
   import java.util.Random;

   class RandomPlayer {
       public void playGame(String gameName) throws InterruptedException {
           System.out.println(gameName + " game started");
           Thread.sleep(500);
           System.out.println(gameName + " game ended");
       }

       public void playMusic(String trackName) throws InterruptedException {
           System.out.println(trackName + " track started");
           Thread.sleep(500);
           System.out.println(trackName + " track ended");
       }
   }

   public class Test {
       static String[] games = { "COD", "Prince Of Persia", "GTA-V5", "Valorant", "FIFA 22", "Fortnite" };
       static String[] tracks = { "Believer", "Cradles", "Taki Taki", "Sorry", "Let Me Love You" };

       public static void main(String[] args) {
           RandomPlayer player = new RandomPlayer();
           Random random = new Random();

           Runnable gameRunner = () -> {
               try {
                   player.playGame(games[random.nextInt(games.length)]);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
           };

           Runnable musicPlayer = () -> {
               try {
                   player.playMusic(tracks[random.nextInt(tracks.length)]);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
           };

           Thread game = new Thread(gameRunner);
           Thread music = new Thread(musicPlayer);

           game.start();
           music.start();
       }
   }
   ```
   Output:
   ```
   Believer track started
   GTA-V5 game started
   Believer track ended
   GTA-V5 game ended
   ```
   Feel free to experiment with these examples and explore the power of lambda expressions in multithreading! 🚀

## 8. Comparator in Lambda Expressions

- Lambda expressions simplify custom sorting using `Comparator`.
- Example: Sorting a list of strings by length.



    A `Comparator` is a functional interface that represents an ordering of objects. In Java 8 and later, you can use lambda expressions to create a `Comparator` in a more concise and readable way. Here's an example:

    ```java
    List<String> names = Arrays.asList("Paul", "Jane", "Michael", "Chris");
    Comparator<String> nameComparator = (name1, name2) -> name1.compareTo(name2);
    names.sort(nameComparator);
    ```

    In this example, `(name1, name2) -> name1.compareTo(name2)` is a lambda expression that compares two strings. It's used to create a `Comparator<String>`.

    You can also use method references with `Comparator.comparing()`, which can make your code even more concise:

    ```java
    Comparator<String> nameComparator = Comparator.comparing(name -> name);
    names.sort(nameComparator);
    ```

    Or even simpler with a method reference:

    ```java
    Comparator<String> nameComparator = Comparator.comparing(String::valueOf);
    names.sort(nameComparator);
    ```

    If you want to sort in reverse order, you can use `Comparator.reversed()`:

    ```java
    Comparator<String> reversedNameComparator = Comparator.comparing(String::valueOf).reversed();
    names.sort(reversedNameComparator);
    ```

    And if you want to chain multiple comparators, you can use `Comparator.thenComparing()`:

    ```java
    Comparator<Student> studentComparator = Comparator.comparing(Student::getLastName)
                                                        .thenComparing(Student::getFirstName);
    students.sort(studentComparator);
    ```

    In this last example, students are sorted by last name, and then by first name within each group of students with the same last name.


## 9. TreeSet and TreeMap with Comparator in Lambda Expressions

- You can customize sorting order using lambda expressions in `TreeSet` and `TreeMap`.

Certainly! Let's explore how to use **lambda expressions** to create `TreeSet` and `TreeMap` with custom comparators in Java. We'll provide detailed code examples for both data structures.

## 1. **Creating a `TreeSet` with a Custom Comparator:**

A `TreeSet` is an implementation of the `Set` interface that maintains elements in a sorted order. By default, it uses natural ordering (based on the elements' `compareTo` method) or allows custom sorting using a provided `Comparator`.

### Example 1: Basic `TreeSet` with Custom Comparator

Suppose we have a class `Employee` with attributes like `id`, `name`, and `age`. We want to create a `TreeSet` of employees sorted by their names.

```java
import java.util.Comparator;
import java.util.TreeSet;

class Employee {
    public int id;
    public String name;
    public Integer age;

    Employee(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return id + " " + name + " " + age;
    }
}

public class TreeSetExample {
    public static void main(String[] args) {
        // Create a TreeSet with a custom comparator for Employee names
        TreeSet<Employee> employeesByName = new TreeSet<>(
            (e1, e2) -> e1.name.compareTo(e2.name)
        );

        employeesByName.add(new Employee(1, "Alice", 30));
        employeesByName.add(new Employee(2, "Bob", 28));
        employeesByName.add(new Employee(3, "Charlie", 25));

        for (Employee employee : employeesByName) {
            System.out.println(employee);
        }
    }
}
```

Output:
```
1 Alice 30
2 Bob 28
3 Charlie 25
```

### Example 2: Reverse Sorting by Names

If you want to sort in descending order by names, you can use the following comparator:

```java
TreeSet<Employee> employeesByNameDesc = new TreeSet<>(
    (e1, e2) -> e2.name.compareTo(e1.name)
);
```

## 2. **Creating a `TreeMap` with a Custom Comparator:**

A `TreeMap` is a sorted map implementation in Java. Similar to `TreeSet`, it uses natural ordering or a custom comparator for sorting keys.

### Example: `TreeMap` with Custom Comparator

Suppose we want to create a `TreeMap` where keys are integers (representing employee IDs) and values are employee names. We will sort the keys in descending order.

```java
import java.util.Comparator;
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        // Create a TreeMap with a custom comparator for integer keys
        TreeMap<Integer, String> employeeMap = new TreeMap<>(
            Comparator.reverseOrder()
        );

        employeeMap.put(101, "Alice");
        employeeMap.put(102, "Bob");
        employeeMap.put(103, "Charlie");

        for (Integer id : employeeMap.keySet()) {
            System.out.println(id + ": " + employeeMap.get(id));
        }
    }
}
```

Output:
```
103: Charlie
102: Bob
101: Alice
```

In both examples, we use lambda expressions to define custom comparators for sorting elements. Lambda expressions make the code concise and expressive, allowing us to create custom sorting logic easily.

Remember that lambda expressions work well with functional interfaces, and in these cases, we use the `Comparator` interface.


## 10. Anonymous Inner Class vs. Lambda Expression

- Anonymous inner classes are verbose; lambda expressions are concise.
- Lambda expressions are preferred for simple behavior.


Certainly! Let's explore the differences between **anonymous inner classes** and **lambda expressions** in Java, along with code examples.

## **1. Anonymous Inner Class:**
- An anonymous inner class is an inner class without a name. It is created on the fly and typically used for specific scenarios.
- Anonymous inner classes can extend abstract or concrete classes and implement interfaces.
- They are useful when you need to create an instance of an object with certain "extras" (such as overloading methods) without explicitly subclassing a class.
- Commonly used for writing implementation classes for listener interfaces in graphics programming.

### **Example: Anonymous Inner Class Implementing an Interface**
Suppose we have the following simple program with an interface `Age`:

```java
interface Age {
    int x = 21;
    void getAge();
}

class AnonymousDemo {
    public static void main(String[] args) {
        Age obj = new Age() {
            @Override
            public void getAge() {
                System.out.println("Age is " + x);
            }
        };
        obj.getAge();
    }
}
```

Output:
```
Age is 21
```

## **2. Lambda Expressions:**
- Lambda expressions were introduced in Java 8 and are used for functional programming.
- They express instances of functional interfaces (interfaces with a single abstract method).
- Lambda expressions allow treating functionality as a method argument or code as data.
- They are concise and provide a way to create functions without belonging to any class.

### **Example: Lambda Expression for a Functional Interface**
Let's create a simple functional interface `FuncInterface`:

```java
interface FuncInterface {
    void abstractFun(int x);
    default void normalFun() {
        System.out.println("Hello");
    }
}

class Test {
    public static void main(String[] args) {
        FuncInterface fobj = (int x) -> System.out.println(2 * x);
        fobj.abstractFun(5);
    }
}
```

Output:
```
10
```

## **Table of Differences:**
| Aspect                  | Anonymous Inner Class                          | Lambda Expression                                           |
|-------------------------|------------------------------------------------|-------------------------------------------------------------|
| Class/Method Name       | No name (anonymous)                            | No name (anonymous function)                                |
| Extends/Implements      | Can extend abstract/concrete classes           | Cannot extend classes                                       |
| Interface Implementation| Can implement interfaces with multiple methods | Implements interfaces with a single abstract method         |
| Instance Variables      | Can declare instance variables                 | Does not allow instance variables (acts as local variables) |
| Instantiation           | Can be instantiated                            | Cannot be directly instantiated                             |
| `this` Reference        | Refers to the anonymous inner class object     | Refers to the enclosing class object                        |

In summary, anonymous inner classes are a good choice when handling multiple methods, while lambda expressions are specifically designed for functional interfaces and provide concise syntax for creating functions. Remember that "this" behaves differently inside each construct: in anonymous inner classes, it refers to the inner class object, while in lambda expressions, it refers to the enclosing class object.



### Variable Declaration Inside Anonymous Inner Class and Use of `this` Keyword

- Variables declared inside an anonymous inner class have their own scope.
- The `this` keyword refers to the inner class instance, not the outer class.



## 11. In Java 8, a **Predicate** is a functional interface that allows you to test a value or an object against a condition and returns a **boolean** value. It's part of the `java.util.function` package and contains only one abstract method: `boolean test(T t)`, where `T` represents the type of the input argument.

Let's dive into more detail with examples:

1. **Creating a Simple Predicate**:
    - Suppose we want to check if an integer is less than 18. We can create a simple `Predicate<Integer>` as follows:

    ```java
    import java.util.function.Predicate;

    public class PredicateInterfaceExample1 {
        public static void main(String[] args) {
            Predicate<Integer> lesserThan = i -> (i < 18);
            System.out.println(lesserThan.test(10)); // Output: true
        }
    }
    ```

    In this example, the `lesserThan` predicate tests whether the given integer is less than 18.

2. **Predicate Chaining**:
    - You can combine multiple predicates using logical operations like `and`, `or`, and `negate`.
    - Let's say we want to check if a number is greater than 10 and less than 20:

    ```java
    import java.util.function.Predicate;

    public class PredicateInterfaceExample2 {
        public static void main(String[] args) {
            Predicate<Integer> greaterThanTen = i -> i > 10;
            Predicate<Integer> lowerThanTwenty = i -> i < 20;

            boolean result = greaterThanTen.and(lowerThanTwenty).test(15);
            System.out.println(result); // Output: true
        }
    }
    ```

    Here, we've combined two predicates using `and`. The `result` will be `true` if the number is greater than 10 and less than 20.

3. **Other Useful Methods**:
    - `isEqual(Object targetRef)`: Returns a predicate that tests if two arguments are equal according to `Objects.equals(Object, Object)`.
    - `negate()`: Returns a predicate that represents the logical negation of the original predicate.
    - `or(Predicate other)`: Returns a composed predicate that represents a short-circuiting logical OR of the original predicate and another.

Remember, **Predicates** are powerful tools for filtering and processing data, especially when working with collections using the Stream API. They improve code manageability and allow you to express complex conditions concisely. 🚀


## 12. In Java 8, a **functional interface** is an interface that has exactly one abstract method. It is also known as a **Single Abstract Method (SAM) interface**. These interfaces play a crucial role in enabling the use of **lambda expressions**, which provide a more concise and expressive way to write functional-style code.

Let's explore functional interfaces in more detail:

1. **Introduction to Functional Interfaces**:
    - A functional interface contains only one abstract method.
    - From Java 8 onwards, **lambda expressions** can be used to represent instances of functional interfaces.
    - A functional interface can also have any number of **default methods**.
    - It's recommended that all functional interfaces have an informative `@FunctionalInterface` annotation. This communicates the purpose of the interface and allows the compiler to generate an error if the annotated interface does not satisfy the conditions.

2. **Function Interface**:
    - The most simple and general case of a lambda is a functional interface with a method that receives one value and returns another.
    - The `Function` interface, parameterized by the types of its argument and return value, represents such a function:
        ```java
        import java.util.function.Function;

        public interface Function<T, R> {
            R apply(T t);
        }
        ```
    - One common usage of the `Function` type in the standard library is the `Map.computeIfAbsent` method. This method returns a value from a map by key, but calculates a value if the key is not already present:
        ```java
        import java.util.Map;
        import java.util.HashMap;

        public class FunctionInterfaceExample {
            public static void main(String[] args) {
                Map<String, Integer> nameMap = new HashMap<>();
                Integer value = nameMap.computeIfAbsent("John", s -> s.length());
                System.out.println(value); // Output: 4 (length of "John")
            }
        }
        ```
    - In this example, we calculate a value by applying a function to a key, put it inside a map, and return it from the method call.

3. **Other Functional Interfaces**:
    - Besides `Function`, Java 8 provides several other functional interfaces such as `Predicate`, `Consumer`, `Supplier`, and more.
    - Each of these interfaces serves a specific purpose and allows you to express different types of behavior concisely using lambda expressions.

Remember, functional interfaces are powerful tools for writing expressive and functional-style code in Java. They simplify the creation of anonymous functions and enhance code readability. 🚀


## 13. In Java 8, the **Consumer** interface is a powerful functional interface that allows you to perform operations on an input value without returning any result. It's part of the `java.util.function` package and is widely used for side-effect operations.

Let's explore the `Consumer` interface in detail with examples:

1. **Creating a Simple Consumer**:
    - A `Consumer` takes an input value (of type `T`) and performs an operation on it. It doesn't return any value.
    - Here's an example of a simple `Consumer` that prints an integer:

    ```java
    import java.util.function.Consumer;

    public class ConsumerExample {
        public static void main(String[] args) {
            Consumer<Integer> display = a -> System.out.println(a);
            display.accept(10); // Output: 10
        }
    }
    ```

    In this example, the `display` consumer accepts an integer and prints it.

2. **Chaining Consumers with `andThen()`**:
    - You can chain multiple consumers together using the `andThen()` method. It creates a new consumer that executes the first consumer followed by the second one.
    - For instance, let's modify a list of integers by doubling each element and then display the modified list:

    ```java
    import java.util.ArrayList;
    import java.util.List;
    import java.util.function.Consumer;

    public class ConsumerChainingExample {
        public static void main(String[] args) {
            Consumer<List<Integer>> modify = list -> {
                for (int i = 0; i < list.size(); i++)
                    list.set(i, 2 * list.get(i));
            };

            Consumer<List<Integer>> dispList = list ->
                list.stream().forEach(a -> System.out.print(a + " "));

            List<Integer> list = new ArrayList<>();
            list.add(2);
            list.add(1);
            list.add(3);

            modify.andThen(dispList).accept(list); // Output: 4 2 6
        }
    }
    ```

    In this example, the `modify` consumer doubles each element in the list, and the `dispList` consumer displays the modified list.

3. **Use Cases for Consumers**:
    - Consumers are useful when you want to perform actions that don't return a result, such as updating data structures, logging, or printing.
    - They allow you to separate behavior from control flow, making your code more modular and expressive.

Remember, **Consumers** are essential for functional programming in Java, especially when working with collections and streams. They help you achieve cleaner and more concise code. 🚀


## 14. In Java 8, the **Supplier** interface is a powerful functional interface that allows you to obtain a value without taking any input. It's part of the `java.util.function` package and is commonly used for lazy evaluation and deferred computation.

Let's explore the `Supplier` interface in detail with examples:

1. **Introduction to Supplier**:
    - A `Supplier` represents a function that produces a value of type `T`.
    - It doesn't take any arguments but provides a result.
    - The lambda expression assigned to a `Supplier` defines its `get()` method, which eventually produces the value.
    - Suppliers are useful when you need to obtain a result without supplying any input.

2. **Creating a Simple Supplier**:
    - Suppose we want to generate a random value. We can create a `Supplier<Double>` as follows:

    ```java
    import java.util.function.Supplier;

    public class SupplierExample {
        public static void main(String[] args) {
            Supplier<Double> randomValue = () -> Math.random();
            System.out.println(randomValue.get()); // Output: 0.5685808855697841
        }
    }
    ```

    In this example, the `randomValue` supplier produces a random double value.

3. **Use Cases for Suppliers**:
    - Suppliers are commonly used in scenarios where you want to defer the computation until the value is actually needed. For instance:
        - **Lazy Initialization**: Creating an object only when it's requested.
        - **Memoization**: Caching expensive computations.
        - **Generating Default Values**: Providing fallback values when needed.

4. **Other Supplier Implementations**:
    - Besides creating custom suppliers, Java 8 provides some built-in suppliers:
        - `Supplier<T>`: General-purpose supplier.
        - `BooleanSupplier`: Produces boolean values.
        - `IntSupplier`: Produces integer values.
        - `LongSupplier`: Produces long values.
        - `DoubleSupplier`: Produces double values.

Remember, **Suppliers** are essential for deferred execution and lazy evaluation. They allow you to separate value production from value consumption, improving efficiency and code readability. 🚀



## 15. The **Java 8** release introduced a revamped **Date-Time API** that addresses the limitations of the older `java.util.Date` and `java.util.Calendar` classes. Let's delve into the details of this new API along with some code examples:

1. **LocalDate**, **LocalTime**, and **LocalDateTime**:
    - These classes provide a simplified date-time API without the complexity of handling time zones.
    - **LocalDate**: Represents a date (year, month, and day) without a time component.
    - **LocalTime**: Represents a time (hours, minutes, seconds, and nanoseconds) without a date component.
    - **LocalDateTime**: Combines both date and time information.
    - Here's an example of using these classes:

```java
import java.time.*;
import java.time.format.DateTimeFormatter;

public class DateExample {
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        System.out.println("Current date: " + date);

        LocalTime time = LocalTime.now();
        System.out.println("Current time: " + time);

        LocalDateTime current = LocalDateTime.now();
        System.out.println("Current date and time: " + current);

        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
        String formattedDateTime = current.format(formatter);
        System.out.println("Formatted date and time: " + formattedDateTime);

        Month month = current.getMonth();
        int day = current.getDayOfMonth();
        int seconds = current.getSecond();
        System.out.println("Month: " + month + ", Day: " + day + ", Seconds: " + seconds);

        LocalDate specificDate = LocalDate.of(1950, 1, 26);
        System.out.println("Republic Day: " + specificDate);

        LocalDateTime specificDateTime = current.withDayOfMonth(24).withYear(2016);
        System.out.println("Specific date with current time: " + specificDateTime);
    }
}
```

2. **ZonedDateTime**:
    - Use this specialized date-time API when considering various time zones.
    - It combines a `LocalDateTime` with a `ZoneId`.
    - Example:

```java
import java.time.*;
import java.time.format.DateTimeFormatter;

public class ZoneExample {
    public static void main(String[] args) {
        LocalDateTime date = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
        String formattedCurrentDate = date.format(formatter);
        System.out.println("Formatted current date and time: " + formattedCurrentDate);

        ZonedDateTime currentZone = ZonedDateTime.now();
        System.out.println("Current zone: " + currentZone.getZone());

        ZoneId tokyo = ZoneId.of("Asia/Tokyo");
        ZonedDateTime tokyoZone = currentZone.withZoneSameInstant(tokyo);
        String formattedTokyoZone = tokyoZone.format(formatter);
        System.out.println("Tokyo time zone: " + formattedTokyoZone);
    }
}
```

In summary, the new Java 8 Date-Time API provides a more robust, thread-safe, and expressive way to handle date and time operations. Feel free to explore these classes further in your projects! 🕰️📅.


## 16.  In **Java 8**, the introduction of the **Stream API** revolutionized how we process collections of objects. Let's dive into the details, along with code examples:

1. **What is the Stream API?**
    - The Stream API is a new abstract layer introduced in Java 8.
    - It allows functional-style operations on elements within collections.
    - Streams are designed for efficiency and can enhance program performance by avoiding unnecessary loops and iterations.
    - You can use streams for filtering, collecting, printing, and converting data structures.

2. **Basic Components of Streams:**
    - **Sequence of Elements**: Streams represent a sequence of components that can be processed sequentially.
    - **Source**: Streams take input from collections, arrays, or I/O channels.
    - **Aggregate Operations**: These operations perform transformations on the stream elements.
    - **Pipelining**: Intermediate operations (like filtering or mapping) can be pipelined, improving efficiency.
    - **Internal Iteration**: Streams handle iteration internally, reducing boilerplate code.

3. **Features of Java Stream:**
    - Streams don't alter the original data structure; they provide results based on pipelined methods.
    - Intermediate operations are lazily executed, returning a stream as a result.
    - Terminal operations mark the end of the stream and return the final result.

4. **Example: Filtering Even Numbers**
    - Suppose we have an `ArrayList` of integers, and we want to filter out even numbers.
    - Let's see how streams work internally:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(10);
        numbers.add(15);
        numbers.add(20);
        numbers.add(25);

        // Using stream to filter even numbers
        List<Integer> evenNumbers = numbers.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());

        System.out.println("Even numbers: " + evenNumbers);
    }
}
```

5. **Explanation**:
    - We create a list of integers (`numbers`).
    - The stream is obtained from the list using `stream()`.
    - The `filter()` operation checks if each number is even.
    - Finally, we collect the filtered numbers into a new list.

6. **Additional Notes**:
    - Streams can be parallelized for better performance using `parallelStream()`.
    - Explore other stream operations like `map`, `reduce`, and `forEach`.

Remember, the Stream API simplifies complex operations and promotes a more concise and expressive coding style.



## 17. Let's explore the **Java 8 Optional** class, which was introduced to handle optional values and reduce the occurrence of **NullPointerExceptions**. I'll provide explanations and code examples to illustrate its usage.

1. **Overview of Java 8 Optional**:
    - The `Optional` class provides a type-level solution for representing optional values instead of using null references.
    - It's part of the `java.util` package and aims to make code more robust by avoiding unexpected null values.
    - Here's why we should care about `Optional`:
        - It helps prevent null pointer exceptions.
        - It promotes cleaner and more concise code.

2. **Creating Optional Objects**:
    - We can create `Optional` objects in several ways:
        - To create an empty `Optional`, use the `empty()` static method:
            ```java
            Optional<String> empty = Optional.empty();
            assertFalse(empty.isPresent());
            ```
        - To create an `Optional` with a non-null value, use `of()`:
            ```java
            String name = "baeldung";
            Optional<String> opt = Optional.of(name);
            assertTrue(opt.isPresent());
            ```
        - If you expect null values, use `ofNullable()`:
            ```java
            String nullableName = null;
            Optional<String> nullableOpt = Optional.ofNullable(nullableName);
            assertFalse(nullableOpt.isPresent());
            ```

3. **Checking Value Presence**:
    - Use `isPresent()` to check if a value exists inside an `Optional`:
        ```java
        Optional<String> nonNullOpt = Optional.of("Baeldung");
        assertTrue(nonNullOpt.isPresent());

        Optional<String> nullOpt = Optional.ofNullable(null);
        assertFalse(nullOpt.isPresent());
        ```
    - As of Java 11, you can also use `isEmpty()` to check if the `Optional` is empty.

4. **Conditional Action with `ifPresent()`**:
    - Execute a block of code if a value is present:
        ```java
        Optional<String> greeting = Optional.of("Hello, world!");
        greeting.ifPresent(message -> System.out.println("Message: " + message));
        ```

5. **Default Value with `orElse()`**:
    - Get the value if present; otherwise, return a default value:
        ```java
        Optional<String> maybeName = Optional.ofNullable(null);
        String name = maybeName.orElse("Unknown");
        System.out.println("Name: " + name);
        ```

6. **Default Value with `orElseGet()`**:
    - Similar to `orElse()`, but the default value is computed lazily:
        ```java
        String computedName = maybeName.orElseGet(() -> computeNameFromDatabase());
        ```

7. **Exceptions with `orElseThrow()`**:
    - Throw a custom exception if the value is absent:
        ```java
        String fetchedName = maybeName.orElseThrow(() -> new NoSuchElementException("Name not found"));
        ```

Remember, using `Optional` can lead to more robust and expressive code. Explore these methods further and adapt them to your specific use cases! 🚀🔍

