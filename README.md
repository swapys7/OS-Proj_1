OS-Proj_1
=========

Currently Working On:
==


§2.2.2 Alarm Clock Description
--

The current version "_busy waits_", spinning in a loop, checking the current time, and calling thread_yield(); until time is up. *Reimplement it to avoid busy waiting*.

Things for Knowing of:
--

1. Unless the system is otherwise idle, the thread need not wake up after _exactly_ x ticks. It just needs to be put on the `ready queue` after the correct amount of time.


Current Ideas:
--

1. We need to implement a wait-queue list or some other kind of list

1. I think the idea is to use a sema_down(); to take the thread off the READY_LIST and put it on a list of threads waiting on a Semaphore by using the elem member of the struct thread.

1. Check out the /* Statistics. */ section of `thread.c`, it keeps track of `timer_ticks` and `thread_ticks`. I think that is important.

1. Do we use `wait() & signal();` in `devices/intq.c` "whose callers are responsible for reenabling interrupts" (§2.3.0 FAQ)?

1. Judging by the added lines to thread.h,  maybe that is where one adds the new WAITING_LIST.

1. Maybe the number of ticks is a condition_variable, as described in `synch.c`
    * but with that method, it seems like we would need a seperate lock/condition for each thread, which may be avoidable with semaphores, though maybe not

The Other Assignment in this Assignment:
==

§2.2.3 Priority Scheduling
--

1. Implement priority scheduling in Pintos.
    * Priorities range from 0 to 63, where higher is higher

1. Implement priority donation to deal with the issue of "priority inversion". Only for the locks, not the other constructs.

    * This is for the situation where H is waiting for a lock held by L, but L never gets to run

    * This must still work in cases of nested donation, up to 8 levels!:
        * H is waiting for M which is waiting for L, so H must levitate L to H, then M to H, then run.
    * H will donate to L with its lock, even if L is READY but not RUNNING

1. Implement the following two functions, for which only the skeletons have been provided in `threads/thread.c`.

    * Function: void thread_set_priority (int new_priority);
        1. Sets the current thread''s priority to new_priority.
        1. If the current thread no longer has the highest priority, yields.

    * Function: int thread_get_priority (void);
        1. Returns the current thread''s priority.
        1. In the presence of priority donation, returns the higher (donated); priority.

    * You need not provide any interface to allow a thread to directly modify other threads'' priorities.

Ideas:
--

The True-Priority should be one thing, and the Highest-Donated-Priority should be a completely different field.

Files/Lines they Modified to Make Reference solution:
==
 1. `devices/timer.c`       |   42 +++++-
    * Contains timer_sleep(); itself
    * Probably won''t need to modify anything else in it

 1. `threads/fixed-point.h` |  120 ++++++++++++++++++
    * I don''t see this file anywhere, maybe they made it !

 1. `threads/synch.c`       |   88 ++++++++++++-
    * semaphores, locks, condition variables

 1. `threads/thread.c`      |  196 ++++++++++++++++++++++++++----
    * Initializes lists, manipulates threads, calls main to start things out, does the scheduling

 1. `threads/thread.h`      |   23 +++
    * I think adding 23 lines to this means they added a couple methods to `thread.c` and had to declare them?

 * 5 files changed, 440 insertions(+); 29 deletions(-);


In General, What else Needs to Be Done:
==

The Design Doc
--

It is saved in the base directory, just like this file, it is called threads_design.txt

Follow the C Style Guide
--

1. Summarize major sections of code
1. Use meaningful variable names
1. Describe what function does, parameters, and return values
1. Don''t use extra whitespace inside brackets and braces



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

