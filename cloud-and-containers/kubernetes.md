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

## K8s Architecture

### Cluster

Kubernetes cluster is made up of multiple computers -- mostly VMs

* Control plane: computer that runs several of Kubernetes critical components&#x20;
  * kube-APIserver: accept commands to view/ change the state of the cluster&#x20;
    * `kubectl` command communicates with the kube-APIserver, but in fact any command that changes the cluster goes through the kube-APIserver
  * etcd: cluster DB that stores the state of the cluster, configuration data, and other dynamic metadata.&#x20;
  * kube-scheduler: scheduling pods onto nodes by evaluating requirements of each indv. pod, and then selects which node is most suitable. **it does not assign, but simply writes information on the pod object which will later get referenced and assigned by another component**&#x20;
  * kube-controller-manager: continuously monitors the state of the cluster through kube-APIserver. when there is a deviation between desired state and current state, this component attempts to make changes to achieve the desired state&#x20;
    * a _controller_ is a code loop that handles the process of remediation on individual kubernetes objects. the kube-controller-manager manages these code loops.&#x20;
  * kube-cloud-mananger: manages controllers that interact with the underlying cloud service providers (CSP)

![Diagram of how the components described above interconnect ](<../.gitbook/assets/image (9).png>)

#### Namespaces&#x20;

* A single cluster can be abstracted into multiple clusters called namespaces&#x20;
* Provide scope for naming resources such as pod deployments and controllers
* For example -- test, stage, and prod
* not required&#x20;
* 3 initial namespaces in a cluster
  * Default
  * Kube-System: namespace for objects created by kubernetes system itself
  * Kube-public: essentially this is a broadcast namespace&#x20;
* Object names need only be unique across a namespace, not across all namespaces&#x20;
* ![](<../.gitbook/assets/image (2).png>)

### Node(s)

* Usually a virtual machine (can be physical)
* Pods live on nodes&#x20;
* Each node managed by the control plane&#x20;

#### Node controllers

* kubelet: kubernetes agent on each node that communicates with kube-APIserver
* kube-proxy: maintains the network connectivity among the pods in a cluster by leveraging firewall capabilities of iptables

### [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)

* ephemeral and disposable objects, w/ lifecycle -- born, running, broken, dead&#x20;
* A set of running containers in your cluster&#x20;
* Placing containers on the same pod will ensure they run on the same node, thus reducing network latency

#### Controller Objects and Pods

* Instead of defining separate individual pods, we can use a controller object whose job is to manage the state of the pods
  * Remember that pods are not self-healing&#x20;

_**Other controller objects**_ :arrow\_down:_****_

{% tabs %}
{% tab title="Deployments" %}
* Create, update, roll back and scale Pods, using ReplicaSets as needed
* For example, when you perform a rolling upgrade of a Deployment, the Deployment object creates a second ReplicaSet, and then increases the number of Pods in the new ReplicaSet as it decreases the number of Pods in its original ReplicaSet.
{% endtab %}

{% tab title="Replication Controllers" %}
{% hint style="danger" %}
No longer recommended, although can perform similar role of ReplicaSets and Deployments combination
{% endhint %}
{% endtab %}

{% tab title="StatefulSet" %}
* Useful for applications that need to maintain a local state
* Pods created through Deployment have unique identities with stable network identity and persistent disk storage&#x20;
{% endtab %}

{% tab title="DaemonSets" %}
* Ensures that a specific Pod is always running on all or some subnet of the nodes&#x20;
* If new nodes are added, DaemonSet will automatically set up Pods in those nodes with the required specification

{% hint style="info" %}
_****_[_**Daemon**_](https://en.wikipedia.org/wiki/Daemon\_\(computing\)) **** is a computer science term which is a non-interactive process that provides useful services to other processes
{% endhint %}
{% endtab %}

{% tab title="Job" %}
* Creates one or more Pods required to run a task
* Once the task completes, the Job controller will terminate the pods&#x20;

{% hint style="warning" %}
<mark style="color:orange;">**Related:**</mark> CronJob controller
{% endhint %}
{% endtab %}
{% endtabs %}

#### Deployment&#x20;

* Declares the state of Pods&#x20;
* Ensures that a defined set of pods is running at any given time
* ![](<../.gitbook/assets/image (8).png>)
* Well-suited for [stateless applications ](kubernetes.md#stateful-and-stateless-applications)
  * i.e. a web frontend&#x20;

{% hint style="info" %}
_**Deployment YAML files**_

* Declares the characteristics of the pods
* Declares how to operationally run these pods and their life cycle events&#x20;
* After the YAML file is submitted to the control plane, a deployment controller is created. See other [controller objects](kubernetes.md#controller-objects-and-pods) :arrow\_up:
{% endhint %}

_**Deployment lifecycle states**_

{% tabs %}
{% tab title="Progressing state" %}
* Indicates that a task has been performed (i.e. creating new replicaSets, scaling up or down replicaSets
{% endtab %}

{% tab title="Complete state" %}
* Indicates that all new replicaSets have been updated to the latest version and are available
{% endtab %}

{% tab title="Failed state" %}
* Creation of a new replicaSet could not be completed&#x20;
  * Could happen because not enough of a resource quota, or lacking permissions, or unable to pull new pods&#x20;
{% endtab %}
{% endtabs %}

{% hint style="success" %}
**Best Practice Reminder**

Keep your deployment YAML files in a source code repository of some sort!
{% endhint %}

### [Workload](https://kubernetes.io/docs/concepts/workloads/)

* An application running on K8s that is run inside a set of pods

### Load-balanced Services&#x20;

* ClusterIP: Exposes the service on an IP address that is only accessible from within this cluster. This is the default type.&#x20;
* NodePort: Exposes the service on the IP address of each node in the cluster, at a specific port number.&#x20;
* LoadBalancer: Exposes the service externally, using a load balancing service provided by a cloud provider.

## [Kubectl command](https://kubernetes.io/docs/reference/kubectl/)

{% hint style="info" %}
`kubectl` is a command line utility to control Kubernetes clusters \
\
[Syntax:](https://kubernetes.io/docs/reference/kubectl/#syntax)**`kubectl [command] [TYPE] [NAME] [flags]`**&#x20;
{% endhint %}

* Communicates w/ kube-APIserver&#x20;
* Must be configured with a location and valid credentials&#x20;

### Configuring kubectl

* Config file lives at `$HOME/.kube/config`
* To view current config: `kubectl config view`

### kubectl syntax&#x20;

![](<../.gitbook/assets/image (10).png>)

#### `kubectl [command] [TYPE] [NAME] [flags]`&#x20;

* the `[NAME]` field is optional, and can be used to specify the object you wish to act upon.&#x20;
  * For example, `kubectl get pod my-test-app` will return the state of the pod _named_ "my-test-app"
* like many CLI tools, `[flags]` can be used to display more or specific information or to specify an output format&#x20;
*

##

## References

* Google Cloud Training - Getting Started with Google Kubernetes Engine
* [Kubernetes Docs](https://kubernetes.io/docs/concepts/)
