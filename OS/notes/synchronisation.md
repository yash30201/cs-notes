# Process Synchronisation

It is required when multiple cooperative process run simultaneously as executions of one process affects the executions of another process. These processes need to be synchronized so that the order of execution can be guaranteed.

+ Process Synchronization is mainly needed in a multi-process system when multiple processes are running together, and more than one processes try to gain access to the same shared resource or any data at the same time.
+ The task phenomenon of coordinating the execution of processes in such a way that no two processes can have access to the same shared data and resources.
+ It is a procedure that is involved in order to preserve the appropriate order of execution of cooperative processes.


**Race condition** : Several processes access and process the manipulations on the same data in a concurrent manner and due to which the outcome depends on the particular order in which the access of data takes place.

<br>

---
<br>

## Critical section problem

Critical section of a process is a code segment that accesses the shared variables and has to executed in atomic manner to prevent any ambiguity.

One process must wait until another finishes its execution of critical section.

### Any solution must satisfy the following 3 conditions : 

1. Mutual exclusion
2. Progress => If no process is in its critical section and any process want to execute its critical section then it must be allowed.
3. Bounded waiting => After a process makes a request fir getting into critical section, there must be a limit for how many other process can get into their critical section.

<br>

### Peterson's solution

This is widely used and software-based solution to critical section problems

```cpp
// Shared variables
    int turn;
    bool flag[N];

// Code for any Pi
    do{
        flag[i] = true; // state that this wants to enter the critical section
        turn = j; // Give chance to another process
        while(flag[j] && turn == j);
        critical section
        flag[i] = false;
        // Give chance to another process that is ready to enter by setting turn
        remainder section
    }while(true);
```

<br>

### Synchronisation hardware

Many systems provide hardware support for critical section code.

+ Its very easy to solve this problem in a single processor environment if we could disallow interrupts to occur while a shared variable is being modified.
+ But this solution is not feasible in a multi-processor environment.
+ As disabling the interrupt is very time consuming an inefficient.


To solve this problem, **Mutex lock** is used.

In this approach, in the entry section of code, a LOCK is acquired over the critical resources modified and used inside the critical section, and in the exit section that LOCK is released.

<br>

> **Advantage of preemptive kernel over non preemptive kernel** <br>
 A preemptive kernel is more suitable for real-time programming, as it will allow a real-time process to preempt a process currently running in the kernel. Furthermore, a preemptive kernel may be more responsive, since there is less risk that a kernel-mode process will run for an arbitrarily long period before relinquishing the processor to waiting processes

<br>

---
<br>

## Semaphores

Semaphores are the integer variables that are used to solve the critical section problem by using two atomic operations, Wait() and Signal().

+ Wait => This decrements the value of argument is its greater than 0.
    ```cpp
    wait(S){
        while(S <= 0);
        S--;
    }
    ```

+ Signal => Increments the value of argument
    ```cpp
    signal(S){
        S++;
    }
    ```

This is how they are used : 

```cpp
// Some code
wait(S);
// critical section
signal(S);
// remainder section
```
<br>

### Types of semaphores

**Counting semaphores** : These are the unbounded integer valued variables whose count is the number of resources available.

**Binary Semaphores** : (aka **Mutex Locks** )Their count is restricted to 0 and 1, thus are easier to implement.

    This doesn't seems dead lock free !

    As there may happen that one process just entered critical section and then gets interrupted by another process which wants to enter critical section. This another process will just wait(S) infinitely.


### Advantages

+ Follows mutual exclusion
+ Machine independent

### Disadvantages
+ Complicated
+ Impractical for large scale
+ Priority inversion may happen

**Busy waiting** : => when process wastes CPU cycles by waiting, which some other process might have been able to use. This type of semaphores are calles **spin lock** as the process spins while waiting for the lock.

<br>

---
<br>

## Implementation of binary semaphore

```cpp
struct semaphore{
    enum value(0, 1);

    Queue<process> q; // Contains the PCBs of processes requesting execution on their respective critical section.
}

wait(semaphore S){ // Runs on entry section
    if(S.value == 1){ //Since no one's occupying, so we can take it.
        S.value = 0;
    }
    else{ // Since occupied, so stand up in queue and sleep
        q.push(P);
        sleep(); // Block the process
    }
}

signal(semaphore S){
    if(S.q.empty()){ // If no queue, then make this free
        S.value = 1;
    }
    else{ // Assign next process 
        process x = q.front(); // => Run process x or unblock the process
        q.pop();
    }
}

```

<br>

---
<br>

## Implementation of Counting semaphore

Now suppose there is a resource whose number of instances is 4. Suppose there are 4 processes P1, P2, P3, P4, and they all call wait operation on S(initialized with 4). If another process P5 wants the resource then it should wait until one of the four processes calls the signal function and the value of semaphore becomes positive.

<br>

---
<br>

## Problem with previous implementation

If one process is in critical section

=> Others wait

=> They continuously check for semaphore value(in If statement), and **waste CPU cycles**!!

Thus, another improvised implementation is as follows - 

```cpp
struct semaphore{
    int value;
    Queue<process> q;
};

wait(semaphore s){
    s.value--;
    if(s.value < 0){
        q.push(p);
        block();
    }
    else return;
}
signal(semaphore s){
    s.value++;
    if(s.value <= 0){
        // remove process from queue
        Process p = q.front();
        wakeup(p);
    }
    else return;
}

// Once a process is blocked, it no longer checks the semaphore until it wakes up!
```
<br>

---
<br>

## Classical IPC problems

### Producer Consumer problem

```cpp
Number of buffers = n
Semaphores –
mutex = 1; //access to buffers
empty = n;
full = 0;
```


This is producer
```cpp
do { // produce an item
    wait (empty);
    wait (mutex);
    // add the item to the buffer
    signal (mutex);
    signal (full);
} while (true);
```


This is consumer
```cpp
do { 
    wait (full);
    wait (mutex);
    // remove an item from buffer
    signal (mutex);
    signal (empty);
    // consume the item
} while (true);
```

<br>

### Dining Philosopher's  problem

Here there are n persons sitting on a round table with n chopsticks(single, not pair) and food at the center. Each need two adjacent chopsticks to their left and right to eat.

```cpp
do { 
    wait (chopstick[i]);
    wait (chopStick[(i+1)%5]);
    // eat
    signal (chopstick[i]);
    signal (chopstick[(i+1)%5]);
    // think
} while (true);
```
But this is deadlock prone!

One solution is, each odd number person will always choose right chopstick first and even numbered will choose left chopstick first.

> Another problem related to this is monitor sharing by processes problem