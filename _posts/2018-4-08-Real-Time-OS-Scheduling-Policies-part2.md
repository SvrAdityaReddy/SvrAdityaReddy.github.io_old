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

Here aperiodic jobs/tasks refer to jobs which occur at random time and have soft deadlines or no deadlines. Here "H" is the Hyper Period which will be discussed in further coming posts.

In the before algorithm we are setting up a timer to interrupt. Instead of it we can can divide the timeline in to frames of frame size "f". "f" can be atleast greater than equal to maximum execution time of tasks. So, here scheduling decison is made at the beginning of each frame. Also, the scheduler has to monitor whether the job that is scheduled to be executed in that frame had been released i.e ready for execution and also to monitor that the job is completed within it's deadline.

If the jobs execution time is too large we have to divide the job into slices inorder to achieve best performance and it would increase context switch time and increases the overhead.

### Cyclic Executives

This is a slight modification of native Clock Driven Scheduling mechanism discussed earlier. Here also scheduling decisions are made in the beginning of frames and allows aperiodic jobs to use the time not used by periodic jobs.

Let us assume there are F blocks numbered from 0 to F-1. Each block is denoted by Lk, "k" ranging from 0 to F-1. The pseudo algorithm is as follow. Here block refers to a frame.

``` python

def cyclic_executive:
    i=0
    k=0 # refers to frame number
    while(1):
        Accept clock interrupt at time tf # tf is the frame size
        current block = L(k)
        i=i+1
        k=i*mod(F)
        if(last_job_is_not_completed):
            take appropriate action
        wake up the periodic task server to execute slices_in the current block
        sleep until periodic task server completes
        while(aperiodic_jobs_queue_is_not_empty):
            take the job_in the beginning of aperiodic job queue
            sleep until it completes
            remove it_from the aperiodic job queue 
        sleep till_next clock interrupt

```

Since aperiodic jobs are executed when there is no periodic job executed in that frame. The sooner the aperiodic job completes the better will be the response time of the system. So, it is important for Real Time System Designers to design such a way to minimize the average response time.

One approach to increase the response time of system is to use "Slack Stealing". It is a method for scheduling aperiodic jobs. Here in "Slack Stealing" the aperiodic job starts executing from beginning of frame till periodic job that has to be executed has been released in the system.

Apart from periodic jobs, aperiodic jobs there are another set of jobs known as "sporadic jobs". Sporadic jobs occur at random time and have hard deadline. Now, we will be discussing a scheduler whhich schedules sporadic jobs apart from scheduling periodic and aperiodic jobs.
 