# 💻 GCP Virtual Machines

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

![](<../../.gitbook/assets/image (2) (1).png>)

* Compute-optimized

![](<../../.gitbook/assets/image (4) (1).png>)

* Memory-optimized

![](<../../.gitbook/assets/image (8) (1) (1).png>)

* Accelerator-optimized

![](<../../.gitbook/assets/image (6) (1) (1) (1).png>)

#### Machine Type

![Machine type structure](<../../.gitbook/assets/image (5) (1).png>)

### Storage Options :minidisc:

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

### Preemptible Resources&#x20;

* Up to 80% savings cost
* VM may be terminated at any time
  * No charge if term'd in first minute
  * 24 hours max
  * 30 second terminate warning, but not guaranteed&#x20;
    * **shutdown script**
* Monitoring and load balancers can be setup to start new preemptible VMs in case of a failure
* Good for batch processing jobs&#x20;

### Shielded VMs

* Offer verifiable integrity to VMs (ensure VMs have not been infected with rootkits)
* Secure boot
* Virtual trusted platform module (vTPM) helps prevent exfil
* Requires "shielded image"

### Confidential VMs

* Encrypts data while it's being processed&#x20;
* N2D Compute Engine VM
* High memory capacity
* Data is encrypted in memory when processing
* Google does not have access to encryption keys&#x20;

### Sole-tenant nodes&#x20;

* Keep your instances physically separated from other customers if needed for compliance or other reason&#x20;

![](<../../.gitbook/assets/image (3).png>)

### Images&#x20;

* Public or custom image (Linux or Windows)&#x20;
* Premium (p) images have special costs&#x20;
* Create custom image with pre-configured and installed SW

#### Machine image&#x20;

_Compute engine resource that stores all the configuration, metadata, permissions and data from one or more disks required to create a virtual machine instance._

* Used in creation, backup recovery and instance cloning&#x20;

### Disk options&#x20;

![](<../../.gitbook/assets/image (7) (1) (1).png>)

* Boot disk&#x20;
* Persistent disk&#x20;
  * attached to VM through network interface&#x20;
  * snapshots&#x20;
  * dynamically resizable&#x20;
  * can be attached in read-only mode to multiple VMs&#x20;
* Local SSD disks
  * ephemeral&#x20;
  * high in iops&#x20;
  * data survives reset, but not terminate&#x20;
* RAM disk

### Common Compute Engine actions&#x20;

* every VM instance stores its metadata on a metadata server&#x20;
* VMs can be moved between zones if:
  * vm is in a terminated state or&#x20;
  * vm instance is a shielded VM that uses UEFI firmware&#x20;
  * can be moved between same region or move to a different region, but there are manual actions required for moving to a different region altogether&#x20;
* Snapshots
  * persistent disk snapshots (snapshots cannot be done on local ssd)

### Billing/ Pricing :moneybag:

* You do not pay for memory or cpu resources when a VM is terminated, but any attached disks and reserved IPs will incur a charge&#x20;
* Sustained use discounts&#x20;
* Preemptible discounts&#x20;

## References&#x20;

* Cloudskillsboost - Essential Google Cloud Infrastructure: Foundation
