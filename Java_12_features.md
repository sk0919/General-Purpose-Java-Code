## Java 12, released in March 2019, introduced several new features, enhancements, and removed or deprecated features. Here are some of the key changes: ##

1. **Switch Expressions (Preview)**: Java 12 introduced a preview of switch expressions that extends the `switch` statement so it can be used as either a statement or an expression¹⁴.

2. **String Class New Methods**: Java 12 added two new methods to the `String` class: `indent` and `transform`¹.

```java
String text = "Hello Baeldung!\\nThis is Java 12 article.";
text = text.indent(4);
System.out.println(text);
text = text.indent(-10);
System.out.println(text);
```

3. **File::mismatch Method**: Java 12 introduced a new `mismatch` method in the `nio.file.Files` utility class. This method is used to compare two files and find the position of the first mismatched byte in their contents¹.

```java
Path filePath1 = Files.createTempFile("file1", ".txt");
Path filePath2 = Files.createTempFile("file2", ".txt");
Files.writeString(filePath1, "Java 12 Article");
Files.writeString(filePath2, "Java 12 Article");
long mismatch = Files.mismatch(filePath1, filePath2);
assertEquals(-1, mismatch);
```

4. **Default CDS Archives**: Class Data Sharing (CDS) archives, which improve startup and footprint, were extended to include the default class list on 64-bit platforms⁴.

5. **Shenandoah**: A new garbage collector, Shenandoah, was added as an experimental feature³⁴.

6. **Microbenchmark Suite**: Java 12 introduced a suite of microbenchmarks to aid in the development of JDK.

Please note that this is not an exhaustive list and there are other changes and enhancements introduced in Java 12.
