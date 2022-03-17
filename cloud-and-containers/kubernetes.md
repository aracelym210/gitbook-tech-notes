---
description: Open source, container orchestration and management software
---

# ☸ Kubernetes

## What is Kubernetes?&#x20;

* Container-centric management environment&#x20;
* Created by Google, then handed over to Open Source community&#x20;
* Automates deployment, scaling, load-balancing, logging and monitoring, and other management features of containerized apps&#x20;
* Declarative configuration&#x20;
  * Describe the desired state you want to achieve instead of issuing the commands to get to the desired state&#x20;
  * Ideal way to run/ manage Kubernetes because once the desired state is achieved, Kubernetes works to maintain that state&#x20;
* Imperative configuration is also allowed
  * Unlike declarative configuration, configuring a system imperatively means you are manually issuing commands to achieve the desired end-state.&#x20;
  * Only use for quick temporary fixes

## Kubernetes features&#x20;

### Stateful and stateless applications&#x20;

#### Stateless

* Examples include: nginx, apache web server

#### Stateful

* User and session data can be stored persistently&#x20;

### Autoscaling&#x20;

* Kubernetes can automatically scale in and out containerized applications based on resource utilization&#x20;

### Resource limits&#x20;

* Resource request levels and resource limits can be defined&#x20;
* Enables improvement of overall workload performance within a cluster&#x20;

### Extensibility&#x20;

* Developers can extend kubernetes through a rich ecosystem of plugins and add-ons&#x20;

### Portability&#x20;

* Workload portability is supported because of Kubernetes open-source nature&#x20;

## Kubernetes Concepts&#x20;

### Kubernetes Object Model

_Everything in Kubernetes is an object, which is similar to the computer science concept of object-oriented programming_

* Attributes of objects can be viewed and changed&#x20;

[#what-is-kubernetes](kubernetes.md#what-is-kubernetes "mention")
