---
description: Notes on the message-passing IPC model
---

# 📬 Message Passing

* Operating system provides the means for cooperating processes to communicate via a message-passing facility
* Message-passing IPC model is useful in a distributed environment where communicating processes may be on different computers, thus communicating over a network
* Messages can be fixed or variable sized&#x20;
* Processes that wish to communicate require a communication link
*   Logical implementation methods

    * Direct or indirect &#x20;
    * Synchronous or asynchronous
    * Automatic or explicit buffering&#x20;



## Direct vs. Indirect Communication

* Also referred to as symmetrical vs. asymmetrical communication scheme

### Direct Communication&#x20;

#### Symmetrical Address Scheme

* Processes must explicitly name the recipient or sender&#x20;
* `send(P, message)`  -- Send message to process _P_
* `receive(Q, message)`  -- Receive message from process _Q_

#### Asymmetrical Address Scheme

