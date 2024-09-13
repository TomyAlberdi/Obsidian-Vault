We create a new [[Bash]] file using `touch` and open it with `nano`:
```sh
touch myscript
nano myscript
```
At the beginning of any Bash script, we must define which Shell we will use:
```sh
#!/bin/bash
```
We configure the file to be executable; otherwise, it will show a permission denied error:
```sh
chmod +x ./myscript
```
We execute it by typing in the shell:
```sh
./myscript
```
We will use this method of generating files with commands so that our system can perform tasks or run processes to automate database backups, server maintenance routines, permission grants, searches, and other things.
## Variables
### Global or Environment Variables:
The Linux system sets some global environment variables when we log into our system, and they are always in uppercase letters. If we want to see the environment variables we are using and that are loaded in our session, we can type the command `printenv` or `env` in our shell.
To declare a global variable, it must be done as follows:
```sh
export VARIABLE_NAME=value
```
To access it, we use the statement:
```sh
$VARIABLE_NAME
```
### Local or User Variables:
These variables have the particularity that they can only be accessed by the user and the session in which they were created. A local variable is declared as follows:
```sh
variablename=value
```
And it is accessed with:
```sh
$variablename
```
## Control Structures
### If-Then Statement:
Bash scripts often require conditionals. Typically, we imagine a scenario like "If the value is less than 10, do this, otherwise do that." For this, we use `if-then`. The most basic structure of the `if-then` statement looks like this:
```sh
if command; then
  do something
fi
```
### If-Then-Else Statement:
The `if-then-else` statement follows this structure:
```sh
if command; then
  do something
else
  do something else
fi
```
If the command executes and returns zero (which means success), it does not run the commands after the `else` statement. However, if the `if` statement returns a number other than zero (which means the condition is not met), the shell executes the commands after the `else` statement. In the following example, we see how it returns a message depending on whether the `ping` command was successful:
```sh
#!/bin/bash
ping -c 1 8.8.8.8
if [ $? -ne 0 ]; then
  echo "Not connected to the network"
else
  echo "Connected to the network"
fi
```
## Comparisons
### Numeric Comparisons:
We can perform a numeric comparison between two values using the following comparison operators:
- `number1 -eq number2`: Checks if `number1` is equal to `number2`.
- `number1 -ge number2`: Checks if `number1` is greater than or equal to `number2`.
- `number1 -gt number2`: Checks if `number1` is greater than `number2`.
- `number1 -le number2`: Checks if `number1` is less than or equal to `number2`.
- `number1 -lt number2`: Checks if `number1` is less than `number2`.
- `number1 -ne number2`: Checks if `number1` is not equal to `number2`.
Considering that the comparison is placed within square brackets, here’s an example:
```sh
#!/bin/bash
num=11
if [ $num -gt 10 ]; then
  echo "$num is bigger than 10"
else
  echo "$num is less than 10"
fi
```
### String Comparisons:
We can perform string comparisons between two alphanumeric values using the following operators:
- `string1 = string2`: Checks if `string1` is identical to `string2`.
- `string1 != string2`: Checks if `string1` is not identical to `string2`.
- `string1 < string2`: Checks if `string1` is less than `string2`.
- `string1 > string2`: Checks if `string1` is greater than `string2`.
- `-n string1`: Checks if `string1` has a non-zero length.
- `-z string1`: Checks if `string1` has a zero length.
We can apply string comparisons in the following example. If the user is logged in as `root`, it goes through the `if`, otherwise it goes through the `else`:
```sh
#!/bin/bash
user="root"
if [ $user = $USER ]; then
  echo "The user $user is the current logged in user"
fi
```
## Math Calculations
We can perform basic mathematical operations using the syntax `$((2 + 2))`:
```sh
#!/bin/bash
var1=$(( 5 + 5 ))
echo $var1
var2=$(( $var1 * 2 ))
echo $var2
```