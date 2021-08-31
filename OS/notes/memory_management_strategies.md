# Memory management strategies
<br>

Memory management is the process of controlling and coordinating computer memory, assigning portions called blocks to various running programs to optimize the overall performance of the system.

## Why do we use it?

+ To isolate each processes so that they don't interfere with each other.
+ To collect and utilise memories when ever they get freed / unallocated.
+ Allocated proper space to routines asking for it.

<br>

---
<br>

## Memory management techniques

+ Single Contiguous Allocation
+ Partitioned Allocation
+ Paging
+ Segmentation

<br>

---
<br>


## Continuous Memory allocation

### Address translation, base and limit registers

Address space means all the space that the program can touch.

=> To restrict what a program can do, it can be done by restricting what it can touch.

**Base** register holds the smallest legal physical memory location => Starting point

**Limit** register holds the size of the range => Length

<br>

### Dynamic storage problem is solved by

+ Best fit => find most tight bounded solution
+ Worst fit => Find most unbounded solution
+ First fit => Find first solution where we can fit.

<br>

---
<br>

## Internal vs External Fragmentation

### Internal Fragmentation

Main memory is split in mounted sized blocks and this size if bigger than required by a process causing internal fragmentation(wastage) of memory within block.

<br>

### External Fragmentation

Main memory has enough space to accommodate the program but its split in non contiguous manner resulting in un-fulfilment of request.

<br>

---
<br>

## Swapping

As name suggests, swapping from main memory(ram) to backing store(hard disk or something other).

Swapping in => To main memory from disk

Swapping out => From main memory to disk

### Benefits

+ High degree of multi programming
+ Allows dynamic relocation
+ Better utilisation of memory
+ Minimum wastage of CPU time

### Disadvantages

+ Context switching time by swapping is very high.
+ **OS can't swap process which is waiting for I/O.**

<br>

---
<br>

## Paging
<br>

Paging is a Memory Management Technique. The Concept 'Paging' is used to remove External Fragmentation.

In this, the Main Memory is divided into parts called as 'Frames' and the process is divided into 'Pages' so that a part of process(a page) can be accommodated in a frame(part of Main Memory).

A Page Table keeps track of the pages and where they are present in the Main Memory.

> **The frames need not be contiguous**.

<br>

![page_table](https://i2.paste.pics/f79ee08674b3aa4ea252878fa8a0312a.png)

> In older OS, page table was kept in secondary memory, thus during context switch, hardware PT has to be loaded with user PT(requiring more time!)

> But in new OS, PT is kept in main memory thus no need to load registers.

For logical address, CPU lets MMU handle and point to the physical memory location but incase of page, Page table holds the physical memory location.

### Advantages

+ Size of process independent of page size
+ No external fragmentation

### Disadvantages
+ **Internal fragmentation** : as page size if fixed even if a process is much smaller in size than that of page

> Each process is allocated a page table.<br>
A **page table base register** (PTBR) points to the page table.<br>
**Changing the page table requires just changing the value of the register, thus reducing the context switch time.**

### Transition look-aside buffer(TLB)

It is a dedicated hardware between CPU and page table for fast access and searching.

Hit ratio = *Ratio that a given page entry exists in TLB*

Note, if it doesn't exits, then CPU again access the Page table memory to retrieve and then add entry in TLB, thus two times memory access

Hence,

Effective access time = h * (t<sub>tlb</sub>+ t<sub>mem</sub>) + (1 - h) * (t<sub>tlb</sub> + t<sub>mem</sub>)

    where,<br>
    Hit ratio = h<br>
    TLB access time = t<sub>tlb</sub><br>
    Memory access time = t<sub>mem</sub>

<br>

### Paging increases context switch time

The operating system must keep track of each individual process's page table, updating it whenever the process's pages get moved in and out of memory, and applying the correct page table when processing system calls for a particular process. This all increases the overhead involved when swapping processes in and out of the CPU. ( The currently active page table must be updated to reflect the process that is currently running. )


<br>

---
<br>

## Paging vs Segmentation

> Both are non contiguous memory allocation scheme

In paging, data is retrieved in the form of chunks of fixed data called **pages** and main memory is divided into small fixed size blocks of physical memory called **frames**.
> Frame's size should be kept same as that of a page(or greater) to have maximum utilisation and avoid external fragmentation.

Where as in segmentation, segments are of variable-length. Segment map us used for managing this.

<br>

## Memory Allocation

Main memory is divided into two types of partitions : 

1. Low memory : OS resides here
2. High memory : User processes are help in high memory

<br>

---
<br>

## Dynamic loading and linking

### Dynamic Loading 

Here, sub routines of a program are not loaded until the program calls it.<br>
All the subroutines are contined in a disk in a relocatable format.

<br>

### Dynamic Linking

Linking is a method which helps OS to collect and merge various system modules of code and data into a single executable file.

In this, its done dynamically.

<br>

### Comparison between static and dynamic loading

In static, every think happens in compile time. The entire program and subroutines will be linked and compiled without the need of any extrenal module or program.

In dynamic, references are provided and the loading is done at the time of execution. Routines are loaded only when they are required.

<br>

### Comparison between static and dynamic linking

Static => when all the other dependency modules are linked into a single executable file at compile time, thus no runtime dependency.

Dynamic => Already know


> **Segmented memory is the only memory management method that does not provide the user’s program with a linear and contiguous address space.**

<br>

---
<br>

<!-- First read VIrtual memory than see "What is Tlb miss" -->





