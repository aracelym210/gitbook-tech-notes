---
description: Interprocess Communication (IPC)
---

# Interprocess Communication

## IPC Background&#x20;

Processes running at the same time may be either independent or cooperating.

|                Independent               |             Cooperating            |
| :--------------------------------------: | :--------------------------------: |
| Does not share data with other processes |  Shares data with other processes  |
|                                          | Can be affected by other processes |

## IPC Purpose

Cooperating processes require a mechanism to allow for exchange of data. Two fundamental models of interprocess commnication enable this exchange of data:&#x20;

* Shared memory&#x20;
* Message Passing
