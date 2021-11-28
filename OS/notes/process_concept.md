# Process Concept
<br>

## Process vs Program

> Program <=> Class
<br> Process <=> Object

### Program
It is a passive entity which resides in secondary memory, which can be run to create an instance of program.

### Process
It is a dynamic entity as process is an instance of program running in a computer.

<br>

---
<br>

## States of process in OS

### States

**New** : Process is about to be created form the program residing in secondary memory.

**Ready** : Process has been created and is ready in main memory to be executed by CPU

**Run** : Process is in execution

**Blocked or wait** : Waiting of I/O, needs user Input or needs access to a critical region(which is already on a lock)

**Terminated or Completed** : Process killed as well as PCB(process control block) deleted.

**Suspend ready** : Process was initially ready in main memory but then swapped out of main memory into external storage(virtual memory) by scheduler.

**Suspend wait ot suspend blocked** : The process which was performing I/O operation and lack of main memory caused them to move to secondary memory.
When work is finished it may go to suspend ready.

<br>

### Cpu and IO bound process

**CPU bound** : Process which is intensive in terms of CPU operations(like installation process of an application).

**I/O bound**  : Process which is intensive in terms of I/O operations(like display adapter)

<br>

### Degree of multiprogramming

The number of process that can reside in the ready state at maximum.

<br>

---
<br>

## PCB and process table
<br>

### Process Control Block(PCB)

PCB contains all the necessary information of a process' current state like PID, process state, program counter, stack pointer,registers(accumulator, base, registers and general purpose registers) status of opened files, scheduling algorithms, etc.

> When a process changes state, OS updates the PCB 

<img src = "https://user-images.githubusercontent.com/54198301/130014391-3f325465-8d44-4f8f-afe1-a216353eeab4.jpg" width = "30%" height = "30%"/>

### Process table

The OS maintains pointers to each process's PCB in a process table to access it quickly.

<br>

---
<br>

## How does a process looks in memory

![processimage](https://user-images.githubusercontent.com/54198301/130014924-9c89bab1-ca34-4a6b-985a-ee165f2c6324.jpg)

### Text
This is a read-only section that contains the executable instruction of the program, constants and macros

### Data 
This section contains global and static variables initialised by the program prior to the execution.

### Heap
Stored the dynamically allotted variables during runtime. Grows upwards.

### Stack
Stores temporary data i.e. function parameters, return addresses, and local variables. Grows downwards.

<br>

---
<br>

## Difference between process and thread

![Untitled-Diagram-361](https://user-images.githubusercontent.com/54198301/130015984-494561f5-0939-4d02-8418-89d3bdb50df9.png)

### Process
We already know it..One extra point is process' are isolated and do not share memory with other process

### Threads
Thread is a smallest sequence of instructions in a program which can be managed independently.

<br>

---
<br>

## Process scheduling
<br>

There are 3 types of queues : 
+ Job queue
+ Ready queue
+ Device queue(queue for processes waiting for I/O or locked area)

> These are implemented using **Linked List**

<br>


They are the softwares whose task is to manage the processes running, select new processes and deciding which process to run.

Comparison among long-term, short-term and medium-term scheduler.

> They are three different schedulers with  3 different tasks at different phases of process

Long-term Scheduler | Short-term scheduler | Medium-term scheduler
--- | --- | ---
Job Scheduler | CPU scheduler | Process swapping scheduler
slow speed | fast speed | in between speed
Controls degree of multi programming | lesser control than long term | reduces degree of multiprogramming(as cannot introduce new processes)
Almost absent or minimal in time sharing system(as time is more or less calculated) | Almost minimal in time sharing sys(same reason) | Part of time sharing system
It selects processes from pool and loads them into memory for execution | It selects those processes which are ready to execute | Can pause + remove process from memory to secondary memory and re-introduce the process into memory and execution can be continued.


> Context switching is just saving of CPU state in PCB. To reduce number of switches, some hardware systems employ two or more sets of processor registers.
<br>


The state of CPU to be saved in context switching includes : 
+ Program Counter
+ Scheduling information
+ Base and limit register value
+ Currently used register
+ Changed State
+ I/O State information
+ Accounting information

<br>

---
<br>

## Inter process communication

Inter-process communication (IPC) is a mechanism that allows processes to communicate with each other and synchronize their actions.

Processes can be independent as well as co-operating process(which require some form of inter process communication)

IPC can be done in two ways - 
1) Shared memory
2) Message passing

Shared memory is easy

So see about message passing.

### Message passing
<br>

### Message passing using communication link

> This is called direct message passing

This requires : 

1. Set-up of communication link if not already set-up
2. Start exchanging messages using basic primitives like : 
    1. send(message, destination)
    3. receive(message, host)

Moreover, there can be three configurations for sender and receiver : 

    *Blocking means synchronous and non-blocking means asynchronous*

1. Blocking send and blocking receive
2. Non-blocking send and non-blocking receive
3. Non-blocking send and blocking receive (**most logical and used**)

### Message passing using mailbox messaging

> This method is indirect

+ Receiver creates a mail box
+ At a time, there can be only one receiver
+ Mailbox is associated with a port
+ The sender is non-blocking and sends the message
+ The first process which executes the receive will enter in the critical section and all other processes will be blocking and will wait in the mailbox.


> Windows XP uses message passing using local procedural calls (LPC)

> Client server applications use sockets, RPC or Pipe

<br>

---
<br>

## Pipes

Very simplistic analogy is just a water pipe where sender pours water(message) at one end and receiver collets water(message from other end)

Every pipe requires two descriptors, one connected to read from pipe and one connected to write to the pipe.

Parent process | Child process

```
Write ------>|'''''''''''''''''''|------> Read
             |      Pipe         |
Read  <------|,,,,,,,,,,,,,,,,,,,|<------ Write
```

For two way communication where both sides can simultaneously send and receive messages, it can be implemented simply by Two pipes and sealing one's read and write appropriately

![two way communication](https://i.imgur.com/ck4UxDT.png)


<br>

---
<br>

## Zombie process

These are the processes which have terminated by calling exit() but still have an entry in the process table.

This happens when a child process is created using fork() and then somehow the parent process wasn't able to get child process from process table.

Way to find max number of zombie process so that program will not stop its execution(it differs from system to system along with specifications) : 

```c
#include<stdio.h>
#include<unistd.h>
  
int main()
{
    int count = 0;
    while (fork() > 0)
    {
        count++;
        printf("%d\t", count);
    }
}
```
This is zombie process because we are not managing the child process by storing its PIDs. Its like creating objects and not assigning them to proper variable and since program is running and continuously in causing memory leak.
