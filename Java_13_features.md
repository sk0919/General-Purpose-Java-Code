## Java 13, released in September 2019, introduced several new features, enhancements, and removed or deprecated features. Here are some of the key changes: ##

1. **Switch Expressions (Preview)**: Java 13 built on the switch expressions introduced in JDK 12 by adding a new `yield` statement. This allows values to be effectively returned from a switch expression¹⁴.

```java
@Test
@SuppressWarnings("preview")
public void whenSwitchingOnOperationSquareMe_thenWillReturnSquare()  {
    var me = 4 ;
    var operation = "squareMe" ;
    var result = switch  (operation) {
        case "doubleMe"  -> { yield  me *  2 ;         }
        case "squareMe"  -> { yield  me * me;         }
        default  -> me;
    };
    assertEquals( 16, result);
}
```

2. **Text Blocks (Preview)**: Text blocks were introduced as a preview feature for handling multi-line `String`s such as embedded JSON, XML, HTML, etc.

```java
String TEXT_BLOCK_JSON = """
{
    "name" : "Baeldung",
    "website" : "https://www.baeldung.com"
}""";
```

3. **String Class New Methods**: Java 13 added new methods to handle text blocks¹.

4. **FileSystems.newFileSystem Method**: A new method `FileSystems.newFileSystem(Path, Map<String, ?>)` was added to `java.nio`.

5. **New Official Japanese Era Name**: A new official Japanese era name was added to `java.time`.

6. **Support for MS Cryptography Next Generation (CNG)**: Support for MS Cryptography Next Generation (CNG) was added to `javax.crypto`.

Please note that this is not an exhaustive list and there are other changes and enhancements introduced in Java 13.

#  #

## A. Switch Expressions (Preview)  ##
Sure, I can explain this with an example. In Java 13, the switch expression was enhanced with the introduction of the `yield` keyword. This allows values to be returned from a switch block, making it an expression that can be assigned to a variable. Here's an example:

```java
public class Main {
    public static void main(String[] args) {
        String day = "MONDAY";
        String typeOfDay = switch (day) {
            case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> {
                yield "Weekday";
            }
            case "SATURDAY", "SUNDAY" -> {
                yield "Weekend";
            }
            default -> {
                yield "Invalid day";
            }
        };
        System.out.println(typeOfDay);  // Outputs "Weekday"
    }
}
```

In this example, the `switch` expression is used to determine whether a day is a weekday or a weekend. The `yield` keyword is used to return a value from each case block. The returned value is then assigned to the `typeOfDay` variable. This makes the code more concise and easier to read compared to traditional switch statements. Note that this feature is a preview language feature in Java 13 and needs to be enabled explicitly when compiling the code. 

Please note that the `yield` keyword was introduced as a preview feature in Java 12 and was finalized in Java 13. It's always a good practice to use the latest stable version of Java to leverage all the finalized features and improvements.


## B. Text Blocks (Preview) ##
Sure, I can explain this with an example. In Java 13, Text Blocks were introduced as a preview feature to handle multi-line Strings. This is particularly useful when dealing with embedded JSON, XML, HTML, etc. Here's an example:

```java
public class Main {
    public static void main(String[] args) {
        String json = """
            {
                "name": "John Doe",
                "email": "john.doe@example.com",
                "roles": [
                    "User",
                    "Admin"
                ]
            }
            """;
        System.out.println(json);
    }
}
```

In this example, the `"""` (triple double-quote) syntax is used to start and end a text block, allowing for easy insertion of multi-line Strings. This makes the code more readable and easier to manage compared to traditional string concatenation or using escape sequences for special characters.

Please note that this feature was introduced as a preview feature in Java 13 and needs to be enabled explicitly when compiling the code. It's always a good practice to use the latest stable version of Java to leverage all the finalized features and improvements.


## C. String Class New Methods & FileSystems.newFileSystem Method ##

1. **String Class New Methods**: Java 13 introduced a few new methods in the `String` class. Here's an example of using the `stripIndent` and `translateEscapes` methods:

```java
public class Main {
    public static void main(String[] args) {
        String str = """
            Hello,
                World!
            """;
        System.out.println(str.stripIndent().translateEscapes());
    }
}
```

In this example, the `stripIndent` method removes incidental white space from the beginning of each line in a text block. The `translateEscapes` method processes escape sequences denoted by the backslash character (`\`).

2. **FileSystems.newFileSystem Method**: This method is used to create a new file system that is identified by a URI. Here's an example:

```java
import java.net.URI;
import java.nio.file.FileSystems;
import java.nio.file.Path;
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) throws Exception {
        Map<String, ?> env = new HashMap<>();
        URI uri = URI.create("jar:file:/path/to/my.jar");
        try (var fs = FileSystems.newFileSystem(uri, env)) {
            Path path = fs.getPath("/path/in/jar");
            // Use the path...
        }
    }
}
```

In this example, a new file system is created for a JAR file. The `newFileSystem` method takes a URI that identifies the file system and a map of environment variables. The file system is closed automatically at the end of the try-with-resources block.

Please note that these features were introduced in Java 13 and need to be enabled explicitly when compiling the code. It's always a good practice to use the latest stable version of Java to leverage all the finalized features and improvements.
