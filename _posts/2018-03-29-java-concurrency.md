---
author: teymur
comments: true
date: 2017-03-29 22:16:08+00:00
layout: post
slug: java-concurrency
title: Java Concurrency
categories: Tutorial
tags:
- java
---

Writing correct programs is hard; writing correct concurrent programs is harder.

## Multitasking

## Process

In computing, a process is an instance of a computer program that is being executed. It contains the program code and its current activity. Depending on the operating system (OS), a process may be made up of multiple threads of execution that execute instructions concurrently.

Process memory is divided into four sections for efficient working :

* The Text section is made up of the compiled program code, read in from non-volatile storage when the program is launched.
* The Stack contains the temporary data such as method/function parameters, return address and local variables.
* The Heap is used for the dynamic memory allocation during its run time.
* The Data section is made up the global and static variables, allocated and initialized prior to executing the main.


### Process States

When a process executes, it passes through different states. 
Processes in the operating system can be in any of the following states:

NEW(Start)- The process is being created.
READY- The process is waiting to be assigned to a processor.
RUNNING- Instructions are being executed.
WAITING- The process is waiting for some event to occur(such as an I/O completion or reception of a signal).
TERMINATED(Exit)- The process has finished execution.

### Process Control Block

A Process Control Block is a data structure maintained by the Operating System for every process. 
The PCB is identified by an integer process ID (PID). 


S.N  | Information | Description
--- | --- | ---
1 	| Process State	| The current state of the process i.e., whether it is ready, running, waiting, or whatever.
2 	| Process privileges | This is required to allow/disallow access to system resources.
3 	| Process ID | Unique identification for each of the process in the operating system.
4 	| Pointer | A pointer to parent process.
5 	| Program Counter | Program Counter is a pointer to the address of the next instruction to be executed for this process.
6 	| CPU registers	| Various CPU registers where process need to be stored for execution for running state.
7 	| CPU Scheduling Information | Process priority and other scheduling information which is required to schedule the process.
8 	| Memory management information	| This includes the information of page table, memory limits, Segment table depending on memory used by the operating system.
9 	| Accounting information | This includes the amount of CPU used for process execution, time limits, execution ID etc.
10 	| IO status information	| This includes a list of I/O devices allocated to the process.


## Process Scheduling

The process scheduling is the activity of the process manager that handles the removal of the running process from the CPU and the selection of another process on the basis of a particular strategy.

Process scheduling is an essential part of a Multiprogramming operating systems.

### Process Scheduling Queues

The OS maintains all PCBs in Process Scheduling Queues. The OS maintains a separate queue for each of the process states and PCBs of all processes in the same execution state are placed in the same queue. When the state of a process is changed, its PCB is unlinked from its current queue and moved to its new state queue.

The Operating System maintains the following important process scheduling queues −

* Job queue − This queue keeps all the processes in the system.
* Ready queue − This queue keeps a set of all processes residing in main memory, ready and waiting to execute. A new process is always put in this queue.
* Device queues − The processes which are blocked due to unavailability of an I/O device constitute this queue.

![Alt text](/techtalks/public/img/java/process_scheduling_queues.jpg?raw=true "Process scheduling Queues")


### Types of Schedulers

* Long Term Scheduler
* Medium Term Scheduler
* Short Term Scheduler

## Context switch

The process of a Context Switch
In computing, a context switch is the process of storing the state of a process or of a thread, so that it can be restored and execution resumed from the same point later. This allows multiple processes to share a single CPU, and is an essential feature of a multitasking operating system


Some operating systems also require a context switch to move between user mode and kernel mode tasks. The process of context switching can have a negative impact on system performance, although the size of this effect depends on the nature of the switch being performed.

When the process is switched, the following information is stored for later use.

* Program Counter
* Scheduling information
* Base and limit register value
* Currently used register
* Changed State
* I/O State information
* Accounting information





## Thread


A thread is a flow of execution through the process code, with its own program counter that keeps track of which instruction to execute next, system registers which hold its current working variables, and a stack which contains the execution history.

Each thread belongs to exactly one process and no thread can exist outside a process. 


![Alt text](/techtalks/public/img/java/thread_processes.jpg?raw=true "Thread Processes")


### Types of Thread

* User Level Threads − User managed threads.
* Kernel Level Threads − Operating System managed threads acting on kernel, an operating system core.



> What is the difference between a process and a thread?


### CPU Scheduling: Dispatcher
Another component involved in the CPU scheduling function is the Dispatcher. The dispatcher is the module that gives control of the CPU to the process selected by the short-term scheduler. This function involves:

* Switching context
* Switching to user mode
* Jumping to the proper location in the user program to restart that program from where it left last time.

The dispatcher should be as fast as possible, given that it is invoked during every process switch. The time taken by the dispatcher to stop one process and start another process is known as the Dispatch Latency

### Thread Libraries
Thread libraries provide programmers with API for creation and management of threads.

Thread libraries may be implemented either in user space or in kernel space. The user space involves API functions implemented solely within the user space, with no kernel support. The kernel space involves system calls, and requires a kernel with thread library support.

## Concurrency


## Parallelism



-----------------------------
In early timesharing systems, each process was a virtual von Neumann com-
puter; it had a memory space storing both instructions and data, executing in-
structions sequentially according to the semantics of the machine language, and
interacting with the outside world via the operating system through a set of I/O
primitives

