## Java 11, released in September 2018, introduced several new features, enhancements, and removed or deprecated features. Here are some of the key changes: ##

1. **New String Methods**: Java 11 added new methods to the `String` class: `isBlank`, `lines`, `strip`, `stripLeading`, `stripTrailing`, and `repeat`¹.

```java
String multilineString = "Baeldung helps \\n \\n developers \\n explore Java.";
List<String> lines = multilineString.lines()
    .filter(line -> !line.isBlank())
    .map(String::strip)
    .collect(Collectors.toList());
```

2. **New File Methods**: It's now easier to read and write `String`s from files using the new `readString` and `writeString` static methods from the `Files` class¹.

```java
Path filePath = Files.writeString(Files.createTempFile(tempDir, "demo", ".txt"), "Sample text");
String fileContent = Files.readString(filePath);
```

3. **Collection to an Array**: The `java.util.Collection` interface contains a new default `toArray` method which takes an `IntFunction` argument¹.

4. **New ChaCha20 and ChaCha20-Poly1305 Cipher Implementations**: These replace the insecure RC4 stream cipher.

5. **Support for Cryptographic Key Agreement with Curve25519 and Curve448**: These replace the existing ECDH scheme.

6. **Removal of Certain Features**: The deployment stack, required for Applets and Web Start Applications, was deprecated in JDK 9 and has been removed in JDK 11².

7. **Oracle vs OpenJDK**: Starting with Java 11, there’s no free long-term support (LTS) from Oracle. However, Oracle continues to provide OpenJDK releases, which we can download and use without charge¹.

Please note that this is not an exhaustive list and there are other changes and enhancements introduced in Java 11.




#                                      Detail Explanation with code                                 # 

## A. String new features ##
Sure, let's go through these new methods added to the `String` class in Java 11:

1. **isBlank()**: This method checks whether the string is blank or not. It returns `true` if the string is empty or contains only white space characters, otherwise `false`. Here's an example:

```java
public class Main {
    public static void main(String[] args){
        String str = "Studytonight";
        boolean r = str.isBlank();
        System.out.println(r); // prints false

        str = "";
        r = str.isBlank();
        System.out.println(r); // prints true
    }
}
```

2. **lines()**: This method returns a stream of lines extracted from the string, separated by line terminators. Here's an example:

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args){
        String str = "Studytonight \\n is a \\r technical \\n portal";
        Stream<String> lines = str.lines();
        lines.forEach(System.out::println); // prints "Studytonight", "is a", "technical portal"
    }
}
```

3. **strip()**, **stripLeading()**, and **stripTrailing()**: These methods are used to remove all the leading and trailing spaces from a string. The `strip()` method removes spaces from both ends, `stripLeading()` removes leading spaces, and `stripTrailing()` removes trailing spaces. Here's an example:

```java
public class Main {
    public static void main(String[] args){
        String str = "      Studytonight portal ";
        System.out.println(str); // prints "      Studytonight portal "
        String str2 = str.strip();
        System.out.println(str2); // prints "Studytonight portal"
    }
}
```

4. **repeat(int count)**: This method repeats the `String` as many times as provided by the `count` parameter¹.

These methods can reduce the amount of boilerplate involved in manipulating string objects, and save us from having to import libraries¹. In the case of the `strip` methods, they provide similar functionality to the more familiar `trim` method; however, with finer control and Unicode support.


