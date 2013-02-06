OS-Proj_1
=========

Current Ideas:
==

1. Maybe we need to implement a blocked queue list

Initial Test Results
=======

1. pass tests/threads/alarm-single
1. pass tests/threads/alarm-multiple
1. pass tests/threads/alarm-simultaneous
1. FAIL tests/threads/alarm-priority
1. pass tests/threads/alarm-zero
1. pass tests/threads/alarm-negative
1. FAIL tests/threads/priority-change
1. FAIL tests/threads/priority-donate-one
1. FAIL tests/threads/priority-donate-multiple
1. FAIL tests/threads/priority-donate-multiple2
1. FAIL tests/threads/priority-donate-nest
1. FAIL tests/threads/priority-donate-sema
1. FAIL tests/threads/priority-donate-lower
1. FAIL tests/threads/priority-fifo
1. FAIL tests/threads/priority-preempt
1. FAIL tests/threads/priority-sema
1. FAIL tests/threads/priority-condvar
1. FAIL tests/threads/priority-donate-chain
1. FAIL tests/threads/mlfqs-load-1
1. FAIL tests/threads/mlfqs-load-60
1. FAIL tests/threads/mlfqs-load-avg
1. FAIL tests/threads/mlfqs-recent-1
1. pass tests/threads/mlfqs-fair-2
1. pass tests/threads/mlfqs-fair-20
1. FAIL tests/threads/mlfqs-nice-2
1. FAIL tests/threads/mlfqs-nice-10
1. FAIL tests/threads/mlfqs-block
1. 20 of 27 tests failed.

Current Test Results
====

1. pass tests/threads/alarm-single
1. pass tests/threads/alarm-multiple
1. pass tests/threads/alarm-simultaneous
1. FAIL tests/threads/alarm-priority
1. pass tests/threads/alarm-zero
1. pass tests/threads/alarm-negative
1. FAIL tests/threads/priority-change
1. FAIL tests/threads/priority-donate-one
1. FAIL tests/threads/priority-donate-multiple
1. FAIL tests/threads/priority-donate-multiple2
1. FAIL tests/threads/priority-donate-nest
1. FAIL tests/threads/priority-donate-sema
1. FAIL tests/threads/priority-donate-lower
1. FAIL tests/threads/priority-fifo
1. FAIL tests/threads/priority-preempt
1. FAIL tests/threads/priority-sema
1. FAIL tests/threads/priority-condvar
1. FAIL tests/threads/priority-donate-chain
1. FAIL tests/threads/mlfqs-load-1
1. FAIL tests/threads/mlfqs-load-60
1. FAIL tests/threads/mlfqs-load-avg
1. FAIL tests/threads/mlfqs-recent-1
1. pass tests/threads/mlfqs-fair-2
1. pass tests/threads/mlfqs-fair-20
1. FAIL tests/threads/mlfqs-nice-2
1. FAIL tests/threads/mlfqs-nice-10
1. FAIL tests/threads/mlfqs-block
1. 20 of 27 tests failed.



§1.1 Getting Started
-
*Here's what it looks like Project 1 will entail:*

1. Modify Base Kernel in threads/
2. Modify Timer implementation in devices/
3. Try tests in /tests

§1.2 Grading
-
*50% Test Results, 50% Design Quality*

Testing

1. To test everything, run `make src/threads/build/check`
2. To run a single test: `make src/tests/threads/TESTYOUWANT.result`

Design

1. In the end it may be more worth while to make sure the design document is perfect than to spend hours trying to pass that one last test.

2. Copy new or modified `struct`, `struct member`, `global`, `typedef`, `enumeration`, and `static` declarations into the design document, to highlight for us the actual changes to data structures. Identify each's purpose in less than 25 words.

3. Describe the `algorithms` that make the code work

4. Explain how you chose to synchronize this particular type of activity

5. Justify your design decisions, by comparing them to alternatives.

6. The `source code` itself must look good, especially parts that are most relevant to the issues focused on in the project.

7. Add comments to every definition of something

§1.3 Don't Cheat
-
1. You may use public libraries
 * E.g. public classes for queues, trees, etc.
2. You may look at the real Linux implementation (cite the source)

3. You may _not_ look at the code of someone else who completed this project


§2 Project 1: Threads Checklist
===============================

§2.1 Background
-

§2.1.1 Understanding Threads

1. Using the GDB debugger, slowly trace through a context switch to see what happens (see section E.5 GDB). You can set a breakpoint on schedule() to start out, and then single-step from there.(1) Be sure to keep track of each thread's address and state, and what procedures are on the call stack for each thread. You will notice that when one thread calls switch_threads(), another thread starts running, and the first thing the new thread does is to return from switch_threads(). You will understand the thread system once you understand why and how the switch_threads() that gets called is different from the switch_threads() that returns. See section A.2.3 Thread Switching, for more information.

2. Don't declare large data structures as non-static local variables, e.g. int buf[1000];. Alternatives to stack allocation include the page allocator and the block allocator (see section A.5 Memory Allocation).

§2.1.2 Source Files

1. In `init.c/h` you may want to add your own initialization code to main(), see A.1.3 for details

2. Much of your work will take place in `thread.c/h`, see A.2.1, and A.2 for details

3. You will need to modify `synch.c/h`, see A.3 for details

§2.1.2.1 "devices" code

1. You will need to modify `timer.c/h`

§2.1.2.2 "lib" files

1. `kernel/list.c/h` doubly linked list you'll need to use

§2.1.3 Synchronization

1. Read A.3 on Synchronization, and the comments in `threads/synch.c`to figure out what primitives to use in what situation

2. It says interrupt handlers can't sleep, so they can't acqure locks, so disabling them is the only way to allow to synchronously share data with the kernel thread.

    * Why can't interrupt handlers sleep?

3. Use semaphores, locks, and condition variables to solve synch. problems instead of just turning interrupts off

4. Remove debugging code before turning the project in

5. Don't do "busy waiting", e.g. a tight loop of thread_yield()'s

§2.1.4 Development Suggestions

1. E.4 Backtraces will help you to get the most out of every kernel panic or assertion failure, for debugging help when you are very confused.


§2.2 Requirements

§2.2.1 Design Document

1. Each person is responsible for submitting their own design document

    * `turnin -submit tw7877 threads_design threads_design.txt`

2. Probably want to read the template for it early on in starting the project

§2.2.2 Alarm Clock
-

1. Reimplement timer_sleep()

    * defined in devices/timer.c.
    * Although a working implementation is provided, it "busy waits," that is, it spins in a loop checking the current time and calling thread_yield() until enough time has gone by.
    * Reimplement it to avoid busy waiting.
    * There are TIMER_FREQ timer ticks per second

§2.2.3 Priority Scheduling

1.


For live markdown previews, see
-
* [dillinger]
* [tmpvar]

[dillinger]: http://dillinger.io
[tmpvar]: http://tmpvar.com/markdown.html
