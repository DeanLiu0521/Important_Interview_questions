# Operating System Concepts

## Threads and Processes

###Process
A process is the execution of a program that allows you to perform the appropriate actions specified in a program. It is an execution unit where a program runs. Is controlled by CPU.

### Threads
Thread is an execution unit that is part of a process. A process can have multiple threads all executing at the same time. Thread is light weight and can be managed independently by a scheduler. Key concept in parallelism.

Types:
1. Kernel-level threads
2. User-level threads
3. Hybrid threads

### Differences

|Parameter	|Process|	Thread|
|:----------------|:---------------------------------:|--------------------------------------:|
|Definition	|Process means a program is in execution.	|Thread means a segment of a process.|
|Lightweight	|The process is not Lightweight.	|Threads are Lightweight.|
|Termination time	|The process takes more time to terminate	|The thread takes less time to terminate.|
|Creation time	|It takes more time for creation.	|It takes less time for creation.|
|Communication	|Communication between processes needs more time compared to thread.|	between threads requires less time compared to processes.|
|Context switching time	|It takes more time for context switching.	|It takes less time for context switching.|
|Resource	|Process consume more resources.	|Thread consume fewer resources.|
|Treatment |by OS	Different process are tread separately by OS.	|All the level peer threads are treated as a single task by OS.|
|Memory	|The process is mostly isolated.	|Threads share memory.|
|Sharing	|It does not share data	|Threads share data with each other.|

## Operating System scheduling algorithms
1. First Come First Serve (FCFS): Simplest scheduling algorithm that schedules according to arrival times of processes. First come first serve scheduling algorithm states that the process that requests the CPU first is allocated the CPU first. It is implemented by using the FIFO queue. When a process enters the ready queue, its PCB is linked onto the tail of the queue. When the CPU is free, it is allocated to the process at the head of the queue. The running process is then removed from the queue. FCFS is a non-preemptive scheduling algorithm.\

2. Shortest Job First (SJF): Process which have the shortest burst time are scheduled first.If two processes have the same bust time then FCFS is used to break the tie. It is a non-preemptive scheduling algorithm.


3. Shortest Remaining Time First (SRTF): It is preemptive mode of SJF algorithm in which jobs are schedule according to shortest remaining time.

4. Longest Remaining Time First (LRTF): It is preemptive mode of LJF algorithm in which we give priority to the process having largest burst time remaining.

5. Round Robin Scheduling: Each process is assigned a fixed time(Time Quantum/Time Slice) in cyclic way.It is designed especially for the time-sharing system. The ready queue is treated as a circular queue. The CPU scheduler goes around the ready queue, allocating the CPU to each process for a time interval of up to 1-time quantum. To implement Round Robin scheduling, we keep the ready queue as a FIFO queue of processes. New processes are added to the tail of the ready queue. The CPU scheduler picks the first process from the ready queue, sets a timer to interrupt after 1-time quantum, and dispatches the process. One of two things will then happen. The process may have a CPU burst of less than 1-time quantum. In this case, the process itself will release the CPU voluntarily. The scheduler will then proceed to the next process in the ready queue. Otherwise, if the CPU burst of the currently running process is longer than 1-time quantum, the timer will go off and will cause an interrupt to the operating system. A context switch will be executed, and the process will be put at the tail of the ready queue. The CPU scheduler will then select the next process in the ready queue.

6. Priority Based scheduling (Non-Preemptive): In this scheduling, processes are scheduled according to their priorities, i.e., highest priority process is scheduled first. If priorities of two processes match, then schedule according to arrival time. Here starvation of process is possible.

7. Highest Response Ratio Next (HRRN): In this scheduling, processes with highest response ratio is scheduled. This algorithm avoids starvation.

  Response Ratio = (Waiting Time + Burst time) / Burst time
8. Multilevel Queue Scheduling: According to the priority of process, processes are placed in the different queues. Generally high priority process are placed in the top level queue. Only after completion of processes from top level queue, lower level queued processes are scheduled. It can suffer from starvation.

9. Multi level Feedback Queue Scheduling: It allows the process to move in between queues. The idea is to separate processes according to the characteristics of their CPU bursts. If a process uses too much CPU time, it is moved to a lower-priority queue.

## How to communicate between processes
Inter Process Communication(IPC)
Independent process and Co-operating process
shared memory and messaging passing
  shared memory producer and consumer model:
```C
  #define BUFFSIZE 25
  struct item{
    //element of the resource array
  };
  //free_index points to the next free index of
  //the resource array. full_index points to the
  //first index of the used resource in the array.
  int free_index =0;
  int full_index =0;
  Producer(){
    while(1){
      while((free_index+1)%BUFFSIZE==full_index);
      shared_buff[free_index]=produced_item;
      free_index = (free_index+1)%BUFFSIZE;
    }
  }
  Consumer(){
    while(1){
      while(free_index==full_index);
      consumed_item = shared_buff[full_index];
      full_index = (full_index+1)%BUFFSIZE;
    }
  }
```
## Mutex and Semaphore

Mutex: This is a locking mechanism used to synchronize access to a resource. Only one task can acquire the mutes. It means there is ownership associated with mutex, and only the owner can release the lock.

Semaphore: Semaphore is a signaling mechanism.


虚拟内存机制的作用
缓存的作用以及缓存替换算法
线程的实现方式
虚拟文件系统
