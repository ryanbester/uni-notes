---
title: "1.4. Processes"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.4. Processes

A **process** is an **instance** of a program that is **currently being executed**.

There are several **attributes** attached to a process, including:

- Ownership
- Process ID (pid)
- CPU usage
- Running time

There are three types of processes:

- **User process**: Initiated by a regular user
- **Daemon process**: A process designed to run in a background
- **Kernel process**: Executed in kernel-mode only

## Process States

Most processes can be in one of the following states: **on** the CPu or **off** the CPU. Only one process can run at a time on a single CPU.

A process that is **off** the CPU can be in the following sub-states:

- **Runnable state**: The process has all the resources it needs except the CPU
- **Sleeping state**: The process needs resources that are not currently available
- **Uninterruptable sleep state**: The process is waiting for a particular time slot or particular event to occur
- **Zombie state**: The time between when the process terminates and the parent releases the child process

![Process States](/img/cyber-security/y1/process-states.png)

## Threads

A thread is the smallest unit of execution, and is a component of a process.

Processes can contain many threads.

![Threads](/img/cyber-security/y1/process-threads.png)
