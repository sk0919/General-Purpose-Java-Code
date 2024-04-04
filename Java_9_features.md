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
