---
title: Managing Processes in Linux
description: 
published: true
date: 2023-02-11T07:32:29.538Z
tags: 
editor: markdown
dateCreated: 2023-02-11T07:32:27.730Z
---

- [Gestión de procesos en Linux***Spanish** document is available*](/es/Knowledge-base/Linux/managing-processes-in-linux)
{.links-list}
- [在 Linux 中管理进程***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/managing-processes-in-linux)
{.links-list}
- [Linux에서 프로세스 관리***Korean** document is available*](/ko/Knowledge-base/Linux/managing-processes-in-linux)
{.links-list}


# Managing Processes in Linux

In this article, we'll take a look at process management in Linux. We'll cover some of the basics of what processes are and how they work, and then we'll get into some of the tools and techniques you can use to manage them.

## What is a Process?

A process is an instance of a program that is being executed. When you run a program, it creates a process. A process has a number of associated data structures, including a list of open files, a list of running threads, and various process-specific options.

Each process is given a unique process ID (PID), which is used by the operating system to keep track of the process. Processes can be created and destroyed, and they can be in one of three states:

- **Running:** The process is currently running.
- **Sleeping:** The process is not currently running, but it is waiting for an event to occur (such as an I/O operation to complete).
- **Zombie:** The process has finished executing, but its parent process has not yet collected its exit status.

## Managing Processes

There are a number of tools and techniques that you can use to manage processes in Linux. We'll cover some of the most common ones here.

### The ps Command

The **ps** command is used to list the currently running processes. By default, it will only show processes that were started by the current user. To see all processes, use the **-A** option:

```
ps -A
```

To see more information about each process, use the **-o** option. For example, to see the PID, command, and user for each process, use this command:

```
ps -o pid,command,user
```

There are a number of other options that you can use with **ps**. For a complete list, consult the **ps** man page.

### The top Command

The **top** command is similar to **ps**, but it provides a continuously updated list of processes. It also shows additional information such as the CPU and memory usage of each process.

To quit **top**, press **q**. To sort the list of processes, press **o** and then enter the sort criteria. For example, to sort by PID, use this command:

```
top -o pid
```

To see a help screen, press **h**.

### The kill Command

The **kill** command is used to send a signal to a process. By default, it sends the **SIGTERM** signal, which requests that the process terminate. If the process does not respond to that signal, you can use the **-9** option to send the **SIGKILL** signal, which forces the process to terminate.

For example, to kill the process with PID 1234, use this command:

```
kill 1234
```

To kill all processes in the process group with ID 5678, use this command:

```
kill -9 -5678
```

There are a number of other signals that you can send with **kill**. Consult the **kill** man page for a complete list.

### The pkill Command

The **pkill** command is similar to **kill**, but it allows you to kill processes by name instead of by PID. For example, to kill all processes with the name **firefox**, use this command:

```
pkill firefox
```

To kill all processes that belong to the user **jane**, use this command:

```
pkill -u jane
```

For a complete list of options, consult the **pkill** man page.

### The killall Command

The **killall** command is similar to **pkill**, but it kills all processes that match the specified name, rather than just the first one it finds. For example, to kill all processes with the name **firefox**, use this command:

```
killall firefox
```

To kill all processes that belong to the user **jane**, use this command:

```
killall -u jane
```

For a complete list of options, consult the **killall** man page.

## Wrapping Up

In this article, we've covered some of the basics of process management in Linux. We've seen how to use the **ps**, **top**, **kill**, **pkill**, and **killall** commands to manage processes.