They share process-wide resources such as memory and file handles, but
each thread has its own program counter, stack, and local variables.

Threads are sometimes called lightweight processes, and most modern oper-
ating systems treat threads, not processes, as the basic units of scheduling. In
the absence of explicit coordination, threads execute simultaneously and asyn-
chronously with respect to one another.


Since threads share the memory address
space of their owning process, all threads within a process have access to the same
variables and allocate objects from the same heap, which allows finer-grained data
sharing than inter-process mechanisms.




Since the basic unit of scheduling is the thread, a program with only one
thread can run on at most one processor at a time.

Using multiple threads can also help achieve better throughput on single-
processor systems. If a program is single-threaded, the processor remains idle
while it waits for a synchronous I/O operation to complete. In a multithreaded
program, another thread can still run while the first thread is waiting for the I/O
to complete, allowing the application to still make progress during the blocking
I/O.



synchronous I/O
nonblocking I/O


Modern GUI frameworks, such as the AWT and Swing toolkits, replace the
main event loop with an event dispatch thread (EDT).


Annotations documenting thread safety are useful to multiple audiences. If a class is
annotated with @ThreadSafe , users can use it with confidence in a multithreaded
environment, maintainers are put on notice that it makes thread safety guarantees
that must be preserved, and software analysis tools can identify possible coding
errors.

```
public class UnsafeSequence {
	private int value;
	/** Returns a unique value. */
	public int getNext() {
		return value++;
	}
}
```

```
@ThreadSafe
public class Sequence {
	@GuardedBy("this") private int value;

	public synchronized int getNext() {
		return value++;
	}
}
```


## Thread Safety


Informally, an object’s state is its data, stored in state variables such as instance
or static fields.



By shared, we mean that a variable could be accessed by multiple threads;
by mutable, we mean that its value could change during its lifetime.



The primary
mechanism for synchronization in Java is the synchronized keyword, which pro-
vides exclusive locking, but the term “synchronization” also includes the use of
volatile variables, explicit locks, and atomic variables.


A class is thread-safe if it behaves correctly when accessed from multiple
threads, regardless of the scheduling or interleaving of the execution of
those threads by the runtime environment, and with no additional syn-
chronization or other coordination on the part of the calling code.

> Stateless objects are always thread-safe.

The possibility of incorrect results in the presence of unlucky timing is so important
in concurrent programming that it has a name: a race condition.

```
@NotThreadSafe
public class LazyInitRace {
	private ExpensiveObject instance = null;
	
	public ExpensiveObject getInstance() {
		if (instance == null)
			instance = new ExpensiveObject();

		return instance;
	}
}
```

LazyInitRace has race conditions that can undermine its correctness. Say that
threads A and B execute getInstance at the same time. A sees that instance
is null , and instantiates a new ExpensiveObject . B also checks if instance is
null . Whether instance is null at this point depends unpredictably on timing,
including the vagaries of scheduling and how long A takes to instantiate the Ex-
pensiveObject and set the instance field. If instance is null when B examines
it, the two callers to getInstance may receive two different results, even though
getInstance is always supposed to return the same instance.


## Parallel Workers

In the parallel worker concurrency model a delegator distributes the incoming jobs to different workers. Each worker completes the full job. The workers work in parallel, running in different threads, and possibly on different CPUs.


### Critical Section Problem

A Critical Section is a code segment that accesses shared variables and has to be executed as an atomic action. It means that in a group of cooperating processes, at a given point of time, only one process must be executing its critical section

### Semaphore

Semaphore is use to manage multiple resources shared between threads and holds a count equivalent to available shared resources.

Binary semaphore is not same as mutex, any thread can release a semaphore, which is not the case in mutex. Semaphore works like signals, and can be used to indicate some event or to maintain the order in which a resource is used or activity is performed.

### Mutex

Mutex is the locking mechanism to protect the critical section. It allows multiple threads to access the same shared resource exclusively. Ownership – Thread locking the critical section can only unlock it. Mutex is used when thread does not want any other thread to execute critical section or access critical resource.

### Synchronization

### Problems of Synchronization

* Bounded Buffer (Producer-Consumer) Problem
* The Readers Writers Problem
* Dining Philosophers Problem

### Race Conditions 

Race conditions can be avoided by proper thread synchronization in critical sections. Thread synchronization can be achieved using a synchronized block of Java code. Thread synchronization can also be achieved using other synchronization constructs like locks or atomic variables like java.util.concurrent.atomic.AtomicInteger.



### Deadlock

### Livelock

The nondeterministic nature of the parallel worker model makes it hard to reason about the state of the system at any given point in time. It also makes it harder (if not impossible) to guarantee that one jobs happens before another.


## Assembly Line


The workers are organized like workers at an assembly line in a factory. Each worker only performs a part of the full job. When that part is finished the worker forwards the job to the next worker.

> What is the difference between concurrency and parallelism?




https://www.quora.com/What-is-the-difference-between-a-process-and-a-thread
https://www.tutorialspoint.com/operating_system/os_processes.html
https://www.studytonight.com/operating-system/operating-system-processes
https://www.studytonight.com/operating-system/
https://en.wikipedia.org/wiki/Context_switch
http://tutorials.jenkov.com/java-concurrency/concurrency-models.html