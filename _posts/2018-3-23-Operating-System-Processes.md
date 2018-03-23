---
layout: post
title: Operating System - Processes
---

In general process is a program in execution. When a system boots up many processes are started which are unknown to user. One of those processes can be to check whether new mail has been received or not if the user had installed mail client and so on. In any multiprogramming system the __CPU__ *switches* between multiple processes running them quickly for 10 or 100 milliseconds giving an illusion that it is running muliple processes which is generally referred as __*pseudoparallelism*__ for a single core processor. In this post we will be discussing about process in detail in __Linux__ context [1].

As the CPU switches back and forth among the processes. It is suggested that while writing programs we should avoid making built-in assumptions about timing. This is because the rate at which a process is executed and rate at which it's computation is done need not be same same accross multiple runs of the same program. Also, if the same program is run twice it is treated as two different process but it is upto the operating system implementation whether to share the code between them or not [1].</br>

## References

[1] Tanenbaum, Andrew S. *Modern operating system*. Pearson Education, Inc, 2009. 

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->