# Shared Memory IPC

## What is the shared memory IPC model?

* Communicating processes establish a region of shared memory
* This shared memory segment is an address space of the _creating,_ or _producing_, process. Other processes that wish to communicate using this same memory segment, or _consumer processes_, must attach it their address space.
* The shared memory model requires that two or more processes agree to remove the typical restriction of not being able to access another process's memory.
* The processes are responsible for avoiding a <mark style="color:purple;">race condition</mark> (i.e. ensuring they do not write to the same memory location).

## Producer-Consumer Problem

The [producer-consumer problem](https://www.youtube.com/watch?v=l6zkaJFjUbM) is a helpful paradigm to consider when thinking of how shared memory works between processes.

A <mark style="color:purple;">buffer</mark> will reside in a shared memory space that is accessible by both producer and consumer processes.

## Unbounded vs. Bounded Buffers

|               Unbounded Buffer               |                     Bounded Buffer                     |
| :------------------------------------------: | :----------------------------------------------------: |
| No practical limit on the size of the buffer |              Assumes a _fixed_ buffer size             |
|   No limit to the amount of items produced   | The consuming process must wait if the buffer is empty |
|                                              |  The producing process must wait if the buffer is full |
