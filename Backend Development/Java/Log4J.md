Created: 2024-09-26 18:09
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
Log4j is a Java library developed by the Apache Software Foundation that allows developers to choose the output and level of granularity for messages or logs at runtime. In other words, it is used to generate logging messages in a clean and simple way, allowing them to be filtered by importance and enabling the output to be configured for the console, files, or other destinations.
## Advantages and disadvantages:

- **Advantage**: Provides a record of what is happening in our systems, allowing us to better understand errors.
- **Disadvantage**: Log files can sometimes become very large and take up a lot of space. This is why it's important to carefully choose what kind of information you want to store.
## Architechture:
The Log4j API follows a layered architecture where each layer provides different objects to perform various tasks. This structure makes the design flexible and easy to extend in the future.
The two types of objects available in the Log4j framework are:
- **Core objects**: Mandatory framework objects required to use the framework.
- **Support objects**: Optional framework objects that support core objects in performing additional tasks.
### Core Objects:
The core objects include the following types:
- **Logger object**
- **Appender object**
- **Layout object**
### Support Objects:
- **Level object**
- **LogManager**
- **Filter object**
- **Object renderer**
### Logging Levels:
Log4j has default priority levels for messages. These include:
- **OFF**: This is the minimum detail level and disables all logging.
- **FATAL**: Used for critical system messages. Generally, after logging the message, the program shuts down.
- **ERROR**: Indicates error events that might still allow the application to continue running.
- **WARN**: Used for warning messages about events.
- **INFO**: Refers to informational messages that highlight the progress of the application at a general level.
- **DEBUG**: Designates detailed informative events most useful for debugging an application.
- **TRACE**: Used to show messages with a higher level of detail than debug.
- **ALL**: The highest level of detail, enabling all logs.
## Configuration
To enable logging in Log4j, we need to add a configuration file. We'll place this file in the root directory of the project, meaning the main folder. For example, if our project is named `app`, we create a configuration file called `log4j.properties` in that folder with the following content:
### Configuration example:
#### Set the minimum logging level and appenders:
In the first line, we define the minimum logging level and the appenders we will use. In this case, we set the logging level to `DEBUG` and create two appenders: `stdout` (for console logging) and `file` (for file logging).
```properties
log4j.rootLogger=DEBUG, stdout, file
```
#### Configure the logging level for warnings:
The second line configures the level at which warnings will start to appear both in the console and in the file.
```properties
log4j.logger.infoLogger=DEBUG
```
#### Prevent appenders from inheriting parent configurations:
The third line prevents appenders from inheriting the configuration of their parent appenders (if any). In our case, there are no parent appenders, so it's not an issue.
```properties
log4j.additivity.infoLogger = false
```
### Console logging configuration:
#### Specify the logger type:
In the first line, we indicate the type of logger by referencing the class that will print the messages.
```properties
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
```
#### Set the out to the console:
The second line tells Log4j to print the logs directly to the console.
```properties
log4j.appender.stdout.Target=System.out
```
#### Set the message format:
The last two lines define the pattern for how each log message will be displayed. You can check all possible configuration options in Oracle's documentation.
```properties
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=[%d{yyyy-MM-dd HH:mm:ss}] [ %-5p] [%c{1}:%L] %m%n
```
### File logging configuration:
#### Configure the appender to write to a file:
The first line sets the logger type to `RollingFileAppender`, which means it will create new files when certain conditions (like file size) are met.
```properties
log4j.appender.file=org.apache.log4j.RollingFileAppender
```
#### Set the log file name:
The second line specifies the name (and path) of the log file.
```properties
log4j.appender.file.File=avisos.log
```
#### Set maximum file size and backup index:
- `MaxFileSize` defines the maximum size of each log file.
- `MaxBackupIndex` indicates how many log files will be kept. Once the limit is reached, the oldest files will be overwritten.
```properties
log4j.appender.file.MaxFileSize=5MB
log4j.appender.file.MaxBackupIndex=3
```
#### Set the message format for file logging:
Similar to console logging, we configure the pattern for how messages will be stored in the log file.
```properties
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%d{yyyy-MM-dd HH:mm:ss}] [ %-5p] [%c{1}:%L] %m%n
```
## Example
In the following example, we will see how to instantiate a `logger` object that allows us to log messages at different priority levels. The most commonly used levels are `error`, `warn`, `debug`, and `info`.
```java
import org.apache.log4j.Logger;

public class TestLog {
   // Instantiate a logger for the class
   private static final Logger logger = Logger.getLogger(TestLog.class);

   public static void main(String[] args) {
     // Log an info message
     logger.info("Starting our MAIN method");

     try {
        String variable = "Hello";
        // This will throw an exception (division by zero)
        int division = 1 / 0;
     } catch (Exception e) {
        // Log an error with the exception details
        logger.error("Error due to division by zero", e);
     }

     // Log a warning message
     logger.warn("Warning: MAIN method is about to end");

     // Log a debug message (will show only if logger is set to DEBUG level)
     logger.debug("This will show only if the logger is in DEBUG mode");

     // Log another info message
     logger.info("Ending the MAIN thread");
  }
}
```
- **`logger.info`**: Logs informational messages that highlight the progress of the application.
- **`logger.error`**: Logs error messages, typically when an exception occurs. In this case, we log the division-by-zero error.
- **`logger.warn`**: Logs warning messages to indicate potential issues.
- **`logger.debug`**: Logs detailed debug information, typically useful for developers to troubleshoot issues. This will only appear if the logger is set to `DEBUG` level in the configuration.
When you run this program, depending on the logging level configured in `log4j.properties`, you will see the appropriate log messages in the console or log file.