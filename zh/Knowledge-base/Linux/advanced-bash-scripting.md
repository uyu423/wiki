---
title: 高级 Bash 脚本
description: 
published: true
date: 2023-02-11T10:32:39.480Z
tags: 
editor: markdown
dateCreated: 2023-02-11T10:32:37.753Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Advanced Bash Scripting***English** document is available*](/en/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}


# 高级 Bash 脚本

Bourne Again SHell (Bash) 是用于 UNIX 系统的免费 shell。它是大多数 Linux 发行版的默认 shell，并且可以在 Mac OS X 和其他 UNIX 系统上找到。

Bash 提供了一种功能强大的脚本语言，可用于从简单脚本到复杂应用程序的所有内容。在本文中，我们将了解 Bash 的一些高级功能，这些功能可用于使您的脚本更加强大和健壮。

## 条件

Bash 提供了多种方法来测试条件并在脚本中做出决定。测试条件的最常见方法是使用 if 语句。

`if` 语句语法如下所示：

```
if CONDITION
then
    STATEMENTS
fi
```

`CONDITION` 可以是任何返回布尔值（真或假）的测试。如果 `CONDITION` 的计算结果为真，则执行 `then` 和 `fi` 关键字之间的 `STATEMENTS`。

这是一个简单的例子：

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
fi
```

在此示例中，检查“$USER”变量以查看它是否等于字符串“root”。如果是，则执行“echo”命令以在屏幕上打印一条消息。

如果 CONDITION 为假，您还可以使用 else 关键字执行一组不同的 STATEMENTS：

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
else
    echo "You are logged in as a normal user."
fi
```

如果需要检查多个条件，可以使用 elif 关键字（“else if”的缩写）：

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

您还可以使用“&&”和“||”运算符来组合多个条件：

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

## 循环

循环用于多次执行一组语句。 Bash 提供了两种不同类型的循环：`for` 循环和`while` 循环。

### 循环

For 循环用于迭代值列表。 for 循环的语法如下所示：

```
for VARIABLE in LIST
do
    STATEMENTS
done
```

`LIST` 可以是任何值列表，例如文件列表、参数列表或数字列表。 `do` 和 `done` 关键字之间的 `STATEMENTS` 将针对 `LIST` 中的每个值执行一次。

这是一个简单的例子：

```bash
for FILE in *.txt
do
    echo $FILE
done
```

此示例将打印当前目录中所有以 .txt 扩展名结尾的文件的名称。

您还可以使用 `seq` 命令生成数字列表：

```bash
for NUM in $(seq 1 10)
do
    echo $NUM
done
```

此示例将打印数字 1 到 10。

### While 循环

While 循环用于执行一组语句，直到满足条件。 while 循环的语法如下所示：

```
while CONDITION
do
    STATEMENTS
done
```

`do` 和 `done` 关键字之间的 `STATEMENTS` 将被执行，直到 `CONDITION` 的计算结果为 false。

这是一个简单的例子：

```bash
while [ $USER != "root" ]
do
    echo "You are not logged in as the root user."
done
```

此示例将继续打印消息“您没有以 root 用户身份登录。”直到 `$USER` 变量包含字符串 `"root"`。

## 功能

函数用于将一组语句组合在一起。函数可以像命令一样使用，并且可以带参数。函数的语法如下所示：

```
function NAME {
    STATEMENTS
}
```

`NAME` 可以是您想要赋予函数的任何名称。 `{` 和 `}` 关键字之间的 `STATEMENTS` 将在调用函数时执行。

这是一个简单的例子：

```bash
function print_message {
    echo "This is a message."
}

print_message
```

此示例定义了一个名为“print_message”的函数，用于将消息打印到屏幕上。该函数在脚本末尾调用。

您还可以将参数传递给函数：

```bash
function print_message {
    echo $1
}

print_message "This is a message."
```

在此示例中，“$1”变量包含传递给函数的第一个参数。您可以使用“$2”、“$3”等变量访问其他参数。

## 数组

数组是可以包含多个值的变量。创建数组的语法如下所示：

```bash
NAME=(VALUE1 VALUE2 VALUE3...)
```

`NAME` 可以是您想要给数组的任何名称。 `VALUE` 是将存储在数组中的值。

这是一个简单的例子：

```bash
FILES=(*.txt *.sh)

for FILE in ${FILES[@]}
do
    echo $FILE
done
```

此示例创建一个名为“FILES”的数组，其中包含当前目录中以“.txt”或“.sh”扩展名结尾的所有文件。 `@` 符号用于将数组扩展为单个值的列表。

您还可以使用索引访问数组中的各个值：

```bash
FILES=(*.txt *.sh)

echo ${FILES[0]}
echo ${FILES[1]}
```

此示例将打印“FILES”数组中的第一个和第二个值（分别为“*.txt”和“*.sh”）。

## 参考

  - [Bash 脚本教程](https://www.shellscript.sh/)
  - [高级 Bash 脚本指南](https://tldp.org/LDP/abs/html/)
  - [Bash 初学者指南](https://www.softpanorama.org/Scripting/Shellorama/bash_guide_for_beginners.shtml)