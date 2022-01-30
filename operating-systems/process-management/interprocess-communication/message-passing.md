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

* Two different address schemes for implementation.
* Both symmetrical and asymmetrical schemes have the disadvantage of <mark style="color:purple;">limited modularity</mark>.

#### Symmetrical Address Scheme

* Processes must explicitly name the recipient or sender&#x20;
* `send(P, message)`  -- Send message to process _P_
* `receive(Q, message)`  -- Receive message from process _Q_

#### Asymmetrical Address Scheme

* Only the _sender_ names the recipient; the recipient need not name the sender&#x20;
* `send(P, message)`  -- Send message to process _P_
* `receive(id, message)`  -- Receive message from _any process_. `id` is a variable and set to the name of the process.

### Indirect Communication

* Messages are sent and received from <mark style="color:purple;">mailboxes</mark>, also known as <mark style="color:purple;">ports</mark>.

> A <mark style="color:purple;">mailbox</mark> can be viewed as an abstract object into which a process can place or remove messages. A mailbox can be owned by a process or the operating system.

* Processes can only communicate if they have a shared mailbox
  * `send(A, message)`  -- Send message to _mailbox A_
  * `receive(A, message)`  -- Receive message from _mailbox A_

## Synchronous vs. Asynchronous Message Passing

There are different design options for implementing the `send()` and `receive()` primitives.

{% tabs %}
{% tab title="Send()" %}
| Blocking (synchronous)                                            | Non-blocking (asynchronous)                                             |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Sending process is blocked until message reaches it's destination | Sending process sends a message and resumes operation (fire and forget) |
{% endtab %}

{% tab title="Receive()" %}
| Blocking (synchronous)                           | Non-blocking (asynchronous)                                  |
| ------------------------------------------------ | ------------------------------------------------------------ |
| The receiver blocks until a message is available | The receiver will retrieve a valid message or a null message |
{% endtab %}
{% endtabs %}
