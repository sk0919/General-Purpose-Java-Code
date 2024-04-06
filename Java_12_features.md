## Java 12, released in March 2019, introduced several new features, enhancements, and removed or deprecated features. Here are some of the key changes: ##

1. **Switch Expressions (Preview)**: Java 12 introduced a preview of switch expressions that extends the `switch` statement so it can be used as either a statement or an expression.

2. **String Class New Methods**: Java 12 added two new methods to the `String` class: `indent` and `transform`¹.

```java
String text = "Hello Baeldung!\\nThis is Java 12 article.";
text = text.indent(4);
System.out.println(text);
text = text.indent(-10);
System.out.println(text);
```

3. **File::mismatch Method**: Java 12 introduced a new `mismatch` method in the `nio.file.Files` utility class. This method is used to compare two files and find the position of the first mismatched byte in their contents.

```java
Path filePath1 = Files.createTempFile("file1", ".txt");
Path filePath2 = Files.createTempFile("file2", ".txt");
Files.writeString(filePath1, "Java 12 Article");
Files.writeString(filePath2, "Java 12 Article");
long mismatch = Files.mismatch(filePath1, filePath2);
assertEquals(-1, mismatch);
```

4. **Default CDS Archives**: Class Data Sharing (CDS) archives, which improve startup and footprint, were extended to include the default class list on 64-bit platforms⁴.

5. **Shenandoah**: A new garbage collector, Shenandoah, was added as an experimental feature.

6. **Microbenchmark Suite**: Java 12 introduced a suite of microbenchmarks to aid in the development of JDK.

Please note that this is not an exhaustive list and there are other changes and enhancements introduced in Java 12.


# #
## A. Switch Expressions (Preview) ##
Sure, I can explain this. 

Java 12 introduced an enhanced version of the `switch` statement, known as `switch` expressions. This feature was in preview in Java 12 and became a standard feature in Java 14.

The traditional `switch` statement works as a multi-way branch statement. It's a statement, meaning it does not return a value. Here's an example:

```java
int num = 2;
switch (num) {
    case 1:
        System.out.println("One");
        break;
    case 2:
        System.out.println("Two");
        break;
    default:
        System.out.println("Invalid number");
}
```

In contrast, a `switch` expression is both a statement and an expression. It returns a value, and you can use it in statements. Here's how you can use `switch` expressions:

```java
int num = 2;
String numericString = switch (num) {
    case 1 -> "One";
    case 2 -> "Two";
    default -> "Invalid number";
};
System.out.println(numericString);
```

In this example, the `switch` expression evaluates the `num` variable. The arrow (`->`) separates the case label from the expression that is returned if that case is matched. The result of the `switch` expression is then assigned to the `numericString` variable.

This feature simplifies the `switch` statement and makes it more flexible. It also helps prevent common errors, such as forgetting the `break` statement in a `switch` block. The `switch` expression automatically breaks after the first match. 

Remember, this feature was in preview in Java 12, so you need to enable it explicitly in the compiler by using the `--enable-preview` flag. It became a standard feature in Java 14.
