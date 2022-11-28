# Chapter 27


## Question 1
It prints out threads and data race informations such as variable name, addresss size etc.

## Question 2
Removing one of the offending lines prints nothing in the helgrind output.
Adding a lock around one of the updates shows possible data race.
Adding lock around both the updates shows no errors.

## Question 3

Two threads waiting for a lock that is locked by another thread.

## Question 4
Thread #3: lock order "0x420050 before 0x420080" violated

==1240110== Helgrind, a thread error detector
==1240110== Copyright (C) 2007-2017, and GNU GPL'd, by OpenWorks LLP et al.
==1240110== Using Valgrind-3.19.0 and LibVEX; rerun with -h for copyright info
==1240110== Command: ./main-deadlock
==1240110== 
==1240110== ---Thread-Announcement------------------------------------------
==1240110== 
==1240110== Thread #3 was created
==1240110==    at 0x4BD5C77: clone (clone.S:62)
==1240110==    by 0x4C2E603: create_thread (pthread_create.c:296)
==1240110==    by 0x4C2EFCB: pthread_create@@GLIBC_2.34 (pthread_create.c:829)
==1240110==    by 0x48731F3: pthread_create_WRK (hg_intercepts.c:445)
==1240110==    by 0x487452F: pthread_create@* (hg_intercepts.c:478)
==1240110==    by 0x400997: main (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110== 
==1240110== ----------------------------------------------------------------
==1240110== 
==1240110== Thread #3: lock order "0x420050 before 0x420080" violated
==1240110== 
==1240110== Observed (incorrect) order is: acquisition of lock at 0x420080
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x400857: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110== 
==1240110==  followed by a later acquisition of lock at 0x420050
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x40088B: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110== 
==1240110== Required order was established by acquisition of lock at 0x420050
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x4007EF: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110== 
==1240110==  followed by a later acquisition of lock at 0x420080
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x400823: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110== 
==1240110==  Lock at 0x420050 was first observed
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x4007EF: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110==  Address 0x420050 is 0 bytes inside data symbol "m1"
==1240110== 
==1240110==  Lock at 0x420080 was first observed
==1240110==    at 0x4870638: mutex_lock_WRK (hg_intercepts.c:942)
==1240110==    by 0x4874967: pthread_mutex_lock (hg_intercepts.c:958)
==1240110==    by 0x400823: worker(void*) (in /home/ec2-user/thread-hw/threads-api/main-deadlock)
==1240110==    by 0x48733D3: mythread_wrapper (hg_intercepts.c:406)
==1240110==    by 0x4C2E9CB: start_thread (pthread_create.c:443)
==1240110==    by 0x4BD5C9B: thread_start (clone.S:79)
==1240110==  Address 0x420080 is 0 bytes inside data symbol "m2"
==1240110== 
==1240110== 
==1240110== 
==1240110== Use --history-level=approx or =none to gain increased speed, at
==1240110== the cost of reduced accuracy of conflicting-access information
==1240110== For lists of detected and suppressed errors, rerun with: -s
==1240110== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 7 from 6)


## Question 5

It doesnt have the same problem. helgrind reports about incorrect lock order problem.


## Question 6

The parent falls in the loop and use up cpu cycles doing nothing.

## Question 7
Possible data race of write/read done and printf(). And the code is not correct.

## Question 8

Both.
## Question 9
No error.


# Chapter 28

Examine flag.s. This code “implements” locking with a single memory flag. Can you understand the assembly?

When you run with the defaults, does flag.s work? Use the -M and -R flags to trace variables and registers (and turn on -c to see their values). Can you predict what value will end up in flag?

$ ./x86.py -p flag.s -M flag,count -R ax,bx -c
0

Change the value of the register %bx with the -a flag(e.g., -a bx=2,bx=2 if you are running just two threads). What does the code do? How does it change your answer for the question above?

$ ./x86.py -p flag.s -M flag,count -R ax,bx -c -a bx=2,bx=2
Each thread runs two loops. flag is still 0.

Set bx to a high value for each thread, and then use the -i flag to generate different interrupt frequencies; what values lead to a bad outcomes? Which lead to good outcomes?

// bad outcomes
$ ./x86.py -p flag.s -M flag,count -R ax,bx -c -a bx=10,bx=10 -i 1-10,12,13,14,17

// god outcomes
$ ./x86.py -p flag.s -M flag,count -R ax,bx -c -a bx=10,bx=10 -i 11,15,16
Now let’s look at the program test-and-set.s. First, try to understand the code, which uses the xchg instruction to build a simple locking primitive. How is the lock acquire written? How about lock release?

Test and acquire in one command.

Now run the code, changing the value of the interrupt interval (-i) again, and making sure to loop for a number of times. Does the code always work as expected? Does it sometimes lead to an inefficient use of the CPU? How could you quantify that?

It works. Mutex is 0.

Use the -P flag to generate specific tests of the locking code. For example, run a schedule that grabs the lock in the first thread, but then tries to acquire it in the second. Does the right thing happen? What else should you test?

$ ./x86.py -p test-and-set.s -M mutex,count -R ax,bx -c -a bx=10,bx=10 -P 0011
Yes. Fairness and performance.

Now let’s look at the code in peterson.s, which implements Peterson’s algorithm (mentioned in a sidebar in the text). Study the code and see if you can make sense of it.

Now run the code with different values of -i. What kinds of different behavior do you see? Make sure to set the thread IDs appropriately (using -a bx=0,bx=1 for example) as the code assumes it.

$ ./x86.py -p peterson.s -M count,flag,turn -R ax,cx -a bx=0,bx=1 -c -i 2
Can you control the scheduling (with the -P flag) to “prove” that the code works? What are the different cases you should show hold? Think about mutual exclusion and deadlock avoidance.

$ ./x86.py -p peterson.s -M count,flag,turn -R ax,cx -a bx=0,bx=1 -c -P 0000011111
Now study the code for the ticket lock in ticket.s. Does it match the code in the chapter? Then run with the following flags: -a bx=1000,bx=1000 (causing each thread to loop through the critical section 1000 times). Watch what happens; do the threads spend much time spin-waiting for the lock?

Yes.

$ ./x86.py -p ticket.s -M count,ticket,turn -R ax,bx,cx -a bx=1000,bx=1000 -c
Count is correct. Yes.

How does the code behave as you add more threads?

$ ./x86.py -p ticket.s -M count -t 10 -c -i 5
spin in tryagain loop

Now examine yield.s, in which a yield instruction enables one thread to yield control of the CPU (realistically, this would be an OS primitive, but for the simplicity, we assume an instruction does the task). Find a scenario where test-and-set.s wastes cycles spinning, but yield.s does not. How many instructions are saved? In what scenarios do these savings arise?

$ ./x86.py -p test-and-set.s -M count,mutex -R ax,bx -a bx=5,bx=5 -c -i 7
$ ./x86.py -p yield.s -M count,mutex -R ax,bx -a bx=5,bx=5 -c -i 7
Saved one instruction each cycle. When the thread doesn't have the mutex.

Finally, examine test-and-test-and-set.s. What does this lock do? What kind of savings does it introduce as compared to test-and-set.s?

Change mutex to 1 only if lock is free. That will avoid unnecessary writing.