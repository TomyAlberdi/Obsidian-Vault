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