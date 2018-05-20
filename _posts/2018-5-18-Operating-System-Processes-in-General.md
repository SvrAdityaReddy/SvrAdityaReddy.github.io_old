---
layout: post
title: Operating System - Processes in General
comments: true
# other options
---

A process is a program in execution.
A process has more than program code.
It has the following components.
1.	Text section
2.	Stack
3.	Data selection
4.	Heap

__TEXT SECTION__: Program code + current activity like program counter and contents of processors registers <br/>
__STACK__: Temporary data such as function parameters, local variables (auto, register variables in C), return addresses <br/>
__DATA SECTION__: Global variables <br/>
__HEAP__: Memory allocated during dynamic allocation. <br/>


__PROCESS STATE IN GENERAL__:

__NEW__:   Process is being created. <br/>
__RUNNING__: Instructions are being executed. <br/>
__WAITING__:  Process is waiting for some event to occur/ to complete. <br/>
__READY__:  Process has all resources allocated except C.P.U (i.e) waiting for to be attached to C.P.U <br/>
__TERMINATED__:  Process has finished execution. <br/>

![_config.yml]({{ site.baseurl }}/images/process_states.png)

Each process in an OS is represented by 
Process Control Block (P.C.B)
PCB has the following information about a process
1.	Process State
2.	Program Counter
3.	CPU Registers
4.	CPU Scheduling Information (Priorities, etc.)
5.	Memory- Management Information

__TWO KINDS OF PROCESSES__
* __I/O – BOUND PROCESSES__: Spends more time doing I/O than it spends doing computations
* __CPU-BOUND PROCESS__: generates I/O requests infrequently and uses more of its time doing computations.
 
It is important that the select good mix of I/O bound and CPU bound processes. Because if all are CPU bound, the wait queue will be empty and devices will go unused. If all are I/O bound, the read queue will almost be empty, the CPU utilization will be very less.

__CONTEXT SWITCH__:

When an interrupt occurs or the scheduler wants to run other process the system needs to save the state of current context of running process namely in PCB and loading the state of process to be runned. So, switching CPU to another process requires performing a state save of the current process and a state restore of different process. This is known as “CONTEXT SWITCH”.

__PROCESS CREATION__:

In “Linux”, process can be created by “fork ()” system call.
* fork () returns pid of child process to parent process.
* fork () returns value of “O” to new process created.

__When a parent forks a child process__

Child, parent can have different address spaces with same content copied and starts executing immediately after fork () function call. 

Also, child, parent can have sane address space, create a copy of necessary required when one of them is trying to modify. This is known as “Copy on write”.

Apart from fork(), execlp () replace entire address space with contents of new process that has to be runned.

__PROCESS TERMINATION__:
When a process creates a child process using “fork ()” system call. The parent has to wait for to collect exit status (int status; exit(&status);) of child. If not
* Parent process is busy somewhere else not collected exit status of child process. The entry in process table doesn’t get removed and it becomes “ZOMBIE” process.
* If parent has terminated before child terminates and has not collected child’s exit status then also child’s entry in process table is not removed and it becomes “Orphan” process and get’s attached as child process to “init” process (or) “systemd” daemon process.

__INTER PROCESS COMMUNICATION__:

A process is “independent” if it cannot affect or cannot get affected by the other processes executing in the system
A process is “cooperating” if it can affect or be affected by other processes executing in the system.

__MAINLY TWO FUNDAMENTAL MODES__:
* Shared memory
* Message passing

1) __SHARED MEMORY__:
	A process shares a memory in its address space with other processes.

2) __MESSAGE PASSING__:
	Allows processes to communicated and to synchronize their actions without sharing the same address space.
	send (message)
	receive (message)

In shared- memory systems, system calls are required only to establish shared-memory regions. Whereas message passing systems are typically implemented using system calls.
But as the processing cores increases, the message passing is preferred over shared memory because shared memory suffers from “cache coherency issues”, which arise because shared data migrate among the several caches.

Apart from them there are other IPC mechanisms like follow

__PIPES__: 
* Named pipe.
* Unnamed pipe (ordinary pipes)

__ORDINARY PIPES__:
* Uni directional.
* One process writes to one end of the pipe (write-end) and other process reads from the other end (read-end).

Sampe code in C to implement using ordinary (unnamed) pipes in UNIX SYSTEMS

```C

// ls -l | more

int fd[2];
pipe(fd);
if (!fork()) {  
	// fd[0] = read
	//fd[1]= write
close (fd[])
dup()   // 0= STDIN , 1=STDOUT
//write (fd)
execlp (“ls”,”ls”,”-1”,NULL);
}
else {
close (fd[0])
dup(0)
execlp (“more”,”more”,NULL);
}
```


## References

[1] Silberschatz, Abraham, Peter Baer Galvin, and Greg Gagne. *Operating system concepts essentials.* John Wiley & Sons, Inc., 2014. <br>

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->
