---
description: Notes on Google Kubernetes Engine -- aka GK
---

# Google Kubernetes Engine

## Containers&#x20;

Containerization is the latest virtualization technology which virtualizes the [user space ](https://en.wikipedia.org/wiki/User\_space\_and\_kernel\_space#:\~:text=Kernel%20space%20is%20strictly%20reserved,software%20and%20some%20drivers%20execute.)where applications reside. Compare this to hypervisors like VMWare, Virtual Box or KVM, which virtualize [kernel space](https://en.wikipedia.org/wiki/User\_space\_and\_kernel\_space#:\~:text=Kernel%20space%20is%20strictly%20reserved,software%20and%20some%20drivers%20execute.)/ hardware.

### Containers are...

* Isolated user spaces for running application code
* Lightweight bc they do not carry the full OS/ kernel code
* &#x20;Start/ stop quickly since processes start/stop much more quickly compared to VM bootup / shutdown&#x20;
* Portable&#x20;
* Enable use of [microservice design pattern ](https://en.wikipedia.org/wiki/Microservices)

### Container images

* &#x20;$$Image = Application + Dependencies$$
* A container is a running instance of an image&#x20;

### Enabling technologies of containers&#x20;

_Containers take advantage of various technologies inherent to the Linux operating system._&#x20;

* Processes
* Namespace
* cgroup
* Union file systems&#x20;

#### _Linux Process_

* Each Linux process has it's own virtual memory address space&#x20;
* Rapidly created and destroyed&#x20;

#### _Linux namespace_&#x20;

* Access control of what an application can see
  * Process ID (pid)
  * Directory trees&#x20;
  * IP addresses&#x20;
  * etc.
* Diff. from Kubernetes namespace&#x20;

#### _Linux cgroups_

* Resource management for an application
  * Max consumption limits for CPU, memory, I/O

#### _Linux Union file systems_&#x20;

* Encapsulate applications and dependencies into "clean" layers

### Structure of containers&#x20;

_Layers, layers, layers_&#x20;

* Image building tool reads instructions from the _container manifest_ file&#x20;
  * In Docker, this is the Dockerfile :whale:
  * GCP container build tool is called _Google Cloud Build,_ and it creates Docker-formatted containers&#x20;
* Each instruction/ command in the manifest file is a layer&#x20;
* Each layer is Read-only, but during execution a R/W ephemeral layer becomes the topmost layer (see container layer in diagram below)
* Organize your layers with least likely to change layer at the bottom/ base, to most likely to change. Note, that the "base" layer will be the first (top) line in your manifest file&#x20;
* Changes to the running container are written to the container layer, which is ephemeral. Meaning, changes will be lost when the container is deleted&#x20;
* Multiple containers can share access to the same underlying image with their own data-state&#x20;

![](<../../.gitbook/assets/image (4).png>)

### How to get containers?&#x20;

* Google's container registry is gcr.io&#x20;
  * GCP customers can store their private images here and use IAM to implement access control&#x20;
* Docker Hub registry&#x20;



{% hint style="success" %}
### Container Best Practices

* Do not build your application in the very same container you ship and run in production&#x20;
* Whenever you want to store data permanently, you must do so somewhere other than the container image&#x20;
{% endhint %}

### GCP Cloud Build

_GCP managed service to build containers_&#x20;

* Integrated with IAM
* Retrieves source code for builds from various storage locations&#x20;
* Define a series of build steps, which include but are not limited to:&#x20;
  * Fetch dependencies&#x20;
  * Compile source code
  * Run integration tests&#x20;
  * Run tools&#x20;
* Each build step runs in a Docker container&#x20;
* Delivers containers to various execution environments such as GitHub Enterprise (GHE) and Cloud Functions&#x20;

## GKE Overview

_GCP managed service that helps to deploy, manage and scale_ [_Kubernetes_](../kubernetes.md) _environments for containerized applications on GCP_

* Fully managed&#x20;
* Container-optimized OS managed by Google
* Auto upgrade
  * Ensures that clusters are automatically upgraded to latest version of Kubernetes&#x20;
* Auto repair
  * Unhealthy nodes are automatically repaired if a node is determined to be unhealthy during periodic health checks&#x20;
* Cluster scaling
* Seamless integration
  * Integrates with GCP Cloud Build
  * Integrates with GCP Container Registry&#x20;
  * Integrates with IAM
  * Integrates with Stackdriver for logging and monitoring&#x20;
  * GCP VPC
* Cloud console can be used to manage and view dashboards&#x20;

{% hint style="info" %}
The virtual machines that host containers inside of a GKE custer is referred to as a _**node**_&#x20;
{% endhint %}

## Kubernetes in GKE

This section documents specifics related to Kubernetes that are [documented here.](../kubernetes.md#architecture)

* GKE manages all control plane components&#x20;
  * Takes responsibility for provisioning and managing all control plane infrastructure&#x20;
* Instead of Kubernetes Admins manually creating nodes, GKE automatically deploys and registers [Compute Engine](google-cloud-fundamentals/#compute-engine) instances as nodes
* Node pool:Subset of nodes within a cluster that share a configuration. This is specific to GKE, although you can manually build out an analogous feature in Kubernetes&#x20;
  * note that there is some overhead&#x20;

![](<../../.gitbook/assets/image (7).png>)

### Zonal Clusters vs. Regional Clusters

* Cannot change zonal to regional or visa-versa&#x20;

![](<../../.gitbook/assets/image (6).png>)

### Private Clusters

![](<../../.gitbook/assets/image (10).png>)

### Object Management

#### Manifest files&#x20;

* YAML or JSON
* Defines a desired state for a pod -- name and specific container image to run&#x20;
  * ![](<../../.gitbook/assets/image (5).png>)****

{% hint style="success" %}
### **Object Management Best Practices**

* Define related objects in the same YAML file
* Version control manifest files
* Apply namespaces at the command line level to make YAML file for more flexibility&#x20;
{% endhint %}

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
* ![](<../../.gitbook/assets/image (2).png>)

#### Controller Objects and Pods

* Instead of defining separate individual pods, we can use a controller object whose job is to manage the state of the pods
  * Remember that pods are not self-healing&#x20;
* A **deployment** ensures that a defined set of pods is running at any given time
  * ![](<../../.gitbook/assets/image (8).png>)

_**Other controller objects**_ :arrow\_down:_****_

{% tabs %}
{% tab title="ReplicaSets" %}
* Ensures identical pods (population) are running at the same time&#x20;
* Can receive declarative updates from a Deployment object
{% endtab %}

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

#### Load-balanced Services&#x20;

* ClusterIP: Exposes the service on an IP address that is only accessible from within this cluster. This is the default type.&#x20;
* NodePort: Exposes the service on the IP address of each node in the cluster, at a specific port number.&#x20;
* LoadBalancer: Exposes the service externally, using a load balancing service provided by a cloud provider.

{% hint style="info" %}
In GKE, LoadBalancers give access to a regional [Network Load Balancing](https://txmx.gitbook.io/tech-notes/cloud-and-containers/gcp/google-cloud-fundamentals#cloud-load-balancing) configuration by default, but this can be modified.&#x20;
{% endhint %}

## References

* Google Cloud Training - Getting Started with Google Kubernetes Engine
