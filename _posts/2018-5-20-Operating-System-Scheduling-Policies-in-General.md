---
layout: post
title: Operating System - Scheduling Policies in General
comments: true
# other options
---

__PROCESS SCHEDULING__: When the CPU becomes idle, the operating system must select one of the processes in the ready queue to be executed. This is done by CPU scheduler. The scheduler selects a process that is in memory that are ready to execute and allocates the CPU to that process. <br/>

“Ready Queue” need not be a “First In First Out (FIFO) Queue”.

Important concept in operating system CPU scheduling is “Preemption”

A “__Preemption__” to a process occurs when an interrupt occurs or when an high priority process wants to execute.

Another important concept is “__Dispatcher__”
It does the following
* Context switch
* Switching to usermode
* Jumping to the proper location in the user program to restart that program

“__Dispatcher__” has to be as fast as possible because it is invoked during every process switch. The time it takes for the dispatcher to stop one process and start another running is known as “Dispatch latency”.

__SCHEDULING CRITERIA__

* __CPU UTILIZATION__:  We want to keep the CPU as busy as possible. <br/>
* __THROUGHPUT__: Number of processes that are completed per time unit. <br/>
* __TURN AROUND TIME__:  The difference in time at which the process is submitted and time at which the process has completed its execution is known as “Turnaround time”. <br/>
* __WAITING TIME__:  It is the amount of time spent by the process waiting in the ready queue. <br/>
* __RESPONSE TIME__: It is the time from the submission of a request until the first response is recorded. <br/>

__SCHEDULING ALGORITHMS__

* __FIRST COME FIRST SERVE (FCFS)__: It is a Non- preemptive policy. According to this the process that requests the CPU first is allocated the CPU first. This can be easily implemented by FIFO queue. <br/>
* __SHORTEST JOB FIRST (SJF)__: It is a Non- preemptive policy. When the CPU is available, it is assigned to the process that has the smallest next CPU burst. If there is a tie then FCFS comes in to the action. <br/>
* __PRIORITY SCHEDULING__: It can be both Preemptive and Non- preemptive. Problem in priority scheduling is a process of lowest priority can indefinitely be blocked. This is known as “Starvation”. One solution is “Aging”. It involves increasing priority of the process that has been waiting for the CPU for long time. <br/>
* __ROUND-ROBIN__: It is a Preemptive policy. It is similar to FCFS scheduling, but preemption is added. A small unit of time, called “time quantum” or “time slice” is defined. Here ready queue is treated as Circular queue. At the end of each quantum in general “dispatcher” is called. <br/>
* __MULTI LEVEL QUEUE SCHEDULING__: It has several queues. A process is assigned into one of the queues depending on some property/criterion. Each queue has priority. A process in lower priority queue will get a chance only if queues having high priority than this has no processes to be executed. Or there has to be some mechanism to decide when will one queue has to be choosed over the other. <br/>
* __MULTI LEVEL FEEDBACK QUEUE__: This is same as multi-level Queue but when a process enters a system is added to the highest priority queue. Then it can be depromoted to lower priority queue or promoted to higher priority queue if available or maintained in the same queue. <br/>

__MULTI-PROCESSOR SCHEDULING__

* __ASYMMETRIC MULTIPROCESSING__: Single processor does scheduling decisions, I/O processing and other system activities. This reduces the need for data sharing. <br/>
* __SYMMETRIC MULTIPROCESSING__: Here each processor is self-scheduling. <br/>

__PROCESSOR AFFINITY__

When a process has been running on a specific processor. The data most recently accessed by the process populate the cache for the processor. If the process migrates the contents of cache must be invalidated for first processor and the cache for the second processor has to be repopulated which is high cost. Solution is “Processor Affinity”.
It is of two types.

* __SOFT AFFINITY__: Here operating system will attempt to keep a process on a single processor but it is possible for a process to migrate between processors. <br/>
* __HARD AFFINITY__: This is stricter. It allows a process to specify a subset of processors on which it may run. <br/>

__Scheduling in LINUX__

* Completely Fair scheduler
* Real-Time scheduler (FIFO, RR)

Nice value is used to assign priority to a process in linux. Nice values ranges from -20 to +19. Lower nice value indicates a higher relative priority. Default priority value assigned to process is zero (0) i.e nice value will be -20. By changing the nice value we can change the priority of a process in Linux. 

Priorities range in Linux is as below.

![_config.yml]({{ site.baseurl }}/images/priority_range_linux.png)

In linux priority is calculated as PR = 20+NI

# References


[1] Silberschatz, Abraham, Peter Baer Galvin, and Greg Gagne. *Operating system concepts essentials.* John Wiley & Sons, Inc., 2014. <br/>
[2] https://askubuntu.com/questions/656771/process-niceness-vs-priority

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->
