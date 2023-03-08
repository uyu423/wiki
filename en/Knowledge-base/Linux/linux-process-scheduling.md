---
title: Linux Process Scheduling
description: 
published: true
date: 2023-02-11T13:32:51.456Z
tags: 
editor: markdown
dateCreated: 2023-02-11T13:32:44.898Z
---

- [Programación de procesos de Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-process-scheduling)
{.links-list}
- [Linux进程调度***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-process-scheduling)
{.links-list}
- [Linux 프로세스 스케줄링***Korean** document is available*](/ko/Knowledge-base/Linux/linux-process-scheduling)
{.links-list}


# Linux Process Scheduling

The Linux process scheduler is a preemptive priority-based scheduler. The scheduler selects the next process to run based on its priority and other factors. The scheduler is implemented as a first-in, first-out (FIFO) queue.

## Process Scheduling Algorithms

The Linux process scheduler supports several scheduling algorithms:

* First-In First-Out (FIFO)
* Round Robin (RR)
* Static Priority Pre-emptive Scheduling (SPP)
* Dynamic Priority Pre-emptive Scheduling (DPP)
* Multiple Queue Scheduling (MQS)
* Completely Fair Scheduling (CFS)

The scheduler uses the following algorithm to select the next process to run:

1. The scheduler selects the process with the highest priority.
2. If there are multiple processes with the same priority, the scheduler selects the process that has been waiting the longest.
3. If there are multiple processes with the same priority and the same wait time, the scheduler select the process with the lowest pid.

## Process Priority

Each process is assigned a priority. The priority is an integer value between -20 and 19. The lower the priority value, the higher the priority of the process. The default priority of a process is 0.

A process can be assigned a higher priority by using the `nice` command. For example, to assign a priority of 10 to the `firefox` process, you would use the following command:

```
$ nice -n 10 firefox
```

A process can be assigned a lower priority by using the `renice` command. For example, to assign a priority of -10 to the `firefox` process, you would use the following command:

```
$ renice -n -10 firefox
```

## Process Scheduling Classes

Processes are classified into one of the following scheduling classes:

* Real-time
* Best-effort
* Idle

### Real-time processes

Real-time processes have the highest priority. They are guaranteed to be scheduled.

### Best-effort processes

Best-effort processes have a priority between 0 and 99. They are not guaranteed to be scheduled.

### Idle processes

Idle processes have the lowest priority. They are only scheduled when there are no other processes to run.

## Process Scheduling Policies

Processes can be scheduled using one of the following policies:

* FIFO
* RR
* SPP
* DPP
* MQS
* CFS

### FIFO

FIFO is the simplest scheduling policy. It schedules processes in the order they are created.

### RR

RR is a more advanced scheduling policy. It schedules processes in a round-robin fashion.

### SPP

SPP is a static priority scheduling policy. It schedules processes based on their static priority.

### DPP

DPP is a dynamic priority scheduling policy. It schedules processes based on their dynamic priority.

### MQS

MQS is a multiple queue scheduling policy. It schedules processes based on their queue.

### CFS

CFS is a completely fair scheduling policy. It schedules processes based on their wait time.

## Process Scheduling Parameters

The Linux process scheduler uses the following parameters to schedule processes:

* `nice`: The priority of the process.
* `rt_priority`: The real-time priority of the process.
* `policy`: The scheduling policy of the process.
* `sched_latency`: The maximum time a process can be delayed before it is scheduled.
* `sched_min_granularity`: The minimum time between schedulings of the process.
* `sched_wakeup_granularity`: The time between schedulings of the process when it is woken up.

## Conclusion

The Linux process scheduler is a preemptive priority-based scheduler. The scheduler selects the next process to run based on its priority and other factors. The scheduler is implemented as a first-in, first-out (FIFO) queue.

The scheduler uses the following algorithm to select the next process to run:

1. The scheduler selects the process with the highest priority.
2. If there are multiple processes with the same priority, the scheduler selects the process that has been waiting the longest.
3. If there are multiple processes with the same priority and the same wait time, the scheduler select the process with the lowest pid.

Each process is assigned a priority. The priority is an integer value between -20 and 19. The lower the priority value, the higher the priority of the process.

Processes are classified into one of the following scheduling classes:

* Real-time
* Best-effort
* Idle

Real-time processes have the highest priority. They are guaranteed to be scheduled.

Best-effort processes have a priority between 0 and 99. They are not guaranteed to be scheduled.

Idle processes have the lowest priority. They are only scheduled when there are no other processes to run.

Processes can be scheduled using one of the following policies:

* FIFO
* RR
* SPP
* DPP
* MQS
* CFS

FIFO is the simplest scheduling policy. It schedules processes in the order they are created.

RR is a more advanced scheduling policy. It schedules processes in a round-robin fashion.

SPP is a static priority scheduling policy. It schedules processes based on their static priority.

DPP is a dynamic priority scheduling policy. It schedules processes based on their dynamic priority.

MQS is a multiple queue scheduling policy. It schedules processes based on their queue.

CFS is a completely fair scheduling policy. It schedules processes based on their wait time.

The Linux process scheduler uses the following parameters to schedule processes:

* `nice`: The priority of the process.
* `rt_priority`: The real-time priority of the process.
* `policy`: The scheduling policy of the process.
* `sched_latency`: The maximum time a process can be delayed before it is scheduled.
* `sched_min_granularity`: The minimum time between schedulings of the process.
* `sched_wakeup_granularity`: The time between schedulings of the process when it is woken up.