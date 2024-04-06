## Java 10, an implementation of Java Standard Edition 10, was released on March 20, 2018. Here are the major new features introduced in Java 10: ##

1. **Local Variable Type Inference (JEP 286)** : This feature introduces the `var` keyword, which allows you to declare a local variable without specifying its type. The type of the variable will be inferred from the type of the actual object created².

2. **Unmodifiable Collections** : There are a couple of changes related to unmodifiable collections in Java 10. The `java.util.List`, `java.util.Map`, and `java.util.Set` each got a new static method `copyOf(Collection)`. It returns the unmodifiable copy of the given Collection¹. Also, `java.util.stream.Collectors` get additional methods to collect a Stream into unmodifiable List, Map, or Set¹.

3. **Optional*.orElseThrow()** : The `java.util.Optional`, `java.util.OptionalDouble`, `java.util.OptionalInt`, and `java.util.OptionalLong` each got a new method `orElseThrow()` which doesn’t take any argument and throws NoSuchElementException if no value is present¹.

4. **Performance Improvements** : There were several performance improvements made in Java 10¹.

5. **Container Awareness**¹: JVMs are now aware of being run in a Docker container and will extract container-specific configuration instead of querying the operating system itself¹.

6. **Garbage-Collector Interface (JEP 304)**²: This is a clean interface within the JVM source code to allow alternative collectors to be quickly and easily integrated².

7. **Parallel Full GC for G1 (JEP 307)**²: The G1 garbage collector is designed to avoid full collections, but when the concurrent collections can’t reclaim memory fast enough, a fall back full GC will occur².

8. **Heap Allocation on Alternative Memory Devices (JEP 316)** : This feature provides a way for the HotSpot VM to allocate the Java object heap on an alternative memory device, specified by the user².

9. **Time-Based Release Versioning (JEP 322)** : Starting from Java 10, Oracle has adapted time-based version-string scheme².

Please note that this is a high-level overview. For more detailed information, you may want to refer to the official Java 10 documentation or other resources..


#  New Features with code and explanation #

## A. Local Variable Type Inference, introduced in Java 10 as part of JEP 286, is a feature that simplifies the declaration of local variables in Java. It introduces the `var` keyword, which allows you to declare a local variable without specifying its type. The Java compiler will automatically infer the type of the variable from the type of the initializer expression.

Here's an example to illustrate this:

```java
// Before Java 10
String str = "Hello, World!";
List<Integer> list = new ArrayList<>();

// With Java 10 and the var keyword
var str = "Hello, World!";
var list = new ArrayList<Integer>();
```

In the above example, `str` is inferred to be of type `String`, and `list` is inferred to be of type `ArrayList<Integer>`. This feature can make your code cleaner and easier to read, especially when dealing with complex types. However, it's important to note that `var` can only be used when the initializer expression is present; the compiler needs it to determine the variable's type.

Also, `var` is only applicable to local variables (those declared inside methods, constructors, or initializers), and cannot be used for fields, method parameters, or return types. It's also not applicable to variables without initializers or with `null` initializers. For example, the following declarations are invalid:

```java
var nothing; // Invalid - no initializer
var nully = null; // Invalid - initializer is null
```

This feature does not change the statically typed nature of Java; it simply allows the compiler to infer the type information. The inferred type is the type of the variable throughout its scope, and it cannot be changed. For example, if a variable is inferred to be `String`, you cannot assign an `Integer` to it later in the code. It's also worth noting that `var` is not a keyword, but a reserved type name. This means it can still be used as a variable, method, or package name. However, it's generally recommended to avoid such usage to prevent confusion. 


## B. Unmodifiable Collections, introduced in Java 10, are a feature that enhances the immutability of collections in Java. This feature introduces new methods that allow you to create unmodifiable copies of collections and collect streams into unmodifiable collections.

Here's an example to illustrate this:

```java
import java.util.*;
import java.util.stream.*;

// Creating a modifiable list
List<String> modifiableList = new ArrayList<>();
modifiableList.add("Hello");
modifiableList.add("World");

// Creating an unmodifiable copy of the list using copyOf method
List<String> unmodifiableList = List.copyOf(modifiableList);
System.out.println(unmodifiableList); // prints [Hello, World]

// Attempting to modify the unmodifiable list
try {
    unmodifiableList.add("!");
} catch (UnsupportedOperationException e) {
    System.out.println("Cannot modify an unmodifiable collection");
}

// Collecting a stream into an unmodifiable list
Stream<String> stream = Stream.of("Hello", "World");
List<String> listFromStream = stream.collect(Collectors.toUnmodifiableList());
System.out.println(listFromStream); // prints [Hello, World]
```

In the above example, `List.copyOf` creates an unmodifiable copy of `modifiableList`, and `Collectors.toUnmodifiableList` collects a stream into an unmodifiable list. If you try to modify these unmodifiable collections (like adding an element), it will throw an `UnsupportedOperationException`.

This feature is also available for `Set` and `Map` interfaces with `Set.copyOf`, `Map.copyOf`, `Collectors.toUnmodifiableSet`, and `Collectors.toUnmodifiableMap`.

These enhancements make it easier to create unmodifiable collections, which are safer because they can't be changed once they're created. This can be particularly useful in multi-threaded environments where you want to ensure that a collection isn't modified by another thread after it's created.


## C. The `orElseThrow()` method was introduced in Java 10 for the `Optional`, `OptionalDouble`, `OptionalInt`, and `OptionalLong` classes. This method doesn't take any arguments and throws a `NoSuchElementException` if no value is present. ##

Here's an example to illustrate this:

```java
import java.util.*;

// Creating an Optional with a value
Optional<String> optionalWithValue = Optional.of("Hello, World!");

// Using orElseThrow when a value is present
try {
    String value = optionalWithValue.orElseThrow();
    System.out.println(value); // prints "Hello, World!"
} catch (NoSuchElementException e) {
    System.out.println("No value present");
}

// Creating an Optional without a value
Optional<String> optionalWithoutValue = Optional.empty();

// Using orElseThrow when no value is present
try {
    String value = optionalWithoutValue.orElseThrow();
    System.out.println(value);
} catch (NoSuchElementException e) {
    System.out.println("No value present"); // prints "No value present"
}
```

In the above example, `orElseThrow` returns the value when one is present in `optionalWithValue`, but throws a `NoSuchElementException` when no value is present in `optionalWithoutValue`.

This method provides a more expressive and efficient way to handle `Optional` values compared to using `isPresent()` and `get()`. It makes it clear that an exception will be thrown if no value is present, and it avoids the potential inefficiency of creating a new exception object as an argument to `orElseThrow()`, which was the previous way to achieve this behavior.
