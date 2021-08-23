# Process scheduling

> Why do we need process scheduling ? <br>
<br>
Process scheduling is an OS task that manages and schedules processes of different states like ready, running and waiting.<br> The reason to use this is to keep the CPU busy at all times => max utilisation and minimum response time for programs.

<br>

*The execution of processes consists of **CPU bursts** and **I/O bursts**, starting and ending with CPU bursts*

<br>

> CPU scheduler is invoked when process changes state or terminates.

<br>

---
<br>

## CPU scheduler

<br>

### Pre-emptive scheduling
Here, a process can be forced to leave CPU and switch to the ready state.

#### Advantages 
+ One process cannot monopolize the CPU
+ Improvises the average response time
+ CPU utilisation increases

#### Disadvantages
+ High computational resources needed
+ Time consumption in context switching


### Non pre-emptive scheduling
Here, a process keeps the CPU until its execution terminates to switches to waiting state.

#### Advantages
+ Offers high throughput(as its number of tasks done per unit of time)
+ Less computational resources needed for this scheduling

#### Disadvantages
+ Can lead to starvation
+ Bugs can cause machine to freeze up
+ Real-time scheduling difficult
+ Poor response time

<br>

---
<br>

## Dispatcher

A dispatcher is a module responsible switching the CPU from one process to another process selected by the scheduler.

Its steps are : 
+ Switching context
+ Switching to user mode (as previous process might have been in kernel mode)
+ Jumping to the appropriate memory locations in the user program

    *A module is a program that contains one or more routines.*

The time taken to stop a process and start another is called **dispatch latency**.


<br>

---
<br>

## Scheduling criteria(key terms)
<br>

**CPU utilisation** : Measured in percentage

**Throughput** : Number of processes completed per unit time

**Turnaround time** : The sum of time spent by process from submission to completion

This includes time for:
+ Waiting to get into memory
+ Waiting in ready queues
+ Waiting in waiting queue(I/O)
+ CPU burst time

**Response time** : Time from submission to first response <br>
*Variance in response time should be minimal*

**Waiting time** : Time spent in the ready queue(as waiting for I/O is independent of scheduling)


<br>

---
<br>

## Scheduling algorithms

### First come first-served scheduling

Needs no explanation.

+ High average response time
+ **Convoy effect** : Several small processes may need to wait if a large proces is given to the CPU

<br>

### Shortest job first

+ process with the smallest next CPU burst is selected
+ FCFS to break ties

> It's ore-emptive version is Shortest remaining time first

<br>

### Priority scheduling

+ CPU allocated to process with highest priority.
+ May be Pre-emptive or not(depends upon we allow current process to finish its execution or not)

> **Ageing** : Gradual increase in the priority of process waiting for a long time

> **Priority inversion** : A low-priority process get the priority of a high priority process waiting for it.

<br>

### Round robin scheduling

+ Each process is only allowed to run for 1 time quantum(a small time)
+ IF time quantum is too small, then this behaves like multi tasking(processor sharing)
+ If time quantum is too large, this behaves like FCFS
+ Pre-emptive
+ New processes and head processes run for more than 1 quantum are added to the tail.
+ Rule of thumb : *0% CPU bursts should be shorter than the time quantum

<br>

### Multilevel queue scheduling

> **Interactive** => Foreground processes

> **Batch** => Background processes

+ There are different queues for different types of processes like system processes, batch processes and interactive processes
+ Their relative priority is system > interactive > batch.
+ A process is permanently assigned to one of the queues.
+ Scheduling among queues - 
    + Fixed priority pre-emptive scheduling method => no process in the batch queue(queue 3) can run unless queue 1 and 2 are empty
    + Time slicing (like multi tasking)

<br>

### Multilevel feedback queue scheduling

- allows processes to move between queues
- inter-queue scheduling: preemptive priority scheduling
- a process waiting too long in a low-priority queue may be moved to a high-priority queue



