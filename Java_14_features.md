## Java 14, released on March 17, 2020, introduced several new features and improvements. Here are some of the key additions: ##

1. **Switch Expressions (JEP 361)**: Switch expressions were standardized in Java 14. They were first introduced as a preview feature in JDK 12. This feature allows for more succinct code writing. For example, you can write switch expressions as follows:
    ```java
    boolean isTodayHoliday = switch (day) {
        case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> false;
        case "SATURDAY", "SUNDAY" -> true;
        default -> throw new IllegalArgumentException("What's a " + day);
    };
    ```

2. **Text Blocks (JEP 368)**: Text blocks, still a preview feature in Java 14, aim to make multiline strings easier to use. They introduced two new escape sequences: `\\` to indicate the end of the line without introducing a new line character, and `\\s` to indicate a single space¹.

3. **Pattern Matching for instanceof (JEP 305)**: This feature was introduced to eliminate boilerplate code and make the developer’s life a little bit easier². For example, you can write:
    ```java
    if (obj instanceof String s) {
        // can use s here
    } else {
        // can't use s here
    }
    ```

4. **Helpful NullPointerExceptions**: Java 14 improves the usability of NullPointerExceptions generated by the JVM by describing precisely which variable was null.

5. **Record Type (Preview)**: This is a new feature added in Java 14.

6. **Non-Volatile Mapped Byte Buffers (Incubator)**: This is another new feature added in Java 14.

Please note that some features were also deprecated in Java 14, such as Solaris and SPARC Ports (JEP 362) and ParallelScavenge + SerialOld GC Combination (JEP 366)¹.


# #
## A.  Switch Expressions ##
In Java 14, the switch statement was enhanced to become more expressive and less error-prone. The new switch expression is both a statement and an expression. It returns a value, which makes the code more readable and eliminates the need for break statements.

Here's an example of how you can use switch expressions in Java 14:

```java
public class Main {
    public static void main(String[] args) {
        String day = "MONDAY";
        String result = switch (day) {
            case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> "Weekday";
            case "SATURDAY", "SUNDAY" -> "Weekend";
            default -> throw new IllegalArgumentException("Invalid day: " + day);
        };
        System.out.println(result);  // prints "Weekday"
    }
}
```

In this example, the `switch` expression takes a variable `day`. Depending on the value of `day`, it returns either "Weekday" or "Weekend". If the value of `day` is not a valid day of the week, it throws an `IllegalArgumentException`. The returned value from the `switch` expression is assigned to the `result` variable, which is then printed out.

This is a more succinct and safer way to write switch statements, as it eliminates the possibility of fall-through, where execution would continue into the next case if a `break` statement is forgotten. It also allows you to return a value directly from the `switch` expression, making the code more readable. 

Please note that this feature is available from Java 14 onwards. If you're using an older version of Java, you'll need to upgrade to use this feature.

Yes, you're correct. The use of `yield` in Java 14's switch expressions is optional. You can choose to use it when you want to return a value from a block of code in a case. If a case only has a single expression that is returned, you can write it directly after the arrow (`->`) without using `yield`. Here are both styles for comparison:

**Without `yield`:**

```java
String day = "MONDAY";
String result = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> "Weekday";
    case "SATURDAY", "SUNDAY" -> "Weekend";
    default -> throw new IllegalArgumentException("Invalid day: " + day);
};
```

**With `yield`:**

```java
String day = "MONDAY";
String result = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> {
        yield "Weekday";
    }
    case "SATURDAY", "SUNDAY" -> {
        yield "Weekend";
    }
    default -> {
        throw new IllegalArgumentException("Invalid day: " + day);
    }
};
```

In both examples, the `switch` expression works the same way. The choice between using `yield` or not depends on your preference and the complexity of the code in each case of your switch expression. If the code is complex and contains multiple statements, using `yield` can make it clearer that a value is being returned from that block of code. On the other hand, for simple, single-expression cases, directly returning the value can make your code more concise.

## B. Pattern Matching for instanceof ##
Pattern Matching for `instanceof` (JEP 305) is a preview feature in Java 14. It enhances the Java programming language with pattern matching for the `instanceof` operator. This feature simplifies common coding patterns by allowing the conditional extraction of components from objects.

Here's an example of how you can use pattern matching with `instanceof` in Java 14:

