Created: 2024-09-28 00:16
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
To allow a Java program to convert an object, alongs with all its attributes, into a stream of bytes and later recover it, the object needs to be **serializable**. By converting the object to bytes, it can be, for example, sent over the network or saved to a file and later reconstructed on the other side or read from the file.
To make an object serializable, it simply need to implement the `Serializable` interface. Since this interface doesn't have any methods, it's straightforward to implement -just write `implements Serializable`.
For example, the following `Person` class is serializable, and Java ill be able to send an object of type `Person` over the network, write it to a file, our reconstruct it from a file.
```java
import java.io.*;

public class Persona implements Serializable {
    private String nombre;
    private String apellido;
    private int DNI;
}
```
If within a class we want to serialize attributes that are instances of other classes, those classes must also be serializable. For example, Java's `ArrayList` class is serializable.
## `ObjectOutputStream` and `ObjectInputStream`
To convert an object into an array of bytes, we use the `ObjectOutputStream` class, and to reconstruct an object from an array of bytes, we use the `ObjectInputStream` class. Below is a Java example of how to save an object to a file and then retrieve it.
```java
import java.io.*;

public class Prueba {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // Create a sample object
        Persona persona = new Persona();
        persona.nombre = "John";
        persona.apellido = "Doe";
        persona.DNI = 12345678;

        /* Save the object to a file */
        FileOutputStream fo = new FileOutputStream("OutputFile.txt");
        ObjectOutputStream oos = new ObjectOutputStream(fo);
        oos.writeObject(persona);
        oos.close(); // Always close the stream

        /* Retrieve the object from the file */
        FileInputStream fi = new FileInputStream("OutputFile.txt");
        ObjectInputStream ois = new ObjectInputStream(fi);
        Persona retrievedPersona = (Persona) ois.readObject(); // Cast back to Persona

        System.out.println("Nombre: " + retrievedPersona.nombre);
        System.out.println("Apellido: " + retrievedPersona.apellido);
        System.out.println("DNI: " + retrievedPersona.DNI);
        
        ois.close(); // Close input stream
    }
}
```