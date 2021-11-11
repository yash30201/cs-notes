# Overview

OS is the intermediary between computer hardware and user of the computer. The purpose of OS is to provide an environment for users to execute programs conveniently and efficiently.

## Services provided by OS
<br>

**Program Execution :**
<br>

**Handling I/O operations :**
<br>

**Manipulation of file system :**
<br>

**Error Detection and handling :**
<br>

**Resource Allocation :**
<br>

**Accounting** (or logging) : 
<br>

**Information and resource protection :**

<br>

---
<br>

## Types of OS
<br>
Not understood clearly, check [this](https://www.geeksforgeeks.org/types-of-operating-systems/) and some youtube tutorial


### Batch OS

In this, there is an intermediate operator which sorts and groups similar jobs into batches before their processing by the CPU.

<br>

### Time-Sharing OS aka multitasking systems

Each task of same/different user is given some time to execute. Each users uses the CPU as a single user for their share of allotted time. The time that each task gets to execute is called quantum.

EG : Unix

<br>

### Distributed OS aka loosely coupled systems

Here various independent units posses their own memory and CPU and communicate with each other via a shared communication network(central OS type). Major benefit ?  A user can access resource not present in its unit.

EG : LOCUS

<br>

### Network OS aka tightly coupled systems

> As each user within network knows all other users configuration compared to independence in distributed os

Here a central server manages data, users, groups, security, applications and other networking functions within the network. These types os OS allows shared access to files, printers, security, applications and other networking functions over a small private network.

EG : Windows server 2008

<br>

### Real-time OS

These OS serve realtime systems where the time interval required to process and respond to inputs are very small(ie, response time is very small)

+ Hard real-time systems : Where time constrains are too strict eg : airbag system.
+ Soft real-time systems : less strict

EG : weapon systems, medical imaging systems

<br>

---
<br>

> SRAM is faster than DRAM, hence used to L2 and L3 cache. [full article](https://www.guru99.com/sram-vs-dram-difference.html)

<br>

> <img src = "../assets/overview/prom_eprom_eeprom.jpg" width = "400" height = "400"></img>

<br>

> Virtualisation vs Containerization => (Virtual Machine vs Docker)<br> => Hardware level virtualisation vs os-level virtualisation <br> [full article](https://www.tutorialspoint.com/difference-between-virtualization-and-containerization)

<br>

> BIOS vs UEFI <br> => Basic I/O sys. vs Unified extended firmware interface.<br>=> Slow, less hardware driver support, less memory support(max 2.1 TB) vs fast, more support, fast boot times, very large memory support(max 9.1 Zeta byte)<br> See full article [here](https://www.howtogeek.com/56958/htg-explains-how-uefi-will-replace-the-bios/)

<br>

> MBR vs GPT<br>=> Master boot record vs GUID partition table<br>=> Old, limited space(2TB max), up to 4 primary partitions vs Modern, very large limit, unlimited partitions, very large nearly unique identifying strings for each partition<br> See full article [here](https://www.howtogeek.com/193669/whats-the-difference-between-gpt-and-mbr-when-partitioning-a-drive/)

<br>

---
<br>

## Important terms to know
<br>

### Compiler and Interpreter
Converts high level language to low level assembly language in one scoop or one line at a time respectively

### Assembler
Converts the assembly code into machine code

### Linker
Links all the different part of the program together for execution by creating an executable machine code.

### Loader
Loads the executable machine code into memory to be executed.

### System call
System call is programmatic way for applications to requests services from the kernel of the OS

<br>

<img src = "../assets/overview/system_calls.png" width = "500" height = "600"></img>

### Kernel
Its the central component of an OS which manages the operations of memory and CPU time. Interfaces between hardware and software processes.

### Application program interface
An application program interface (API) is code that allows two software programs to communicate with each other

### Shell
A shell is special user program which provide an interface to user to use operating system services

### JVM
It is a specification that provides runtime environment in which java bytecode can be executed. Java bytecode is a assembly language of java

### Booting
Booting is a startup sequence that starts the operating system of a computer when it is turned on.<br>In some systems, a simple bootstrap loader fetches a more complex boot program from disk, which in turn loads the kernel.

<br>

---
<br>

## Multi-programming, multi-processing, multi-tasking and multi-threading
<br>

### Multiprogramming
A computer running more than one program at a time (like running Excel and Firefox simultaneously) through context switching


### Multiprocessing
A computer using more than one CPU at a time.

### Multitasking
Its a logical extension of multi-programming as apart from context-switching, it also utilises the concept of time sharing.

### Multithreading 
Multi threading is an execution model that allows a single process to have multiple code segments (i.e., threads) running concurrently within the “context” of that process.

<br>

---
<br>

## Monolithic kernel and Micro kernel

### Monolithic kernel
This kernel is a single large process running entirely in a single address space. All the kernels services exist and execute in kernel address space. There is no provision of user space having less privilege. Eg : Linux

### Micro kernel
It's an approach where core functionality is isolated from system services via user space for core functionality task and kernel space for system related services. They communicate with each other via IPC(Inter process communication)

> Linux is a monolithic kernel

> Windows very monolithic kernal but is desiged to be a modular(like a microkernel) as OS components run in their own private address space.

> macOS is also unix like but combines the feature of a microkernel (Mach)) and a monolithic kernel (BSD).

<br>

---
<br>

## Process upon turning up of computer

![12331](https://user-images.githubusercontent.com/54198301/129674034-9180e547-befd-41d7-8b08-d64109ab1eeb.png)

-> Firstly bios performs POST(Power in self test). This initializes various hardware devices, checks RAM and secondary storages.
-> Secondly, MBR(master boot record), a small program starts when the computer start booting, in order to find the OS in storage, which is generally located in the first sector, first head and first cylinder.


-> If POST is successful, the boot loader(GRUB in linux) loads the OS from the computer into memory.(system kernels and user kernels are loaded)

-> Lastly, in Init check the records for initial system state to be loaded, starts up various various supporting services like drivers. For eg, X server daemon manages mouse, keyboard, and display. Its only after starting this that we see GUI / login screen. 