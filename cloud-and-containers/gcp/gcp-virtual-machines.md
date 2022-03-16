# GCP Virtual Machines

## Compute Engine&#x20;

* "Traditional" virtual machine&#x20;
* Pure Infrastructure as a Service (IaaS)
* Primary usecase: any general workload, especially any application designed to run on a traditional server&#x20;
* Pre-defined and custom machine types allow you to mix-match desired resources&#x20;

### Compute Options&#x20;

* Specifications for currently [available VM machine types can be found here](https://cloud.google.com/compute/docs/machine-types)

#### Machine Family - (four types)

* curated set of processor and hardware configs optimized for specific workloads&#x20;
* _**General-purpose**_

![](<../../.gitbook/assets/image (2).png>)

* Compute-optimized

![](<../../.gitbook/assets/image (4).png>)

* Memory-optimized

![](<../../.gitbook/assets/image (7).png>)

* Accelerator-optimized

![](<../../.gitbook/assets/image (6).png>)

#### Machine Series

#### Machine Type

![Machine type structure](<../../.gitbook/assets/image (5).png>)

### Storage Options

* Harddisk vs SSDs -- performance vs. cost
  * SSDs designed for higher IOPs per dollar vs. std disk&#x20;

### VM access and lifecycle&#x20;

* Changing VM state from running&#x20;
  * console, gcloud, API, OS
  * **relevant when writing shutdown / startup scripts for preemptible VMs**&#x20;

### Patch mangement&#x20;

* os patches can be applied across a set of compute engine vm instance&#x20;
* Create patch approvals&#x20;
* Flexible scheduling
* Customize with pre/ post scripts&#x20;

### Billing/ Pricing

* You do not pay for memory or cpu resources when a VM is terminated, but any attached disks and reserved IPs will incur a charge&#x20;
* Sustained use discounts&#x20;
* Pre-emptible discounts&#x20;

