---
title: Linux System Monitoring and Logging
description: 
published: true
date: 2023-02-12T10:32:15.614Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:32:13.963Z
---

- [Supervisión y registro del sistema Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-system-monitoring-and-logging)
{.links-list}
- [Linux 系统监控和日志记录***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-system-monitoring-and-logging)
{.links-list}
- [Linux 시스템 모니터링 및 로깅***Korean** document is available*](/ko/Knowledge-base/Linux/linux-system-monitoring-and-logging)
{.links-list}


# Linux System Monitoring and Logging

The Linux operating system has many tools for monitoring system performance and activity. The tools are useful for checking the health of the system and for diagnosing and troubleshooting problems.

System performance can be monitored using tools that measure CPU and memory usage, network traffic, disk activity, and process information. System activity can be monitored using tools that track system log files, user activity, and process information.

## CPU and Memory Usage

The top command is a general purpose system activity monitor. It can be used to view information about the currently running processes, including the process ID, user ID, CPU usage, and memory usage. The htop command is a more user-friendly alternative to top.

The vmstat command can be used to view information about virtual memory, including memory usage, disk activity, and process information. The iostat command can be used to view information about disk activity.

The free command can be used to view information about the amount of free and used memory on the system. The -m option displays the output in megabytes.

## Network Traffic

The iftop command can be used to view information about network traffic. The tcpdump command can be used to capture and view network traffic.

## Disk Activity

The iotop command can be used to view information about disk activity. The -d option displays the output in megabytes per second.

## Process Information

The ps command can be used to view information about processes. The -e option displays all processes. The -f option displays the full command line for each process.

The pstree command can be used to view a tree of processes. The -p option displays the process ID for each process.

The lsof command can be used to view information about open files. The -n option displays the network files.

The kill command can be used to kill a process. The -9 option sends a SIGKILL signal to the process.

## System Log Files

The /var/log/messages file contains system messages. The /var/log/secure file contains security messages. The /var/log/apache2/access.log file contains Apache access logs.

## User Activity

The w command can be used to view information about user activity. The -u option displays information for a specific user.

The last command can be used to view information about the last logged in users. The -x option displays information about system reboots.

The who command can be used to view information about the users currently logged in.

## Conclusion

Linux provides many tools for monitoring system performance and activity. The tools are useful for checking the health of the system and for diagnosing and troubleshooting problems.