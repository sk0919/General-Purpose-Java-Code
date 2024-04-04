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
