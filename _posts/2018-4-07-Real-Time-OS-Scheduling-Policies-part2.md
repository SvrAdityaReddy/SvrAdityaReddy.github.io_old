---
layout: post
title: Real Time Systems - Scheduling Mechanisms - II
comments: true
# other options
---

In this post we are going to discuss Clock Driven Scheduling mechanism which is used in Real Time Systems in detail.

## Clock Driven

As discussed in the earlier [post](https://svradityareddy.github.io/Real-Time-OS-Scheduling-Policies-part1/) this is also known as Time Driven scheduling. This is usually used in "Hard Real Time Systems". But in this approach the parameters of the job has to be known in advance. This approach works well when the execution time of the job is well known and is stable i.e the variance between two successful execution times of same job is very minimal.