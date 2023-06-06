---
title: "8. Process Scheduling"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
math: true
---

# 8. Process Scheduling

[🔒 Recording 1](https://github.com/ryanbester/uni-resources/tree/main/arch-op/y1/tb2/8-process-scheduling-1)

[🔒 Recording 2](https://github.com/ryanbester/uni-resources/tree/main/arch-op/y1/tb2/9-process-scheduling-2)

## CPU Scheduling

- CPU scheduling is the basis of multiprogrammed operating systems. By switching the CPU among processes, the operating system can make the computer more productive
- In a single-processor system, only one process can run at a time. Others must wait until the CPU is free and can be rescheduled. The objective of multiprogramming is to have some process running at all times, to maximised CPU utilisation
- A process is executed until it must wait, typcially for the completion of some I/O request
- Several processes are kept in memory at one time. Wehn one process has to wait, the operating system takes the CPU away from that process and gives the CPU to another process
- CPU scheduling is central to operating system design

## CPU - I/O cycle

- Process execution consists of a cycle of CPU execution and I/O wait
- Processes alternate between these two states. Process execution begins with a CPU burst. That is followed by an I/O burst, which is followed by another CPU burst, then I/O burst and so on
- The final CPU burst ends with a system request to terminate execution

![CPU I/O Cycle](/img/arch-op/y1/cpu-io-cycle.png)

## CPU Scheduling

- Whenever the CPU becomes idle, the operating system must select one of the processes in the ready queue to be executeed. The selection process is carried out by the CPU scheduler
- The scheduler selects a process from the processes in memory that are ready to execute and allocates the CPU to that process
- Conceptually, all the processes in the ready queue are lined up waiting for a chance to run on the CPU

### Non-preemptive Scheduling

- Process cannot be stopped by other processes
- CPU non-preemptive or cooperative scheduling decisions may take place under the following circumstances:
    - When a process switches from the running state to the waiting state
    - When a process terminates
- There is no choice in terms of scheduling. A new process (if one exists in the ready queue) must be selected for execution
- CPU has been allocated to a proces, the process keeps the CPU until it releases the CPU either by terminating or by switching to the waiting state
- This method was using in Windows 3.x

### Preemptive Scheduling

- When a new process with higher priority arrives, the running may be stopped
- CPU preemptive scheduling decisions may take place under the following circumstances:
    - When a process switches from the running state to the ready state (e.g. when an interrupt occurs)
    - When a process switches from the waiting state to the ready state (e.g. completion of I/O)
- There are choices in terms of scheduling
- It requires the special hardware (for example, a timer) needed for preemptive scheduling
- Windows 95 and greater, and macOS use preemptive scheduling

## Scheduler

Schedulers are special pieces of system software which handle process scheduling in various ways. Their main task is to select the jobs 
to be submitted into the system and to decide which processes to run.

There are three types of scheduler:

- **Long term scheduler**: It is the decision of long term scheduler that how many processes will stay in the ready queue. Long term schedulers decide the degree of multiprogramming of the system.
- **Medium term scheduler**: Most often, a running process needs I/O operationg which does not require CPU. Hence during the execution of a process when an I/O operation is required then the operating system sends that process from the running queue to the waiting queue. When a process completed its I/O operation then it should again be shifted to ready queue. All these decisions are taken by the medium term scheduler.
- **Short term scheduler**: When there are lots of processes in main memory initially all are present in the ready queue. Among all the processes, a single process is to be selected for execution. This decision is handled by the short term scheduler.

## Dispatcher

- A dispatcher is a special program which comes into play after the scheduler
- When the scheduler completes its job of selecting a process, it is the dispatcher which takes that process to the desired state/queue
- The dispatcher is the module that gives a process control over the CPU after it has been selected by the short-term scheduler
- This function involves the following:
    - Switching context
    - Switching to user mode
    - Jumping to the proper location in the user program to restart that program
- Once the scheduler has selected a process from the queue, the dispatcher comes into the picture, and it is the dispatcher who takes that process from the ready queue and moves it into the running state

## Scheduling Criteria

- **CPU utilisation**: Keep the CPU as busy as possible
- **Throughput**: Number of processes that complete their execution per unit time
- **Turnaround time**: Amount of time to execute a particular process
    - Turnaround time = Exit time - Arrival time
- **Waiting time**: Amount of time a process has been waiting in the ready queue
    - Waiting time = Turnaround time - Burst time
- **Response time**: Amount of time it takes from when a request was submitted until the first response is produced, not output (for time-sharing environment)

## Scheduling Algorithms

CPU scheduling deals with the problem of deciding which of the processes in the ready queue are to be allocated the CPU.

There are many different CPU scheduling algorithms. The main 6 of these include:

- First-Come, First-Served Scheduling (FCFS)
- Shortest-Job-First Scheduling
- Priority Scheduling
- Round-Robin Scheduling
- Multilevel Queue Scheduling
- Multilevel Feedback Queue Scheduling

### First-Come, First-Served Scheduling (FCFS)

- The process that requests the CPU first is allocated the CPU first
- Managed with First In First Out (FIFO) queue
- When a process enters the ready queue, its PCB (Program Control Block) is linked onto the tail of the queue. When the CPU is free, it is allocated to the process at the head of the queue. The running process is then removed from the queue
- Once the CPU has been allocated to a process, that process keeps the CPU until it releases the CPU, either by terminating or by requesting I/O

#### Example

![FCFS Example](/img/arch-op/y1/scheduling-fcfs.png)

If $P_1$ were to arrive last, the average waiting time would be much shorter.

#### Summary

- Offers non-preemptive scheduling algorithm
- Jobs are always executed on first-come, first-serve basis
- It is easy to implement and use
- However, this method is poor in performance, and the general wait time is quite high

### Shortest-Job-First Scheduling

- The process with the shortest execution time should be selected for execution next
- SJF is optimal: it gives minimum average waiting time for a given set of processes
- The difficulty is knowing the length of the next CPU request

#### Example - Non Preemptive

![SJF Example](/img/arch-op/y1/scheduling-sjf.png)

#### Example - Preemptive

- The choice arises when a new process arrives at the ready queue while a previous process is still executing
- The next CPU burst of the newly arrived process may be shorted than what is left of the currently executing process
- A preemptive SJF algorithm will preempt the currently executing process, whereas a non preemptive SJF algorithm will allow the currently running process to finish its CPU burst

![SJF Preemptive Example](/img/arch-op/y1/scheduling-sjf-preemptive.png)

#### Summary

- Can be preemptive or non-preemptive
- It significantly reduces the average waiting time for other processes awaiting execution
- When the CPU is available, the next process or job with the shortest completion time will be executed first
- Useful for batch-type processing, where waiting for jobs to complete is not critical
- It improves job output by offering shorter jobs, which sould be executed first, which mostly have a shorter turnaround time

### Priority Scheduling

- A priority number (integer) is associated with each process
- The CPU is allocated to the process with the highest priority (smallest integer = highest priority)
- SJF is priority scheduling where priority is the inverse of predicted next CPU burst time
- This algorithm is used for both non preemptive and preemptive scheduling
    - A **non preemptive** priority scheduling algorithm will simply put the new process at the head of the ready queue
    - A **preemptive** priority scheduling algorithm will preempt the CPU if the priority of the newly arrived process is higher than the priority of the currently running process

#### Example - Non Preemptive

![Priority Example](/img/arch-op/y1/scheduling-priority.png)

#### Example - Preemptive

![Priority Preemptive Example](/img/arch-op/y1/scheduling-priority-preemptive.png)

#### Summary

What is the main problem with priority scheduling?

- **Starvation** or **Indefinite Blocking**: A process that is ready to run but waiting for the CPU can be considered blocked. A priority scheduling algorithm can leave some low-priority processes waiting indefinitely. In a heavily loaded computer system, a steady stream of higher-priority processes can prevent a low-priority process from ever getting the CPU.

What is the solution?

**Aging**: Aging involves gradually increasing the priority of processes that wait in the system for a long time. For example, if priorities range from 127 (low) to 0 (high), we could increase the priority of a waiting process by 1 every 15 minutes.

### Round-Robin Scheduling

- The Round-Robin (RR) scheduling algorithm is designed especially for time-sharing systems. It is similar to FCFS scheduling, but preemption is added to enable the system to switch between processes
- Each process gets a small unit of CPU time (time quantum or time slice), usually 10-100 ms. After this time has passed, the process is preempted and added to the end of the ready queue
- The ready queue is treated as a circular queue and FIFO queue of processes
- The CPU schedular goes around the ready queue, allocating the CPU to each process for a time interval of up to 1 time quantum
- No process is allocated the CPU for more than 1 time quantum in a row (unless it is the only runnable process)
- In the round-robin algorithm, two things will happen:
    - The process may have a CPU burst of less than 1 time quantum. In this case, the process itself will release the CPU voluntarily. The scheduler will then proceed to the next process in the ready queue
    - If the CPU burst of the currently running process is longer than 1 time quantum, the timer will go off and will cause an interrupt to the operating system. A context switch will be executed, and the process will be put at the tail of the ready queue. The CPU scheduler will then select the next process in the ready queue
- RR performance:
    - Large time quantum -> FIFO
    - Small time quantum -> Context switch overhead is too high

#### Example

![RR Example](/img/arch-op/y1/scheduling-rr.png)

### Multilevel Queue Scheduling

- The ready queue is partioned into separate queues, e.g:
    - Foreground (interactive) processes
    - Background (batch) processes
- These two types of processes have different response-time requirements and so may have different scheduling needs
- The processes are permantently assigned to one queue, generally based on some property of the process, such as memory size, process priority, or process type
- Each queue has its own scheduling algorithm, e.g.:
    - Foreground: RR
    - Background: FCFS
- Scheduling must be done between the queues:
    - Fixed priority scheduling (i.e. serve all from foreground then background). Possibility of starvation:
        - No process in the batch queue, for example, could run unless the queues for system processes, interactive processes, and interactive editing processes were all empty. If an interactive editing process entered the ready queue while a batch process was running, the batch process would be preempted.
    - Time slice:
        - EAch queue gets a certain amount of CPU time wihwhich it can schedule amongst its processes, i.e. 80% to foreground in RR, 20% to background in FCFS

![Multilevel Scheduling Queues](/img/arch-op/y1/scheduling-multilevel-queues.png)

### Multilevel Feedback Queue Scheduling

- A process can move between the various queues (they are not permantently assigned to a queue), aging can be implemented this way
- Multilevel-feedback-queue schedulers defined by the following parameters:
    - The number of queues
    - The scheduling algorithms for each queue
    - The method used to determine when to upgrade a process
    - The method used to determine when to demote a process
    - The method used to determine which queue a process will enter when that process needs service

![Multilevel Feedback Queue Scheduling Example](/img/arch-op/y1/scheduling-multilevel-feedback-queue.png)
