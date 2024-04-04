Let's explore the concepts of **try-with-resources**, as well as the new features introduced in **Java 7** and **Java 9**, along with code examples.

## Try-With-Resources (Before Java 7)

Before Java 7, managing resources (such as files, sockets, or database connections) in a clean and efficient way required explicit `try-catch-finally` blocks. Developers had to manually close resources in the `finally` block to ensure proper cleanup, even in the presence of exceptions.

Here's an example of how resource management was done before Java 7:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ResourceManagementExample {
    public static void main(String[] args) {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader("sample.txt"));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (reader != null) {
                    reader.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

In this example:
- We open a file using `FileReader` and wrap it with a `BufferedReader`.
- We read lines from the file and print them.
- The `finally` block ensures that the `BufferedReader` is closed, even if an exception occurs.

## New Features in Java 7

### 1. Try-With-Resources

Java 7 introduced the **try-with-resources** statement, which simplifies resource management. Resources declared within the `try` block are automatically closed when the block exits, whether normally or due to an exception.

Here's how the same example looks using try-with-resources:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class TryWithResourcesExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("sample.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this version:
- We declare the `BufferedReader` within the `try` block.
- The resource is automatically closed when the block exits, without the need for an explicit `finally` block.


## New Features in Java 9
However, in Java 9, this limitation is lifted. We can use a reference to a resource that is not declared locally. Here's the same example updated for Java 9:

```java
import java.io.FileNotFoundException;
import java.io.FileOutputStream;

public class TryWithResourcesExample {
    public static void main(String[] args) throws FileNotFoundException {
        // Resource declared outside the try block
        FileOutputStream fileStream = new FileOutputStream("javatpoint.txt");
        try (fileStream) {
            String greeting = "Welcome to javaTpoint.";
            byte[] b = greeting.getBytes();
            fileStream.write(b);
            System.out.println("File written");
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

In this Java 9 code, the resource reference variable `fileStream` is created outside the `try` block, and it works seamlessly within the `try-with-resources` construct. The file is written successfully, and there are no compile errors.



# New Feature SafeVarargs :- explore the **`@SafeVarargs`** annotation in both Java 7 and Java 9, along with code examples to highlight the differences.

## `@SafeVarargs` Annotation

### Overview

The `@SafeVarargs` annotation is used to suppress unsafe operation warnings related to varargs (variable-length argument lists) at compile time. These warnings occur when we invoke a method that has varargs, potentially causing heap pollution.

### Java 7 Example

In Java 7, the `@SafeVarargs` annotation can be applied to **final or static methods** and constructors. It indicates that the method does not perform unsafe operations on its varargs parameter.

Let's consider an example:

```java
import java.util.ArrayList;
import java.util.List;

public class SafeVarargsExample {
    @SafeVarargs
    public final <T> void safePrint(T... elements) {
        for (T element : elements) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        SafeVarargsExample example = new SafeVarargsExample();
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        example.safePrint(names, "David", "Eve");
    }
}
```

In this Java 7 example:
- We define a method called `safePrint` that takes a varargs parameter of type `T`.
- The method is marked with `@SafeVarargs`.
- We use the method to print a list of names along with additional names.

### Java 9 Enhancement

In Java 9, the use of `@SafeVarargs` was extended. Now, apart from final or static methods, we can also apply it to **private methods**. Private methods cannot be overridden, making them safe for varargs.

Here's an example using Java 9:

```java
import java.util.Arrays;

public class SafeVarargsJava9Example {
    @SafeVarargs
    private <T> T sum(T... values) {
        return Arrays.stream(values).reduce(null, (a, b) -> (a == null) ? b : a);
    }

    public static void main(String[] args) {
        SafeVarargsJava9Example example = new SafeVarargsJava9Example();
        Integer result = example.sum(1, 2, 3, 4);
        System.out.println("Sum: " + result);
    }
}
```

In this Java 9 example:
- We define a private method called `sum` that takes varargs of type `T`.
- The method is marked with `@SafeVarargs`.
- We use the method to calculate the sum of integers.

### Conclusion

The `@SafeVarargs` annotation helps ensure safe use of varargs, especially when dealing with generics. It allows us to declare that certain methods will not cause heap pollution. In Java 9, we can also apply it to private methods, further enhancing its utility. 🌟

Certainly! Let's explore the **Java 9 collection factory methods** in detail and highlight the differences from previous approaches. These factory methods provide a concise way to create small unmodifiable collections (such as lists, sets, and maps) with a single line of code.



# Java 9 Collection Factory Methods

### Overview

In Java 9, convenience factory methods were introduced for creating immutable collections. These methods allow you to initialize collections (such as lists and sets) in a concise and readable manner. The resulting collections are unmodifiable, meaning that no elements can be added, removed, or modified after initialization.

### Motivation

Before Java 9, creating small immutable collections was verbose and involved unnecessary code. Let's consider an example using a set:

```java
Set<String> set = new HashSet<>();
set.add("foo");
set.add("bar");
set.add("baz");
set = Collections.unmodifiableSet(set);
```

This approach required multiple lines of code and wasn't intuitive. Additionally, there was no straightforward way to create unmodifiable maps using existing methods.

### Java 9 Factory Methods

Java 9 introduced static factory methods for the following interfaces:

1. **List**: `List.of(...)`
2. **Set**: `Set.of(...)`
3. **Map**: `Map.of(...)`

These methods take the elements as arguments and return an instance of the corresponding collection type. Let's explore each type:

#### 1. List and Set

The signature and characteristics of the factory methods for lists and sets are the same:

- `static <E> List<E> of(E e1, E e2, E e3)`
- `static <E> Set<E> of(E e1, E e2, E e3)`

Usage examples:

```java
List<String> list = List.of("foo", "bar", "baz");
Set<String> set = Set.of("foo", "bar", "baz");
```

As you can see, these methods are simple, short, and concise. You can use them to create lists and sets of specific sizes (in this case, size 3). There are also overloaded versions of these methods for different numbers of elements (from 0 to 10) and a varargs version.

#### 2. Map

For maps, the factory method is:

- `static <K, V> Map<K, V> of(K k1, V v1, K k2, V v2, ...)`

Usage example:

```java
Map<String, Integer> map = Map.of("one", 1, "two", 2, "three", 3);
```

### Summary

Java 9's collection factory methods simplify the creation of small unmodifiable collections. They are concise, intuitive, and eliminate unnecessary code. Remember that the resulting collections are immutable, so any attempt to modify them will throw an `UnsupportedOperationException`. 🌟
