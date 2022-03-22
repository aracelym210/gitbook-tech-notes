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

_Everything that is managed by Kubernetes is an object, which is similar to the computer science concept of object-oriented programming_

* Attributes of objects can be viewed and changed&#x20;
* A Kubernetes object is a persistent entity that represents the state of something running in a cluster. More specifically, the _desired state_ and the _current state_ are part of the object definition.&#x20;

### Principle of declarative management&#x20;

* Kubernetes expects to be told what the desired state of the objects under it's management is
* Given a defined state, Kubernetes will work to bring that state to fruition, and will keep it there&#x20;
  * This is achieved by the Kubernetes "watchloop"

### Architecture

#### **Basic components**

* Cluster
* Node(s)
* [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
  * ephemeral and disposable objects, w/ lifecycle -- born, running, broken, dead&#x20;
  * A set of running containers in your cluster&#x20;
* Container
* [Workload](https://kubernetes.io/docs/concepts/workloads/)
  * An application running on K8s that is run inside a set of pods

Kubernetes cluster is made up of multiple computers -- mostly VMs

* Control plane: computer that runs several of Kubernetes critical components&#x20;
  * kube-APIserver: accept commands to view/ change the state of the cluster&#x20;
    * `kubectl` command communicates with the kube-APIserver, but in fact any command that changes the cluster goes through the kube-APIserver
  * etcd: cluster DB that stores the state of the cluster, configuration data, and other dynamic metadata.&#x20;
  * kube-scheduler: scheduling pods onto nodes by evaluating requirements of each indv. pod, and then selects which node is most suitable. **it does not assign, but simply writes information on the pod object which will later get referenced and assigned by another component**&#x20;
  * kube-controller-manager: continuously monitors the state of the cluster through kube-APIserver. when there is a deviation between desired state and current state, this component attempts to make changes to achieve the desired state&#x20;
    * a _controller_ is a code loop that handles the process of remediation on individual kubernetes objects. the kube-controller-manager manages these code loops.&#x20;
  * kube-cloud-mananger: manages controllers that interact with the underlying cloud service providers (CSP)
*   Node

    * kubelet: kubernetes agent on each node that communicates with kube-APIserver
    * kube-proxy: maintains the network connectivity among the pods in a cluster by leveraging firewall capabilities of iptables



![Diagram of how the components described above interconnect ](<../.gitbook/assets/image (9).png>)

####

## References

* Google Cloud Training - Getting Started with Google Kubernetes Engine
* [Kubernetes Docs](https://kubernetes.io/docs/concepts/)
