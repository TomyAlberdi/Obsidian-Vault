JUnit is the most widely used open-source [[testing]] [[Frameworks|framework]] for [[Java]]. It allows developers to write and run automated tests and is supported by all major [[IDEs]], build tools, and frameworks like Spring.
## Configuration
To set up the **JUnit** library in your development environment, follow these steps:

1. **Select the Class to Test**:  
    Stand on the class you want to test, then press `Alt + Enter` (or the equivalent shortcut in your IDE).
2. **Create Test**:  
    From the options that appear, select **Create Test**.
3. **Add JUnit Library**:  
    The IDE will guide you automatically to add the JUnit library to your project. Follow the prompts.
4. **Download JUnit**:  
    Click the **OK** button to download the JUnit library to the recommended path specified by the IDE.
5. **Add JUnit to Classpath**:  
    The final step is to add the library to the **classpath**. The IDE typically provides a recommendation or guide on how to do this. You simply need to follow the instructions to include the JUnit package in your classpath.
## Parametrized Testing
In tests, we often perform multiple checks for different cases, which can lead to repetitive code. For example:
```java
import org.junit.Assert;
import org.junit.Test;

public class MultiplicarTest {
   @Test
   public void debemosCorroborarMultiplicaciones() {
       Assert.assertEquals(4, 2*2);
       Assert.assertEquals(6, 3*2);
       Assert.assertEquals(5, 5*1);
       Assert.assertEquals(10, 5*2);
   }
}
```
To avoid repetition, JUnit offers **parameterized tests** using a custom runner called `Parameterized` This allows us to define parameters for multiple executions of a single test:
```java
import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;

import java.util.Arrays;

@RunWith(Parameterized.class)
public class MultiplicarTest {
   @Parameterized.Parameters
   public static Iterable<Object[]> data() {
       return Arrays.asList(new Object[][] {
           {4, 2, 2}, {6, 3, 2}, {5, 5, 1}, {10, 5, 2}
       });
   }

   private int multiplierOne;
   private int expected;
   private int multiplierTwo;

   public MultiplicarTest(int expected, int multiplierOne, int multiplierTwo) {
       this.multiplierOne = multiplierOne;
       this.expected = expected;
       this.multiplierTwo = multiplierTwo;
   }

   @Test
   public void debeMultiplicarElResultado() {
       Assert.assertEquals(expected, multiplierOne * multiplierTwo);
   }
}
```
### Key Concepts:
- **@RunWith(Parameterized.class)**: Indicates that we are using the `Parameterized` runner, which will run the test multiple times, based on the number of parameter sets.
- **@Parameters**: Defines the method that returns the collection of parameters to be used by the runner. Each test iteration is initialized with different parameters from this set.
- **Constructor**: A constructor is required to initialize the test class with the parameters defined in each element of the collection.
## Test Suite
A **JUnit Test Suite** allows grouping and executing multiple tests together. Test suites can be created using the following annotations:
- **@RunWith(Suite.class)**: Specifies that a suite of tests will be run.
- **@SuiteClasses**: Defines the test classes to be included in the suite.
```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

import com.TestFeaturePrimero;
import com.TestFeatureSegundo;

@RunWith(Suite.class)
@SuiteClasses({ TestFeaturePrimero.class, TestFeatureSegundo.class })
public class TestFeatureSuite {
   // This class remains empty, it is used only as a holder for the above annotations
}
```
This way, you can run multiple test classes together as part of a suite, which is useful for organizing tests into logical groups.