---
layout: post
title: Operating System - Processes
---

In general process is a program in execution. When a system boots up many processes are started which are unknown to user. One of those processes can be to check whether new mail has been received or not if the user had installed mail client and so on. In any multiprogramming system the __CPU__ *switches* between multiple processes running them quickly for 10 or 100 milliseconds giving an illusion that it is running muliple processes which is generally referred as __*pseudoparallelism*__ for a single core processor. In this post we will be discussing about process in detail in __Linux__ context. 

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->