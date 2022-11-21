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