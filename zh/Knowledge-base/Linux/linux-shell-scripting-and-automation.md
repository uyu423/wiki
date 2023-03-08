---
title: Linux Shell 脚本和自动化
description: 
published: true
date: 2023-02-12T06:32:33.454Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:32:31.698Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Shell Scripting and Automation***English** document is available*](/en/Knowledge-base/Linux/linux-shell-scripting-and-automation)
{.links-list}


# Linux Shell 脚本和自动化

Linux shell 是自动执行任务的强大工具，使开发人员的工作更加轻松。在本文中，我们将探讨 shell 脚本的一些基础知识以及它如何帮助您的工作。

## 什么是外壳？

shell 是一种命令行解释器，可让您与操作系统进行交互。在 Linux 中，默认的 shell 是 Bash (Bourne Again Shell)。

Shell 脚本只是存储在文本文件中的一系列 Shell 命令。您可以通过在命令提示符下键入脚本名称来运行 shell 脚本。

## 为什么要使用 shell 脚本？

Shell 脚本是一种很好的自动化任务的方法，否则您必须手动执行这些任务。例如，假设您想列出目录中的所有文件。您可以通过在命令提示符下键入 ls 来手动执行此操作，但如果您必须对数千个目录执行此操作，那么编写一个 shell 脚本来为您执行此操作会快得多。

shell 脚本的另一个常见用途是自动执行重复性任务。例如，如果您需要使用不同的参数一遍又一遍地运行相同的命令，您可以编写一个 shell 脚本来为您完成。

Shell 脚本也是自动执行需要定期运行的任务（例如备份）的好方法。您可以使用 `cron` 等工具安排 shell 脚本每天、每周或每月运行。

## 如何编写 shell 脚本

Shell 脚本只是包含一系列 Shell 命令的文本文件。您可以使用任何文本编辑器创建一个新的 shell 脚本，例如 `nano` 或 `vi`。

让我们创建一个简单的 shell 脚本，它将列出当前目录中的所有文件。首先，使用 `nano` 打开一个新的文本文件：

```
nano list-files.sh
```

现在在文件中键入以下内容：

```
#!/bin/bash
ls
```

保存文件并退出“nano”。

要使 shell 脚本可执行，您需要使用 `chmod` 命令更改其权限：

```
chmod +x list-files.sh
```

现在您可以通过输入脚本名称来运行 shell 脚本：

```
./list-files.sh
```

您应该会看到当前目录中所有文件的列表。

让我们看看我们的 shell 脚本的每一行做了什么：

- 第一行，`# !/bin/bash`，称为 shebang。它告诉 shell 使用哪个解释器来执行脚本。
- `ls` 命令列出当前目录中的所有文件。

## 变量

Shell 脚本可以使用变量来存储数据并使您的脚本更加灵活。

要创建一个变量，您只需要给它一个名称和一个值。例如，要创建值为“bar”的变量“foo”，您可以在命令提示符下键入以下内容：

```
foo=bar
```

您现在可以使用“$”符号来访问变量的值。例如，要打印 `foo` 变量的值，您可以键入以下内容：

```
echo $foo
```

您还可以在 shell 脚本中使用变量。让我们修改我们的 list-files.sh 脚本来使用一个变量。

首先，让我们创建一个变量来存储我们要列出的目录：

```
directory=/path/to/directory
```

现在我们可以在 shell 脚本中使用 `$directory` 变量：

```
#!/bin/bash
ls $directory
```

保存文件并退出“nano”。

您现在可以使用 `directory` 变量运行 shell 脚本：

```
./list-files.sh
```

您应该会看到指定目录中所有文件的列表。

## 条件

Shell 脚本可以使用条件来决定要采取什么行动。

条件语句基于“if”、“then”和“fi”关键字。例如，以下条件将检查“foo”变量是否等于“bar”，如果是，将打印“equal”：

```
if [ $foo = "bar" ]; then
  echo "equal"
fi
```

`if` 关键字后跟方括号 (`[]`) 中的条件。条件后跟 `then` 关键字，然后是满足条件时要采取的操作。该操作后跟 `fi` 关键字，它结束条件。

让我们修改我们的 list-files.sh 脚本以使用条件。

首先，让我们创建一个变量来存储我们要列出的目录：

```
directory=/path/to/directory
```

现在我们可以在 shell 脚本中使用 `$directory` 变量：

```
#!/bin/bash
if [ -d $directory ]; then
  ls $directory
fi
```

保存文件并退出“nano”。

您现在可以使用 `directory` 变量运行 shell 脚本：

```
./list-files.sh
```

您应该会看到指定目录中所有文件的列表。

if 语句的 -d 选项检查 directory 变量是否为目录。如果是，则执行 ls 命令并列出目录的内容。

## 循环

Shell 脚本可以使用循环来重复代码块，直到满足条件。

循环基于“while”和“do”关键字。例如，以下循环将打印从 1 到 10 的数字：

```
i=1
while [ $i -le 10 ]; do
  echo $i
  i=$((i+1))
done
```

`while` 关键字后跟方括号 (`[]`) 中的条件。条件后跟 do 关键字，然后是要采取的操作。该操作后跟一个结束循环的“完成”关键字。

在上面的示例中，我们创建了一个变量 i 并将其设置为 1。只要 i 的值小于或等于 10，while 循环就会继续运行。

每次循环运行时，它都会打印 `i` 的值，然后将 `i` 递增 1。所以第一次循环运行时，`i` 为 1，第二次 `i` 为 2，依此类推.

## 功能

Shell 脚本可以利用函数将相关代码组合在一起。

函数基于“function”关键字。例如，以下函数将打印当前日期和时间：

```
function print-date {
  date
}
```

`function` 关键字后跟函数名称（本例中为 `print-date`）。函数体包含在大括号 (`{}`) 中。

要调用一个函数，您只需键入它的名称。例如，要调用 `print-date` 函数，您可以键入以下内容：

```
print-date
```

## 结论

Shell 脚本是自动执行任务并使您作为开发人员的生活更加轻松的好方法。在本文中，我们探讨了 shell 脚本的一些基础知识，包括如何编写 shell 脚本、使用变量、条件和循环，以及如何创建函数。

## 资源

- [Shell 脚本教程](https://www.shellscript.sh/)
- [Bash 初学者指南](https://www.tldp.org/LDP/Bash-Beginners-Guide/html/)
- [高级 Bash 脚本指南](https://www.tldp.org/LDP/abs/html/)