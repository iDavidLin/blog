---
layout: post
title: "Concurrency Programming -- Basic Concepts"
date: 2018-01-28
categories: "Computer science"
description: concurrency 101
tags: [concurrency]
---

Some concepts about concurrency programming.

### 一、同步(synchronous) VS 异步(asynchronous)
What’s synchronous and asynchronous?

If you went to the Bank and you want to open a now a account.
You line up a line and have to wait there till the one in front had finish his service.
That’s synchronous.

If you ever went to startbucks, you will know that when you order coffee there, they will give you a number (or a token) and talk to wait somewhere off line. So they can continue service others who’s behind. You wouldn’t block other people. And when your coffee is made, they will call you.
That’s asynchronous.

Synchronous (one thread):  

    1 thread ->   |<---A---->||<----B---------->||<------C----->|

Synchronous (multi-threaded):

    thread A -> |<---A---->|   
                        \  
    thread B ------------>   ->|<----B---------->|   
                                              \   
    thread C ---------------------------------->   ->|<------C----->| 

Asynchronous (one thread):

                  A-Start ------------------------------------------ A-End   
                    | B-Start -----------------------------------------|--- B-End   
                    |    |      C-Start ------------------- C-End      |      |   
                    |    |       |                           |         |      |
                    V    V       V                           V         V      V  
          1 thread->|<-A-|<--B---|<-C-|-A-|-C-|--A--|-B-|--C-->|---A---->|--B-->| 

Asynchronous (multi-Threaded):
    
     thread A ->     |<---A---->|
     thread B ----->     |<----B---------->| 
     thread C --------->     |<------C--------->|
 
 * Start and end points of tasks A, B, C represented by <, > characters.
 * CPU time slices represented by vertical bars

<br>
### 二、并发(Concurrency)和并行(Parallelism)

![concurrency vs Parallelism](/image/Concurrency-vs-Parallelism.png)

Concurrent  

    Two queues and one coffee machine.

Parallel

    Two queues and two coffee machines.

   
<br>

### 三、临界区(Critical Section)

In concurrent programming, concurrent accesses to shared resources can lead to unexpected or erroneous behavior, so parts of the program where the shared resource is accessed are protected. This protected section is the **critical section** or **critical region**. It cannot be executed by more than one process. Typically, the critical section accesses a shared resource, such as a data structure, a peripheral device, or a network connection, that would not operate correctly in the context of multiple concurrent accesses.


![Critical-Section](/image/Critical-Section.jpg)

### 四、阻塞(Blocking)和非阻塞(Non-Blocking)

**Blocking** assignment executes "in series** because a blocking assignment blocks execution of the next statement until it completes. Therefore the results of the next statement may depend on the first one being completed.

**Non-blocking** assignment executes in parallel because it describes assignments that all occur at the same time. The result of a statement on the 2nd line will not depend on the results of the statement on the 1st line. Instead, the 2nd line will execute as if the 1st line had not happened yet.

    Let's say you go to startbucks and order a coffee. And you are waitting and can
    not do anything. That's Blocking. You are blocked there. But if you just pull 
    out you phone and just open you twitter or whatever, then you are Non-blocking.

![Blocking-VS-Non-Blocking](/image/Blocking-VS-Non-Blocking.png)

### 五、锁(Deadlock)、饥饿(Starvation)和活锁(Livelock**

#### **Deadlock**  
`Deadlock describes a situation where two more threads are blocked because of waiting for each other forever.` When deadlock occurs, the program hangs forever and the only thing you can do is to kill the program.  
Like the picture below, cars are waiting other cars.
![Deadlock](/image/deadlock.jpg)

<br>
#### **Starvation**
`Starvation describes a situation where a greedy thread holds a resource for a long time so other threads are blocked forever.` The blocked threads are waiting to acquire the resource but they never get a chance. Thus they starve to death.
Starvation can occur due to the following reasons:
- Threads are blocked infinitely because a thread takes long time to execute some synchronized code (e.g. heavy I/O operations or infinite loop).

- A thread doesn’t get CPU’s time for execution because it has low priority as compared to other threads which have higher priority.

- Threads are waiting on a resource forever but they remain waiting forever because other threads are constantly notified instead of the hungry ones.

When a starvation situation occurs, the program is still running but doesn’t run to completion because some threads are not executed.

<br>
#### **Livelock**
`Livelock describes situation where two threads are busy responding to actions of each other.` They keep repeating a particular code so the program is unable to make further progress:
Thread 1 acts as a response to action of thread 2

Thread 2 acts as a response to action of thread 1

Unlike deadlock, threads are not blocked when livelock occurs. They are simply too busy responding to each other to resume work. In other words, the program runs into an infinite loop and cannot proceed further.
 
A Livelock Example:
Let’s see an example: a criminal kidnaps a hostage and he asks for ransom in order to release the hostage. A police agrees to give the criminal the money he wants once the hostage is released. The criminal releases the hostage only when he gets the money. Both are waiting for each other to act first, hence livelock.

#### **Reference Links**  
[Critical Section](https://en.wikipedia.org/wiki/Critical_section)  
[临界区，互斥量，信号量，事件的区别](http://blog.csdn.net/bao_qibiao/article/details/4516196)  
[concurrent and parallel programming](https://joearms.github.io/published/2013-04-05-concurrent-and-parallel-programming.html)  
[Asynchronous vs synchronous execution, what does it really mean?](https://stackoverflow.com/questions/748175/asynchronous-vs-synchronous-execution-what-does-it-really-mean)  
[Understanding Deadlock, Livelock and Starvation with Code Examples in Java](http://www.codejava.net/java-core/concurrency/understanding-deadlock-livelock-and-starvation-with-code-examples-in-java)

#### **Extended reading**  
[The Java Memory Model](http://www.cs.umd.edu/~pugh/java/memoryModel/)
