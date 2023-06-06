---
title: "6. Operating Systems Introduction"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 6. Operating Systems Introduction

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/arch-op/y1/tb2/6-operating-systems-intro)

## History of Operating Systems

- **Late 1940s**: No operating system, the programmer was also the user
- **1950s**: Specialist operators, who where not programmers, fed the machine with programs
- **1960s**: Programs were stored on a punched card which was loaded into the machine
- **Late 1960s and 1970s**: First attempt to provide interactive use of a computer
- **1980s**: Networking and communication
- **1990s**: Move to open systems

## What is an Operating System?

An operating system is a program, which is written just like any other program. It is loaded each time the computer is turned on and runs until it is switched off.

Operating systems makes the hardware more useful and more user-friendly.

## What Does an Operating System do?

- Provides an environment which helps others to do productive work
- Helps a user to develop and run programs, by providing a convenient environment
- Starting and stopping programs, and sharing the CPU between them
- **Managing memory**:
    - Which parts of memory are in use and which are free
    - Provides mechanisms by which programs can ask for more memory or give back memory they no longer need
- **Input and Output**:
    - Covers up the differences between alternative makes and models of devices
    - Overlaps input and output with processing
- File systems/organisation
- Protection: one memory, one CPU: protect programs interference
- Networking: covers up the differences between machines
- Error handling and recovery

## What is a Kernel?

- Central component or heart of operating system
- Interface between hardware components and software applications
- Makes the software to interact with the hardware to get a specific task done
- It decides the amount of resources (RAM, GPU, etc) to be used by every application
- It decides on what programs to be executed and in which order
- It has a separate space on memory so it functions independently
- It acts as a central authority which guides memory and keeps eye on all the hardware and software data flow
- System call: Every process which starts on a system, demands the resources from the kernel

![Operating System Kernel](/img/arch-op/y1/os-kernel.png)

A CPU operates in at least two different modes:

- **User Mode**: The CPU can only execute a subset of its instructions (the more common ones like add, subtract, load, and store). If a 
program is executed in user mode, it does not have access to memory, hardware, and such resources.
- **Kernel Mode**: The CPU can execute all of its instructions, including extra privileged instructions. If a program is executed in Kernel mode, it has direct access to memory, hardware, and such resources.

There are two types of kernels:

- **Monolithic Kernel**: User services and kernel services both are kept in the same address space, larger than a micro kernel, less access time and fast execution, hard to extend, higher performance, higher risk of system crash. Linux uses monolithic kernel.
- **Microkernel**: User services and kernel services are kept in separate address space, smaller in size, greater access time and slow execution, easily extendable, lower responsibility. Windows uses hybrid (micro + monolithic).


![Monolithic and Micro Kernels](/img/arch-op/y1/monolithic-and-micro-kernels.png)

## Types of Operating Systems

### Batch Systems

- Earliest systems developed
- Data and commands to manipulate the program and data are all submitted together to the computer in the form of a job
- Little or no interaction between users and an executing program
- Example: Payroll processing, bank or credit card statements

### Interactive Systems

- Most common mode of computing using keyboard, mouse, and screen
- Significant improvement on batch systems, as it is now possible to intervene directly while a program is being developed, or as it is running
- **Single user**: Multitasking and interactive computing on a single-user bassis, such as Windows, MS-DOS, and OS/2
- **Multi user**: Interactive computing on a multi-access or multi-user basis (using different terminals), such as Unix, Linux, Windows 10, macOS

### General Purpose

A given environment may want a bit of everything. For example, supporting interactive users but also including the ability to run programs in batch mode.

- **Network OS**: To share resource such as printers and databases across a network, such as Windows NT Server
- **Distributed Systems**: The most recent development in operating systems, consists of a group of machines acting together as one
- **Specialist Systems**: Dedicated to processing large volumes of data

## Design of Operating Systems

Operating systems must contain the following functions:

- Process management
- Memory management
- I/O management
- File storage
- Network management
