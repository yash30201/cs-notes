# Thread Concept

Thread is an execution unit that consists of its own program counter, a stack and a set of registers.

They are light weight processes sharing same code base, data and files that of the parent process.

There is no existence of threads beyond being a child of a process.

Single threaded vs multi-threaded process

![single threaded vs multi threaded process](https://i2.paste.pics/460b66847745597561e47521ff50b780.png)

> Advantages : resource sharing, multi threading => scalability


## Types of threads
<br>

### Kernel Threads

+ Supported by kernel
+ Implemented by OS => OS specific => Complex
+ Hardware support is needed
+ Designed to be independent threads
+ non other blocking threads

### User threads

+ No support from kernel
+ Implemented by users => generic, not os specific => easy to implement
+ No hardware support needed
+ In general, designed to be dependent threads
+ Other blocking threads


<br>

---
<br>

## Multithreading models

    User to kernel

### Many to one

+ This is the default model which kernels use

### One to one

+ Users can create limited number of threads
+ Provided more concurrency.


### Many to Many

+  The many to many model multiplexes any number of user threads onto an equal or smaller number of kernel threads, combining the best features of the one-to-one and many-to-one models.

+ Processes can be split across multiple processors

### Multithreading issues

+ Signal handling - If a process gets a message, should i notify all its threads?
+ Fork() : If a thread is forked, should the parent process and all its threads be copied?
+ Security issues due to extensive sharing of resources.

<br>

---
<br>

> Multi threading is a headache for multi core processors

```cpp
special_object *get_special_object( void ) {
    static special_object *obj = NULL;
    if( obj == NULL ) {
        obj = malloc( sizeof( *obj ) ); /* allocation */
        init_special_obj( obj ); /* initialization */
    }
    return obj;
}
 ```

 > BTW this design type is called **Singleton**

 > This code works perfectly in a single-threaded context, but can fail badly in a multithreaded context.

 > Consider the situation where one thread enters the conditional block because "obj" is NULL and then is interrupted by the scheduler. A second thread calls "get_special_object" and does the allocation and initialization itself, because "obj" is still NULL. When the first thread resumes it will do its own initialization and now you have two distinct copies of the special object floating around. At best this is a resource leak



    Static variables represent global state. That's hard to reason about and hard to test: