## Introduction to the Linux Terminal
### The Console:
The **Command Line Interface** (CLI) is a method of communication between the user and the machine that accepts user instructions through text lines, following specific syntax rules that the operating system can interpret. The tool that enables this user interface function is called a **shell**. In the context of the CLI, this would be referred to as a **CLI shell** or **command interpreter**.
### Different types of Shells:
In Linux, there are numerous different shells or interpreters. The most well-known is likely **[[Bash]]**, as it usually comes by default in most GNU/Linux distributions. However, there are other notable shells such as **Bourne Shell** (`sh`), **Korn Shell** (`ksh`), or **C Shell** (`csh`), which we will explore.
- **Bourne Shell:** Named after its creator at Bell Labs, Steve Bourne, this was the first shell used for the Unix operating system and has surpassed the functionality of many newer shells. All versions of Linux and Unix allow users to switch to the original Bourne Shell, known simply as "sh." However, it lacks some features like file name completion and command history, which were added by later shells.
- **C/TC Shell:** Developed after the Bourne Shell, the **C Shell** was designed to facilitate system control for programmers in the C language, with a syntax very similar to C. Popularly known as **`csh`**, it is present in other operating systems like macOS. Its evolution, **`tcsh`**, incorporates advanced features and more keyboard shortcuts.
- **Korn Shell:** Written by David Korn at Bell Labs, this shell aims to combine the features of C Shell, TC Shell, and Bourne Shell in a single package. It also allows developers to create new shell commands as needed. It has advanced features for handling command files, comparable to specialized programming languages like AWK and Perl.
- **Bourne-Again Shell (BASH):** **Bash** is an updated version of the original Bourne Shell and is widely used in the open-source community. Its syntax is similar to that of the Bourne Shell but includes more advanced features from the C, TC, and Korn shells. Bash adds capabilities like file name completion by pressing TAB, command history recall, and the ability to run multiple programs in the background simultaneously.
### Running the Console:
- **Execution at Startup:** Each Linux distribution has its own way of accessing the console, but when the OS starts at run levels 1, 2, 3, or 4, it will default to the console.
- **Execution from GUI:** If the OS starts at level 5 (with a graphical user interface), we have several options to use the terminal, depending on the installed distribution. For example, in **Ubuntu**, there are two main methods:
    - Launching a **TTY** (a workspace without a graphical environment). Up to 7 terminals can run this way. Terminals 1 through 6 lack a graphical interface. To switch TTYs in Linux, use the keyboard shortcut **Control + Alt + F1 to F7** for the desired TTY.
    - Finding a dedicated terminal app running in a window, accessible from the applications panel of the distribution. In Ubuntu, for instance, this terminal can be found within the **GNOME** graphical environment's application drawer.
### Privilege Elevation:
Operating systems typically use a single user with administrator permissions. In Linux, however, the **root** account, which separates regular users from the superuser, handles this. The root account has full privileges to perform actions on the system. Some commands require root access, which involves entering the root password. However, users must be cautious, as incorrect actions can cause significant damage to the system. Using commands with superuser privileges can be highly useful but also devastating if one is unaware of their consequences.
Let’s look at how to elevate privileges: Suppose you’ve logged in as a regular user named `edorio` and want to restart a service (cron). You will get the following error:
```sh
edorio@DESKTOP-W10:~$ service cron start
 * Starting periodic command scheduler cron                                                                             
cron: can't open or create /var/run/crond.pid: Permission denied

[fail]
edorio@DESKTOP-W10:~$
```
To avoid this error, you must use the **sudo** command before the command you wish to execute. It will prompt you for the root password, and the command will run successfully:
```sh
edorio@DESKTOP-W10:~$ sudo service cron start
[sudo] password for edorio:
 * Starting periodic command scheduler cron                                                                      
[ OK ]
edorio@DESKTOP-W10:~$
```
