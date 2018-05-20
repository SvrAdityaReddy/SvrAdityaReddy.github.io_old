---
layout: post
title: Operating System - Scheduling Policies in General
comments: true
# other options
---

__PROCESS SCHEDULING__: When the CPU becomes idle, the operating system must select one of the processes in the ready queue to be executed. This is done by CPU scheduler. The scheduler selects a process that is in memory that are ready to execute and allocates the CPU to that process.

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

* __CPU UTILIZATION__:  We want to keep the CPU as busy as possible.
* __THROUGHPUT__: Number of processes that are completed per time unit.
* __TURN AROUND TIME__:  The difference in time at which the process is submitted and time at which the process has completed its execution is known as “Turnaround time”.
* __WAITING TIME__:  It is the amount of time spent by the process waiting in the ready queue.
* __RESPONSE TIME__: It is the time from the submission of a request until the first response is recorded.

__SCHEDULING ALGORITHMS__

* __FIRST COME FIRST SERVE (FCFS)__: It is a Non- preemptive policy. According to this the process that requests the CPU first is allocated the CPU first. This can be easily implemented by FIFO queue.
* __SHORTEST JOB FIRST (SJF)__: It is a Non- preemptive policy. When the CPU is available, it is assigned to the process that has the smallest next CPU burst. If there is a tie then FCFS comes in to the action.
* __PRIORITY SCHEDULING__: It can be both Preemptive and Non- preemptive. Problem in priority scheduling is a process of lowest priority can indefinitely be blocked. This is known as “Starvation”. One solution is “Aging”. It involves increasing priority of the process that has been waiting for the CPU for long time.
* __ROUND-ROBIN__: It is a Preemptive policy. It is similar to FCFS scheduling, but preemption is added. A small unit of time, called “time quantum” or “time slice” is defined. Here ready queue is treated as Circular queue. At the end of each quantum in general “dispatcher” is called.
* __MULTI LEVEL QUEUE SCHEDULING__:
It has several queues. A process is assigned into one of the queues depending on some property/criterion. Each queue has priority. A process in lower priority queue will get a chance only if queues having high priority than this has no processes to be executed.
Or there has to be some mechanism to decide when will one queue has to be choosed over the other.
MULTI LEVEL FEEDBACK QUEUE:This is same as multi-level Queue but when a process enters a system is added to the highest priority queue. Then it can be depromoted to lower priority queue or promoted to higher priority queue if available or maintained in the same queue.
MULTI-PROCESSOR SCHEDULING:
	ASYMMETRIC MULTIPROCESSING: Single processor does scheduling decisions, I/O processing and other system activities. This reduces the need for data sharing.
	SYMMETRIC MULTIPROCESSING:  Here each processor is self-scheduling.
PROCESSOR AFFINITY:
When a process has been running on a specific processor. The data most recently accessed by the process populate the cache for the processor. If the process migrates the contents of cache must be invalidated for first processor and the cache for the second processor has to be repopulated which is high cost. Solution is “Processor Affinity”.
Two types
	SOFT AFFINITY:
Here operating system will attempt to keep a process on a single processor but it is possible for a process to migrate between processors.
	HARD AFFINITY:
This is stricter. It allows a process to specify a subset of processors on which it may run.
LINUX:
	Completely Fair scheduler
	Real-Time scheduler (FIFO, RR)
Nice values     -20 to +19
Lower nice value indicates a higher relative priority.
Default nice value is zero (0).
0                     99   100                 139
   Real-time                   Normal
PR = 20+NI
