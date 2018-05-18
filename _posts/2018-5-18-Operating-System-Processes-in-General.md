---
layout: post
title: Operating System - Processes in General
comments: true
# other options
---

A process is a program in execution.
A process has more than program code.
It has the following components.
1.	Text section
2.	Stack
3.	Data selection
4.	Heap
TEXT SECTION:
* Program code + current activity like program counter and contents of processors registers
STACK:
*	Temporary data such as function parameters, local variables (auto, register variables in C), return addresses 
DATA SECTION:
*	Global variables
HEAP:
	Memory allocated during dynamic allocation.
PROCESS STATE IN GENERAL:
NEW:   Process is being created.
RUNNING: Instructions are being executed.
WAITING:  Process is waiting for some event to occur/ to complete.
READY:  Process has all resources allocated except C.P.U (i.e) waiting for to be attached to C.P.U
TERMINATED:  Process has finished execution.

## References

[1] Silberschatz, Abraham, Peter Baer Galvin, and Greg Gagne. *Operating system concepts essentials.* John Wiley & Sons, Inc., 2014. <br>

<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

<!-- The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. -->
