---
title: Linux Shell Scripting and Automation
description: 
published: true
date: 2023-02-12T06:32:38.966Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:32:31.702Z
---

- [Automatización y secuencias de comandos de shell de Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-shell-scripting-and-automation)
{.links-list}
- [Linux Shell 脚本和自动化***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-shell-scripting-and-automation)
{.links-list}
- [Linux 셸 스크립팅 및 자동화***Korean** document is available*](/ko/Knowledge-base/Linux/linux-shell-scripting-and-automation)
{.links-list}


# Linux Shell Scripting and Automation

The Linux shell is a powerful tool for automating tasks and makes life much easier for developers. In this article we'll explore some of the basics of shell scripting and how it can help you in your work.

## What is a shell?

A shell is a command-line interpreter that allows you to interact with your operating system. In Linux, the default shell is Bash (Bourne Again Shell).

Shell scripts are simply a sequence of shell commands stored in a text file. You can run a shell script by typing its name at the command prompt.

## Why use shell scripting?

Shell scripting is a great way to automate tasks that you would otherwise have to do manually. For example, let's say you wanted to list all the files in a directory. You could do this manually by typing `ls` at the command prompt, but if you had to do this for thousands of directories, it would be much faster to write a shell script to do it for you.

Another common use for shell scripts is to automate repetitive tasks. For example, if you need to run the same command over and over again with different arguments, you can write a shell script to do it for you.

Shell scripts are also a great way to automate tasks that need to be run on a regular basis, such as backups. You can schedule a shell script to run daily, weekly, or monthly using a tool like `cron`.

## How to write a shell script

Shell scripts are simply text files containing a sequence of shell commands. You can create a new shell script with any text editor, such as `nano` or `vi`.

Let's create a simple shell script that will list all the files in the current directory. First, open a new text file with `nano`:

```
nano list-files.sh
```

Now type the following into the file:

```
#!/bin/bash
ls
```

Save the file and exit `nano`.

To make the shell script executable, you need to change its permissions with the `chmod` command:

```
chmod +x list-files.sh
```

Now you can run the shell script by typing its name:

```
./list-files.sh
```

You should see a list of all the files in the current directory.

Let's take a look at what each line of our shell script does:

- The first line, `#!/bin/bash`, is called the shebang. It tells the shell which interpreter to use to execute the script.
- The `ls` command lists all the files in the current directory.

## Variables

Shell scripts can make use of variables to store data and make your scripts more flexible.

To create a variable, you just need to give it a name and a value. For example, to create a variable `foo` with the value `bar`, you would type the following at the command prompt:

```
foo=bar
```

You can now use the `$` symbol to access the value of the variable. For example, to print the value of the `foo` variable, you would type the following:

```
echo $foo
```

You can also use variables in your shell scripts. Let's modify our `list-files.sh` script to make use of a variable.

First, let's create a variable to store the directory we want to list:

```
directory=/path/to/directory
```

Now we can use the `$directory` variable in our shell script:

```
#!/bin/bash
ls $directory
```

Save the file and exit `nano`.

You can now run the shell script with the `directory` variable:

```
./list-files.sh
```

You should see a list of all the files in the specified directory.

## Conditionals

Shell scripts can make use of conditionals to make decisions about what actions to take.

Conditionals are based on the `if`, `then`, and `fi` keywords. For example, the following conditional will check if the `foo` variable is equal to `bar` and, if so, will print `equal`:

```
if [ $foo = "bar" ]; then
  echo "equal"
fi
```

The `if` keyword is followed by a condition in square brackets (`[]`). The condition is followed by the `then` keyword, which is followed by the action to take if the condition is met. The action is followed by the `fi` keyword, which ends the conditional.

Let's modify our `list-files.sh` script to make use of a conditional.

First, let's create a variable to store the directory we want to list:

```
directory=/path/to/directory
```

Now we can use the `$directory` variable in our shell script:

```
#!/bin/bash
if [ -d $directory ]; then
  ls $directory
fi
```

Save the file and exit `nano`.

You can now run the shell script with the `directory` variable:

```
./list-files.sh
```

You should see a list of all the files in the specified directory.

The `-d` option to the `if` statement checks if the `directory` variable is a directory. If it is, the `ls` command is executed and the contents of the directory are listed.

## Loops

Shell scripts can make use of loops to repeat a block of code until a condition is met.

Loops are based on the `while` and `do` keywords. For example, the following loop will print the numbers from 1 to 10:

```
i=1
while [ $i -le 10 ]; do
  echo $i
  i=$((i+1))
done
```

The `while` keyword is followed by a condition in square brackets (`[]`). The condition is followed by the `do` keyword, which is followed by the action to take. The action is followed by the `done` keyword, which ends the loop.

In the example above, we create a variable `i` and set it to 1. The `while` loop will continue to run as long as the value of `i` is less than or equal to 10.

Each time the loop runs, it will print the value of `i` and then increment `i` by 1. So the first time the loop runs, `i` is 1 and the second time `i` is 2, and so on.

## Functions

Shell scripts can make use of functions to group related code together.

Functions are based on the `function` keyword. For example, the following function will print the current date and time:

```
function print-date {
  date
}
```

The `function` keyword is followed by the name of the function (`print-date` in this example). The function body is enclosed in curly brackets (`{}`).

To call a function, you just need to type its name. For example, to call the `print-date` function, you would type the following:

```
print-date
```

## Conclusion

Shell scripting is a great way to automate tasks and make your life as a developer much easier. In this article we've explored some of the basics of shell scripting, including how to write shell scripts, use variables, conditionals, and loops, and how to create functions.

## Resources

- [Shell Scripting Tutorial](https://www.shellscript.sh/)
- [Bash Guide for Beginners](https://www.tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash-Scripting Guide](https://www.tldp.org/LDP/abs/html/)