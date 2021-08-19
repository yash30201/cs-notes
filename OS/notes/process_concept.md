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
They are segment of a process => processes can have multiple threads.

They only have 3 states - running, waiting and blocked

They share memory, this are not completely isolated.

<br>

---
<br>

## Process scheduling
<br>

There are 3 types of queues : 
+ Job queue
+ Ready queue
+ Device queue

> These are implemented using **Linked List**

<br>

The task of managing the processes to be loaded, running and waiting by process scheduler is called process scheduling

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

