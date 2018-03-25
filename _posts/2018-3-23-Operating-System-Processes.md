---
layout: post
title: Operating System - Processes
comments: true
# other options
---

In general process is a program in execution. When a system boots up many processes are started which are unknown to user. One of those processes can be to check whether new mail has been received or not if the user had installed mail client and so on. In any multiprogramming system the __CPU__ *switches* between multiple processes running them quickly for 10 or 100 milliseconds giving an illusion that it is running multiple processes which is generally referred as __*pseudoparallelism*__ for a single core processor. In this post we will be discussing about process in detail in __Linux__ context [1].

As the CPU switches back and forth among the processes. It is suggested that while writing programs we should avoid making built-in assumptions about timing. This is because the rate at which a process is executed and rate at which it's computation is done need not be same same accross multiple runs of the same program. Also, if the same program is run twice it is treated as two different process but it is upto the operating system implementation whether to share the code between them or not [1].

## Process Creation

The following are the events that could cause creation of processes.

* System Initialization
* Process creation system call (__fork__ system call in Linux) by a running process
* User request to create a new process

During System Initialization several processes are created. Some of them are called as foreground processes which interact with user others are called as bachground processes which donot interact with user directly. These background processes could be __systemd__ which is a init process in __Linux__ and is a root of process tree structure and is also an example of daemon process i.e which runs in the background.

Also if webserver is running on a system it could *fork* a process to handle new incoming request. If a process calls *fork* system call both parent and child process shares same text segment but child process gets a seperate copy of data, stack, heap segments. In somecases, the child process could execute __execve__ system call which would change the memory image and execute a new program. In some __UNIX__ implementations the parent and child process instead of sharing only the text segment could share entire memory space in such case memory is shared on __copy-on-write__. If either of them wants to modify memory that chunk of memory is copied first and then changes are made so that such changes are relected only to that particular process. So, here writable memory is not shared [1].

For more information regarding creation of process using __fork__ system call and address space refer [Process Address Space](https://github.com/SvrAdityaReddy/RTOS/tree/master/Assignment_3/address_space_process)

## Process Termination

A process can be terminated because of following conditions [1]

* Normal exit
* Error exit
* Fatal error
* killed by another process

When a process had completed it's execution it would execute the system call __exit__. An error exit would occur is that if certain parameters provided to a process are invalid. A fatal error would occur if *divide by zero* occurs during the execution of process. A process can be killed by another process having certain privileges using __kill__ sytem call in __UNIX/Linux__.

## Process States in Linux

Here *process* is referred to as *task* and these terms are often interchangeable.

![_config.yml]({{ site.baseurl }}/images/process_states_linux_ibm.gif)

* __TASK_RUNNING:__ The process is either running on CPU or waiting in a run queue to get scheduled [2].

* __TASK_INTERRUPTIBLE:__ The process is sleeping and is waiting for an event to occur. The process is open to be interruptible by signals. On interrupted by signals or wake-up call it goes to __TASK_RUNNING__ state [2].

* __TASK_UNINTERRUPTIBLE:__ This state is similar to __TASK_INTERRUPTIBLE__ state except that here process is not open to process signals it received. Because it might not be correct to interrupt the process as it might be in the middle of completing some important task. If the event it is waiting for had occured it has to be explicitly waken up by wake-up call [2]. 

* __TASK_STOPPED:__ In this state process is stopped. This state would occur if process receives signals like __SIGSTOP__. The process is runnable on receipt of __SIGCONT__ signal [2].

* __EXIT_ZOMBIE:__ The process arrives this state when the process has terminated and is waiting for the parent process to collect it's exit status which is busy somewhere else [2].

* __EXIT_DEAD:__ This is the final state of process [2].

## Implementation of Processes

The operating system maintains a *process table* or *program control block (PCB)* to store the information like status of opened files, program counter, stack register, memory allocation, process state for each process [2].

For each I/O class there is a location called __interrupt vector__ which contains the address of the interrupt service procedure. Suppose an interrupt occurs when a process is in execution the following steps are followed [2]

1. Hardware stacks program counter, etc.
2. Hardware loads new program counter from interrupt vector.
3. Assembly-language procedure saves registers.
4. Assembly-language procedure sets up new stack.
5. C interrupt service runs (typically reads and buffers input).
6. Scheduler decides which process is to run next.
7. C procedure returns to the assembly code.
8. Assembly-language procedure starts up new current process.

## References

[1] Tanenbaum, Andrew S. *Modern operating system*. Pearson Education, Inc, 2009. <br>
[2] Avinesh Kumar *TASK_KILLABLE: New process state in Linux*,  https://www.ibm.com/developerworks/linux/library/l-task-killable/

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->