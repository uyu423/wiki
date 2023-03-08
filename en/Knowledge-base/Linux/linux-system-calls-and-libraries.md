---
title: Linux System Calls and Libraries
description: 
published: true
date: 2023-02-09T11:17:39.117Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:17:32.961Z
---

- [Llamadas y bibliotecas del sistema Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-system-calls-and-libraries)
{.links-list}
- [Linux 系统调用和库***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-system-calls-and-libraries)
{.links-list}
- [Linux 시스템 호출 및 라이브러리***Korean** document is available*](/ko/Knowledge-base/Linux/linux-system-calls-and-libraries)
{.links-list}


# Linux System Calls and Libraries

System calls are how a program request services from an operating system. Libraries are how a program request services from a programming language.

In this article, we'll take a look at how system calls and libraries work in Linux. We'll start with a brief overview of each, and then we'll look at some specific examples.

## System Calls

System calls are the interface between user space and kernel space. They are how a program request services from an operating system.

System calls are made by calling a function that has a special name. For example, in Linux the system call for reading from a file is called `read()`.

System calls are made by passing arguments to the function. The first argument is always a number that identifies the system call. The rest of the arguments depend on the system call being made.

When a system call is made, the kernel checks to see if the calling program has the permission to make the call. If the call is allowed, the kernel executes the code for the system call.

The code for a system call is usually written in assembly language. This makes it difficult for programmers to understand and debug.

System calls are slow because they involve a context switch between user space and kernel space. A context switch is when the CPU saves the state of one process and loads the state of another process.

System calls are also a security risk. A buggy system call can crash the kernel or allow a malicious user to gain access to privileged information.

## Libraries

Libraries are a way for programs to request services from a programming language.

Libraries are made up of a collection of functions. Each function performs a specific task.

For example, the C standard library provides functions for reading and writing to files, manipulating strings, and performing math operations.

Libraries are usually written in the same language as the programs that use them. This makes it easier for programmers to understand and debug.

Libraries are faster than system calls because they don't involve a context switch.

Libraries are also more secure than system calls because they are less likely to contain buggy code.

## Examples

Now that we've seen a brief overview of system calls and libraries, let's look at some specific examples.

### Reading from a File

Here's an example of how to read from a file using a system call:

```c
#include <unistd.h>

int main() {
  char buf[1024];
  int n;

  n = read(0, buf, sizeof(buf));
  if (n < 0) {
    perror("read");
    return 1;
  }

  write(1, buf, n);

  return 0;
}
```

The `read()` system call reads data from a file. The first argument is the file descriptor. The second argument is a buffer where the data will be stored. The third argument is the size of the buffer.

The `write()` system call writes data to a file. The first argument is the file descriptor. The second argument is the buffer containing the data. The third argument is the number of bytes to write.

### Writing to a File

Here's an example of how to write to a file using a library:

```c
#include <stdio.h>

int main() {
  FILE *fp;
  char buf[1024];
  int n;

  fp = fopen("test.txt", "w");
  if (fp == NULL) {
    perror("fopen");
    return 1;
  }

  n = fwrite(buf, 1, sizeof(buf), fp);
  if (n < 0) {
    perror("fwrite");
    return 1;
  }

  fclose(fp);

  return 0;
}
```

The `fopen()` function opens a file. The first argument is the path of the file. The second argument is the mode. The mode can be `"r"` for reading, `"w"` for writing, or `"a"` for appending.

The `fwrite()` function writes data to a file. The first argument is the buffer containing the data. The second argument is the size of each element. The third argument is the number of elements to write. The fourth argument is the file pointer.

The `fclose()` function closes a file. The argument is the file pointer.

## Conclusion

In this article, we've seen a brief overview of system calls and libraries. We've also seen some specific examples of how to use them.