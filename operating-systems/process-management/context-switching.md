# 🔀 Context Switching

## What is context switching?&#x20;

Context switching is the task of performing a state save of the current running process and and a state restore of the process that is being switched to. This "save & restore" is required for the CPU to switch between process.&#x20;

### When does a context switch occur?&#x20;

Occurs when the CPU switches from one process to another

### How long does a context switch take?&#x20;

* The time spent during a context switch is considered overhead, as the system is unable to do useful work during this time.
* How long a context switch takes is **hardware dependent.**

## What is "context"?&#x20;

* The context of a process can be thought of as metadata related to the process.&#x20;
* Found in the process control block (PCB) of a process
  * Value of CPU registers&#x20;
  * State of the process&#x20;
  * Memory management information&#x20;
