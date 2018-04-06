---
layout: post
title: Real Time Systems - Scheduling Mechanisms - I
comments: true
# other options
---

In this post we will be discussing three broad categories of scheduling mechanisms in Real-Time Systems briefly. They are

* Clock Driven 

* Weighted Round Robin

* Priority Driven




## __Clock Driven__

This is also known as Time Driven scheduling. This is usually used in "Hard Real Time Systems". But in this approach the parameters of the job has to be known in advance. This approach works well when the execution time of the job is well known and is stable i.e the variance between two successful execution times of same job is very minimal.

## __Weighted Round Robin__

This is similar to standard "Round Robin Approach" in General purpose operating systems. But priority i.e higher time slice in general is given to those jobs who actually are in need.

## __Priority Driven__

In this mechanism the jobs are assigned priority depending on certain criterion and scheduled to be executed based upon the priority. The following are some of the criterion which we can use in assigning priority to a job. They are

* __Earliest Deadline First (EDF)__

    Here jobs which are are having earliest deadline are assigned highest priority.
    
* __Lowest Release Time (LRT)__

    Here Release time refers to the time by which a job is ready for execution/scheduling. Jobs having the lowest release time are assigned highest priority.

## __Comparison between Clock Driven and Priority Driven__


| **Clock Driven** | **Priority Driven** |
| ----------|--------|
| Here we need to know the release time, deadline, execution time of the job while designing it | Here we need to know the priority of the job |
| Suitable for Hard Real Time Systems  |  Not suitable for Hard Real Time Systems
| Not Suitable for application with varying time and resource requirements | Suitable for application with varying time and resource requirements |
| Timing Behaviour is deterministic | Timing Behaviour is non-deterministic |
{:.mbtablestyle}
