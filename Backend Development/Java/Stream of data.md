Created: 2024-09-26 19:28
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
In Java, as in other languages, data input and output from and to a program are handled as a **stream** of data. These can be either input or output streams. To determine the "direction" of the stream, the perspective is taken from the code that is being executed: an output stream takes data and "sends" it out to the platform, writing to a disk, sending over a network, etc. An input stream, on the other hand, receives data from the platform that "comes in," reading from a disk, a device, etc.
## Reading and Writing
Input and output streams are used to read and write data to and from the platform. In Java, there are a set of basic classes for reading and writing binary data. Additionally, there are other classes designed for reading and writing characters. Furthermore, there are additional classes that specify these behaviors to further simplify reading and writing operations.
Let’s look at the basic stream hierarchy in Java, which is made up of **InputStream** (Input) and **OutputStream** (Output) with their basic operations.
### Reading:
![[Backend Development/Java/attachments/image.png]]
The basic operation for input streams is the `read()` method.  
Each byte read returns an integer value. Using an integer, 257 values can be returned (0 to 256), and an additional `-1` is returned when there is nothing left to read.
### Writing:
![[Backend Development/Java/attachments/image 1.png]]
The basic operation for output streams is the `write()` method.  
It is possible to pass a byte directly.
## Buffers
In Java, all input and output streams can operate in two ways: **byte-by-byte** or in **batches**. For example, if you need to read a file of 1024 bytes, you can either read one byte 1024 times or read in batches, such as 8 times with 128 bytes per batch. To handle this, both binary and character streams have **Buffered** subclasses. These classes provide methods that allow you to choose the size of the batches for reading or writing—if no size is specified, they set a default size.
Choosing between a **buffered** or **non-buffered** stream depends on the application. While buffering speeds up read operations, it consumes more memory—each batch read is stored in memory until processed (e.g., writing it elsewhere). On the other hand, not using buffers consumes less memory but requires a system or platform call for each byte read, which increases CPU usage.
That said, using **buffered streams** has some advantages for developers. For example, `BufferedInputStream` allows reading blocks of bytes, making it easier to read a file. Otherwise, you would need to read character by character and detect line breaks manually.
### Reading:
To read the contents of a file, we need to instantiate a `FileInputStream` object and pass it as a parameter to the constructor of a `BufferedInputStream` object. Then, we will read the content using `read()` until the end of the file is reached (`-1`).
```java
import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class PruebaLeerArchivo {
    public static void main(String[] args) throws FileNotFoundException {
        FileInputStream fi = new FileInputStream("InputFile.txt");
        BufferedInputStream bi = new BufferedInputStream(fi);
        try {
            int i;
            while ((i = bi.read()) != -1) {
                System.out.print((char) i);
            }
            bi.close();
            fi.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
#### Methods of `BufferedInputStream`:

| Method                                       | Description                                                                                             |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `int available()`                            | Returns the estimated number of bytes available to read.                                                |
| `void close()`                               | Closes the `BufferedInputStream`.                                                                       |
| `void mark(int readLimit)`                   | Marks the current position to read the stream again later.                                              |
| `boolean markSupported()`                    | Checks if the stream supports `mark()` and `reset()` methods.                                           |
| `int read()`                                 | Reads a byte of data from the input stream.                                                             |
| `int read()`                                 | Reads the specified byte from the input array.                                                          |
| `int read(byte[] b, int off, int len)`       | Read bytes from the input array starting from the given offset.                                         |
| `byte[] readAllBytes()`                      | Reads all the remaining bytes from the input stream.                                                    |
| `byte[] readNBytes(int len)`                 | Reads up to the specified number of bytes.                                                              |
| `int readNBytes(byte[] b, int off, int len)` | Reads the specified number of bytes into the array starting from the offset.                            |
| `long skip(long n)`                          | Skips or discards the specified number of bytes during reading.                                         |
| `void skipNBytes(long n)`                    | Skips or discards up to the specified number of bytes during reading.                                   |
| `long transferTo(OutputStream out)`          | Reads all bytes from the input stream and writes them to the specified output stream in the same order. |

### Writing:
To write content to a file, we need to instantiate a `FileOutputStream` object and pass it as a parameter to the constructor of a `BufferedOutputStream` object. Then, we will write the desired content using `write()`, in this case, a byte.
```java
import java.io.BufferedOutputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class WriteBufferedFile {
    public static void main(String[] args) throws FileNotFoundException {
        FileOutputStream fo = new FileOutputStream("OutputFile.txt");
        BufferedOutputStream bo = new BufferedOutputStream(fo);
        byte b = 65;
        try {
            bo.write(b);
            System.out.println("The byte was written successfully");
            bo.close();
            fo.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
#### Methods of `BufferedOutputStream`:

| Method                                   | Description                                                                          |
| ---------------------------------------- | ------------------------------------------------------------------------------------ |
| `void close()`                           | Closes the output stream and releases all resources.                                 |
| `void flush()`                           | Flushes the `BufferedOutputStream`, writing any remaining data to the output stream. |
| `void write(byte[] b)`                   | Writes `b.length` bytes to the output stream.                                        |
| `void write(int byte)`                   | Writes the specified byte to the output stream.                                      |
| `void write(byte[] b, int off, int len)` | Writes the specified number of bytes from the array, starting at the offset.         |
| `OutputStream nullOutputStream()`        | Returns a new output stream that discards all bytes.                                 |