```java
public class Main {
    public static void main(String[] args) {
        Object obj = "Hello, World!";
        
        if (obj instanceof String s) {
            System.out.println("String length is: " + s.length());
        } else {
            System.out.println("Not a string");
        }
    }
}
```

In this example, `obj` is an object of type `Object`. The `instanceof` operator is used to check if `obj` is an instance of `String`. If it is, it's automatically cast to `String` and assigned to the variable `s`. This eliminates the need for a separate explicit casting step. If `obj` is not a `String`, the else branch is executed.

Please note that this feature is available from Java 14 onwards as a preview feature. If you're using an older version of Java, you'll need to upgrade to use this feature. Also, because it's a preview feature, you'll need to enable it using the `--enable-preview` flag when compiling and running your code. 

This feature can make your code more readable and safer by eliminating the need for explicit casts and reducing the potential for `ClassCastException`. It's especially useful in situations where you have complex conditional logic based on the type of objects.


## C. Helpful NullPointerExceptions ##
In Java 14, a new feature called "Helpful NullPointerExceptions" was introduced. This feature improves the usability of NullPointerExceptions generated by the JVM by describing precisely which variable was null¹².

Traditionally, when a NullPointerException was thrown, it was difficult to determine which variable was null without using a debugger. The JVM would only print out the method, filename, and line number that caused the exception¹.

With Java 14, the JVM can provide a detailed NullPointerException message by describing the null variable, alongside the method, filename, and line number¹. This is achieved by analyzing the program’s bytecode instructions¹.

However, this detailed exception message is switched off by default in JDK 14. To enable it, you need to use the command-line option: `-XX:+ShowCodeDetailsInExceptionMessages`¹.

Here's an example of how this works:

```java
public class HelpfulNullPointerException {
    public static void main(String[] args) {
        Employee e = null;
        System.out.println(e.getName());
    }
}

class Employee {
    Long id;
    String name;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

If you run this code without the `-XX:+ShowCodeDetailsInExceptionMessages` flag, you'll get a traditional NullPointerException message:

```
Exception in thread "main" java.lang.NullPointerException
    at com.howtodoinjava.core.basic.HelpfulNullPointerException.main(HelpfulNullPointerException.java:9)
```

But if you run it with the `-XX:+ShowCodeDetailsInExceptionMessages` flag, you'll get a more helpful message:

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "com.howtodoinjava.core.basic.Employee.getName()" because "e" is null
    at com.howtodoinjava.core.basic.HelpfulNullPointerException.main(HelpfulNullPointerException.java:9)
```

This time, from the additional information, we know that the null variable `e` causes our exception². This enhancement can save us time during debugging.


## D. Record ##

A record in Java is a special class type that acts as a transparent carrier for immutable data². It's designed to be used in places where a class is created only to act as a plain data carrier². The important difference between a class and a record is that a record aims to eliminate all the boilerplate code needed to set and get the data from the instance².

Consider a scenario where you're developing a system that handles employee data. Traditionally, you would create a class `Employee` with private final fields for each piece of data, getters for each field, a public constructor with a corresponding argument for each field, and `equals`, `hashCode`, and `toString` methods¹. This can be quite tedious and prone to errors.

With the introduction of Record Type in Java 14, you can simplify this process significantly. Here's how you would define the `Employee` record:

```java
public record Employee(Long id, String firstName, String lastName, String email, int age) { }
```

When you create this `Employee` record, the compiler generates the following:

- An all-arguments constructor accepting all fields.
- The `toString()` method that prints the state/values of all fields in the record.
- The `equals()` and `hashCode()` methods using an invokedynamic based mechanism.
- The getter methods whose names are similar to field names without the usual POJO/JavaBean `get` prefix i.e. `id()`, `firstName()`, `lastName()`, `email()`, and `age()`².

This enhancement can save us time during development¹ and improve the reliability of our immutable classes¹.

Here's an example of how you might use the `Employee` record in a real-world scenario:

```java
public class Main {
    public static void main(String[] args) {
        Employee e = new Employee(1L, "John", "Doe", "john.doe@example.com", 30);
        System.out.println("Employee ID: " + e.id());
        System.out.println("Employee Name: " + e.firstName() + " " + e.lastName());
        System.out.println("Employee Email: " + e.email());
        System.out.println("Employee Age: " + e.age());
    }
}
```

In this example, we create an `Employee` record, `e`, and then use the generated getter methods to print out the employee's information. This is a simple example, but it illustrates how records can be used to simplify the handling of immutable data in real-world applications. 
