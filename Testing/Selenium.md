Created: 2024-10-02 18:39
## Family Tree:
1. Computer
2. [[Testing/Testing|Testing]]
-- -
Selenium is an open-source tool for automating web browser testing. It provides the ability to record and/or replay, edit, and debug test cases that can be executed repeatedly when needed. Selenium offers three products, each with different purposes.
## Selenium IDE
This component is an automation tool that allows us to record, edit, and debug tests without the need for a programming language. It is also known as **Selenium Recorder**.  
The recorded flows are contained within a script that can be edited and parameterized to adapt to different cases. Most importantly, its execution can be repeated as many times as desired.  
Its main goal is to automate repetitive functional tests, making the tester's job easier, and it is also useful for regression testing.  
It allows referencing objects in the DOM based on **ID, CSS, name**, or through **XPath**. Additionally, actions can be executed step by step.
## Selenium WebDriver
This tool allows the automation of UI (user interface) tests for web applications. Some of the languages supported by Selenium WebDriver include **Java, C#, Python, Ruby, PHP,** and **JavaScript**.
Selenium WebDriver is one of the most important frameworks used for generating automated tests. It is a suite of tools for web browser automation that leverages the best available techniques to control browser instances and emulate user interactions with the browser.
It allows users to simulate interactions performed by end-users, such as entering text into fields, selecting values from dropdown menus, checking checkboxes, and more. Additionally, it also enables validations on the behavior of any component. This helps verify the expected behavior detailed in the test cases that are designed and ready to be automated.
WebDriver uses the browser automation APIs provided by browser developers to control and execute tests. This is similar to how a real user would manipulate the browser, with the main difference being the speed of execution—WebDriver is significantly faster than manual execution.
Selenium supports many programming languages such as **Java, C#, Python**, etc., and is compatible with multiple browsers such as **Google Chrome, Firefox, Internet Explorer**, among others.
Selenium WebDriver operates within three main components:
1. **The tests** to be executed (written in a language of choice, like Java, C#, Node.js, etc.).
2. A **standalone server** where the test cases will be executed.
3. A **browser driver** that connects the scripts generated by the Client API to the browser through Selenium Server.
Graphically, it can be represented as follows:
![[Testing/attachments/image.png]]
## Selenium Grid
This tool allows designing automated tests for web applications across various platforms. It also enables the execution of tests on multiple servers in parallel, which reduces execution time and cost, as the tests can be run on various browsers and operating systems. Selenium Grid consists of two components: **Selenium Hub** and **Remote Control**.