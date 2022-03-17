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

#### Linux namespace&#x20;

* Access control of what an application can see
  * Process ID (pid)
  * Directory trees&#x20;
  * IP addresses&#x20;
  * etc.
* Diff. from Kubernetes namespace&#x20;

#### Linux cgroups

* Resource management for an application
  * Max consumption limits for CPU, memory, I/O

#### Linux Union file systems&#x20;

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

### Container Best Practice Notes

* Do not build your application in the very same container you ship and run in production&#x20;
* Whenever you want to store data permanently, you must do so somewhere other than the container image&#x20;

## GCP Cloud Build

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

## References:

* Google Cloud Training - Getting Started with Google Kubernetes Engine
