---
title: Advanced Bash Scripting
description: 
published: true
date: 2023-02-11T10:32:44.324Z
tags: 
editor: markdown
dateCreated: 2023-02-11T10:32:37.758Z
---

- [Secuencias de comandos Bash avanzadas***Spanish** document is available*](/es/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}
- [高级 Bash 脚本***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}
- [고급 Bash 스크립팅***Korean** document is available*](/ko/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}


# Advanced Bash Scripting

The Bourne Again SHell (Bash) is a free shell for UNIX systems. It is the default shell for most Linux distributions and can be found on Mac OS X and other UNIX systems.

Bash provides a powerful scripting language that can be used for everything from simple scripts to complex applications. In this article, we will take a look at some of the advanced features of Bash that can be used to make your scripts more powerful and robust.

## Conditionals

Bash provides a number of ways to test conditions and make decisions in your scripts. The most common way to test a condition is to use the `if` statement.

The `if` statement syntax looks like this:

```
if CONDITION
then
    STATEMENTS
fi
```

The `CONDITION` can be any test that returns a boolean value (true or false). The `STATEMENTS` between the `then` and `fi` keywords will be executed if the `CONDITION` evaluates to true.

Here is a simple example:

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
fi
```

In this example, the `$USER` variable is checked to see if it is equal to the string `"root"`. If it is, the `echo` command is executed to print a message to the screen.

You can also use the `else` keyword to execute a different set of `STATEMENTS` if the `CONDITION` is false:

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
else
    echo "You are logged in as a normal user."
fi
```

If you need to check multiple conditions, you can use the `elif` keyword (short for "else if"):

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
elif [ $USER = "bob" ]
then
    echo "You are logged in as Bob."
else
    echo "You are logged in as a normal user."
fi
```

You can also use the `&&` and `||` operators to combine multiple conditions:

```bash
if [ $USER = "root" ] && [ $SHELL = "/bin/bash" ]
then
    echo "You are logged in as the root user and using the Bash shell."
fi

if [ $USER = "root" ] || [ $USER = "bob" ]
then
    echo "You are logged in as the root user or Bob."
fi
```

## Loops

Loops are used to execute a set of statements multiple times. Bash provides two different types of loops: `for` loops and `while` loops.

### For Loops

For loops are used to iterate over a list of values. The syntax for a for loop looks like this:

```
for VARIABLE in LIST
do
    STATEMENTS
done
```

The `LIST` can be any list of values, such as a list of files, a list of arguments, or a list of numbers. The `STATEMENTS` between the `do` and `done` keywords will be executed once for each value in the `LIST`.

Here is a simple example:

```bash
for FILE in *.txt
do
    echo $FILE
done
```

This example will print the names of all files in the current directory that end with the `.txt` extension.

You can also use the `seq` command to generate a list of numbers:

```bash
for NUM in $(seq 1 10)
do
    echo $NUM
done
```

This example will print the numbers 1 through 10.

### While Loops

While loops are used to execute a set of statements until a condition is met. The syntax for a while loop looks like this:

```
while CONDITION
do
    STATEMENTS
done
```

The `STATEMENTS` between the `do` and `done` keywords will be executed until the `CONDITION` evaluates to false.

Here is a simple example:

```bash
while [ $USER != "root" ]
do
    echo "You are not logged in as the root user."
done
```

This example will keep printing the message "You are not logged in as the root user." until the `$USER` variable contains the string `"root"`.

## Functions

Functions are used to group a set of statements together. Functions can be used like commands, and they can take arguments. The syntax for a function looks like this:

```
function NAME {
    STATEMENTS
}
```

The `NAME` can be any name you want to give the function. The `STATEMENTS` between the `{` and `}` keywords will be executed when the function is called.

Here is a simple example:

```bash
function print_message {
    echo "This is a message."
}

print_message
```

This example defines a function called `print_message` that prints a message to the screen. The function is called at the end of the script.

You can also pass arguments to a function:

```bash
function print_message {
    echo $1
}

print_message "This is a message."
```

In this example, the `$1` variable contains the first argument passed to the function. You can access additional arguments with the `$2`, `$3`, etc. variables.

## Arrays

Arrays are variables that can contain multiple values. The syntax for creating an array looks like this:

```bash
NAME=(VALUE1 VALUE2 VALUE3...)
```

The `NAME` can be any name you want to give the array. The `VALUE`s are the values that will be stored in the array.

Here is a simple example:

```bash
FILES=(*.txt *.sh)

for FILE in ${FILES[@]}
do
    echo $FILE
done
```

This example creates an array called `FILES` that contains all files in the current directory that end with the `.txt` or `.sh` extensions. The `@` symbol is used to expand the array into a list of individual values.

You can also access individual values in an array using their index:

```bash
FILES=(*.txt *.sh)

echo ${FILES[0]}
echo ${FILES[1]}
```

This example will print the first and second values in the `FILES` array (`*.txt` and `*.sh`, respectively).

## References

  - [Bash Scripting Tutorial](https://www.shellscript.sh/)
  - [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
  - [Bash Guide for Beginners](https://www.softpanorama.org/Scripting/Shellorama/bash_guide_for_beginners.shtml)