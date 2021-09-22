# Virtual Memory Management

> Goal of memory management is to allow multiple processes in the memory to allow multiprogramming.

There are many use cases of virtual memories. You can read [here](https://www.tutorialspoint.com/operating_system/os_virtual_memory.htm).

<br>

This is how MMU works!

<br>

![MMU](https://i2.paste.pics/d431ba27385757c85f8f2b0fb9f7e13c.png)

<br>

---
<br>

> Again, Virtual Memory is a section of secondary memory set up to emulate the computer's main memory

Virtual memory is commonly implemented by **demand paging** (also called lazy swapping). And here, when the program references a memory reference not in the main memory, it called **Page Fault.**

In **pure demand paging**, even a single page is not loaded into memory initially. Hence pure demand paging causes a page fault definitely!

**Swap space** : Section of hard disk used for implementing virtual memory.

### Advantages of demand paging
+ Large virtual memory
+ More efficient use of memory
+ There is no limit on degree of multiprogramming.

### Disadvantages of demand paging
+ Process overhead increases


<br>

---
<br>

## Page replacement algorithms

=> which decides which memory pages to swap out, write to disk when page fault occurs.

> Main deciding factor for page replacement algorithms are the time required for I/O completion.

+ **Hit** -> Means page is there in main memory
+ **Miss** -> Means page is not in the main memory

**Reference String** : It is a string of memory references (generated artificially of by tracing a given system)

+ For example, consider the following sequence of addresses − 123,215,600,1234,76,96

+ If page size is 100, then the reference string is 1,2,6,12,0,0

<br>

### FIFO

Simple, oldest one gets removed and **new one takes its place**, not the back of the queue.

> **Bellady's Anamoly** <br> <br> This states that increasing the page size doesn't implies that page faults will decrease.

<br>

### Optimal Page algorithm

**This has the lowest page fault rate of all algorithms.**

Replace the page that will not be used for the longest time in future. If there are many such processes then replace the one that is in memory for the longest time.

Is is possible in real world?

<br>

### LRU

Page which has not been used for the longest time in main memory is the one which will be selected for replacement.


Some more algos

**Least frequently Used(LFU) algorithm**

+ The page with the smallest count is the one which will be selected for replacement.

+ This algorithm suffers from the situation in which a page is used heavily during the initial phase of a process, but then is never used again.

**Most frequently Used(MFU) algorithm**

+ This algorithm is based on the argument that the page with the smallest count was probably just brought in and has yet to be used.


<br>

**Effective memory access time** = p * page_fault_time + (1 - p) * general memory access time

Where, p = probability of a page fault occurring

<br>

---
<br>

## Thrashing


*Page Fault and Swapping: A page fault occurs when the memory access requested (from the virtual  address space) does not map to something that is in RAM. A page must  then be sent from RAM to swap, so that the requested new page can be  brought from swap to RAM. This results in 2 disk I/Os. Now you might know that disk I/Os are very slow as compared to memory access.*


**Thrashing**: Now if it happens that your system has to swap pages at such a higher rate **that major chunk of CPU time is spent in swapping** then this state is known as thrashing. So effectively during thrashing, the CPU spends less time in some actual productive work and more time in swapping.

**In other words we can say that when page fault ratio decreases below level, it is called thrashing.**

This forms a cycle, i.e.

Low CPU utilisation <br>
=> Degree of multiprogramming increases(as new processes come and old are still not completed)<br>
=> More Page faults<br>
=> More swapping<br>
=> Cycle continues<br>
=> Thrashing occurs(as now major chunk of time is spent swapping)<br>
=> Page fault occurs tremendously<br>
=> CPU utilisation decreases sharply<br>


### Causes

Since the disk I/O speed is something which is already fixed, so let's see about other causes.

+ High Degree of multiprogramming
+ Less number of frames available


### Solution

When thrashing occurs, CPU applies either of the two algorithms - <br>

+ Global page replacement algorithm
+ Local page replacement algorithm

### Global page replacement algorithm

+ The paging algorithm is applied to  all the pages of the memory regardless of which process "owns" them.
+ A  page fault in one process may cause a replacement from any process in  memory. 
+ Thus, the size of a partition may vary randomly.

If global page replacement is used, situations worsens very quickly. CPU thinks that CPU utilization is decreasing, so it tries to increase the degree of multiprogramming. Hence bringing more processes inside memory, which in effect increases the thrashing and brings down CPU utilization further down. The CPU notices that utilization is going further down, so it increases the degree of multiprogramming further and the cycle continues.


### Local page replacement 

 + The memory is divided into partitions of a predetermined size for each  process and the paging algorithm is applied independently for each  region. 
 + A process can only use pages in its partition

 In this, a process can only be allocated pages in its own region in memory. If the swaps of a process increase also, the overall CPU utilization does not decrease much. If other transactions have enough page frames in the partitions they occupy, they will continue to be processed efficiently. 


### Solutions

+ Priority based paging algorithm
+ Work set model(it is a strategy)
    +  It starts by looking at how many frames a process is actually using. This defines the locality model.
    + A locality is a set of pages that are actively used together.
    + Locality Model It states that as a process executes, it moves from locality to locality, i.e. the set of pages actively used changes from one set to another set.
    + A program is generally composed of several different localities which overlap.











