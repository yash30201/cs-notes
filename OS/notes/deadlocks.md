# Deadlocks


## What is dead lock?

If you don't even know this at this moment of time, then your situation is pretty bad. Speed up!!


### Conditions for deadlock to occur

+ Mutual Exclusion
+ Hold and wait => process should be able to request for more resources after holding a resource
+ No pre emption
+ Circular waiting

    One of the classic examples of deadlock is dining philosopher problem.


> There is a subtle difference between deadlock prevention and deadlock avoidance. Prevention means using an algo such that deadlock can never happen. Avoid means checking is this particular resource allocation can result in deadlock or not then assigning the resource.

> There is a lock called **Livelock**

Real world example of deadlock prevention : <br>
DBMS

Real world example of deadlock avoidance : <br>

The Unix file locking system lockf has a deadlock detection mechanism built into it. Whenever a process attempts to lock a file or a record of a file, the operating system checks to see if that process has locked other files or records, and if it has, it uses a graph algorithm similar to the one discussed above to see if granting that request will cause deadlock, and if it does, the request for the lock will fail, and the lockf system call will return and errno will be set to EDEADLK.


> Multithreaded programs are more prone to deadlocks as they compete for shared resources.


## Some important algos : 

### Banker's Algorithm

Banker's algo is an deadlock avoidance algorithms. 

> Why is is named banker's ? <br> Because this represents the situation when multiple people are taking loan from bank having limited money.

> This class of algo is called Resource-request algorithm.


### Ostrich Algorithm

Just like an Ostrich, which buries its head in earth when senses danger, just ignore deadlock handling hoping that it will not happen.

> Scientists all over the world believe that the most efficient method to deal with deadlock is deadlock prevention. But the Engineers that deal with the system believe that deadlock prevention should be paid less attention as there are very less chances for deadlock occurrence. 

