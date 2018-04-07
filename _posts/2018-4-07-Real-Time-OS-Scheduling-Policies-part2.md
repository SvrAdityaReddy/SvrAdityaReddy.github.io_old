---
layout: post
title: Real Time Systems - Scheduling Mechanisms - II
comments: true
# other options
---

In this post we are going to discuss Clock Driven Scheduling mechanism which is used in Real Time Systems in detail.

## Clock Driven

As discussed in the earlier [post](https://svradityareddy.github.io/Real-Time-OS-Scheduling-Policies-part1/) this is also known as Time Driven scheduling. This is usually used in "Hard Real Time Systems". But in this approach the parameters of the job has to be known in advance. This approach works well when the execution time of the job is well known and is stable i.e the variance between two successful execution times of same job is very minimal.

Let us assume there are N tasks numbered from 0 to N-1 are to scheduled. Each task is denoted by Tk, "k" ranging from 0 to N-1. The pseudo algorithm is as follow.

``` python

def task_scheduler:
    k=0 # initialize k to 0
    i=0
    set_the timer to expire at tk, tk is_the time at which next task
    has to be scheduled.
    i=i+1
    k=i*mod(N) # to calculate k which indicates the next task to be scheduled
    while(1):
        accept_timer_input
        
        if(aperiodic_task_in_execution):
            preempt it
        
        current task T=Tk
        i=i+1 #increment i by 1
        k=i*mod(N) # to calculate k which indicates the next task to be scheduled
        set the timer to expire at [i/N]*H + tk
        
        if(current_task_in_execution_is_Idle_task):
            let the job infront of aperiodic job queue execute
        else:
            allow current task to execute
        
        sleep

```

In the before algorithm we are setting up a timer to interrupt. Instead of it we can can divide the timeline in to frames of frame size "f". "f" can be atleast greater than equal to maximum execution time of tasks. So, here scheduling decison is made at the beginning of each frame. Also, the scheduler has to monitor whether the job that is scheduled to be executed in that frame had been released i.e ready for execution and also to monitor that the job is completed within it's deadline.

If the jobs execution time is too large we have to divide the job into slices inorder to achieve best performance and it would increase context switch time and increases the overhead.