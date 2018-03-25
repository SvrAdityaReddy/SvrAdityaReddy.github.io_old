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

## Process Termination

A process can be terminated because of following conditions [1]

* Normal exit
* Error exit
* Fatal error
* killed by another process

When a process had completed it's execution it would execute the system call __exit__. An error exit would occur is that if certain parameters provided to a process are invalid. A fatal error would occur if *divide by zero* occurs during the execution of process. A process can be killed by another process having certain privileges using __kill__ sytem call in __UNIX/Linux__.

## Process States

![_config.yml]({{ site.baseurl }}/images/process_states_linux_ibm.gif)

## References

[1] Tanenbaum, Andrew S. *Modern operating system*. Pearson Education, Inc, 2009. <br>
[2] Avinesh Kumar *TASK_KILLABLE: New process state in Linux*,  https://www.ibm.com/developerworks/linux/library/l-task-killable/

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->