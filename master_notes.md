# General OSTEP notes

Big three pieces: Virtualization, Concurrency, Persistence 

*projects* https://github.com/remzi-arpacidusseau/ostep-projects

*goal* get good at writing systems programs using C on UNIX based OS

## Operating System
OS is to make the system easier to use.
Allows programs to have their own virtual memory, address space etc...
These virtualizations let the running programs share physical resources (memory, CPU, etc...)

OS comes with a standard library of system calls (API to use)

*What and OS actually does*
It takes physical resources, such as a CPU, memory, or disk, 
and virtualizes them.
It handles tough and tricky issues related to concurrency.
And it stores files persistently, thus making them safe over the long-term. 

### Processes
*Address Space*

*KEY IDEA* -> a running program has it's *own* address space

"as far as the running program is concerned, it has physical memory all to itself"
~ https://pages.cs.wisc.edu/~remzi/OSTEP/intro.pdf


### Concurrency
Running multiple programs at once
parallelism: literally at the same time on different cores 
concurrency: Interleaving programs to run 'at the same time'
*pthread* -> the 'p' stands for POSIX: read as 'posix thread'

Can lead to data races
    - like our example of incrementing a counter that is shared between two threads
    - both threads load the value from memory into a register, increment the value, then write back to memory. However when doing so they will sometimes overwrite each other. 
    - ex: say we have two threads thread1 and thread2 (thread handlers), and thread1 loads counter from memory and it is 50, then this program is paused to go run thread2 (or even at the exact same time in parallel), thread2 loads the same value of 50 for counter, they both increment, then BOTH write back to memory that the value of counter is now 51! The overwriting and data race here will cause some of the increments to be lost 

### Persistence
"The file system is the part of the OS in charge of managing persistent data"