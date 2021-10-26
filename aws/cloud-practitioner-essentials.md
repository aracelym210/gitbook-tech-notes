# AWS Cloud Practitioner Essentials

- AWS Cloud Concepts 
- AWS Services 
- Security in AWS
- AWS Architecture 
- AWS Pricing 
- AWS Support
- AWS Certified Cloud Practitoner Exam

## Module 1 - Overview of Cloud Concepts 
- **Benefits of AWS**
  - Flexibility of using resources as needed, and returning when no longer needed.
    - Makes it easier to develop and deploy applications  
  - Undifferentiated heavy lifting of IT (routine, repetive tasks) 
  - Trade upfront expense for variable expense 
    - Upfront expense = data centers, physical servers, etc. which requires payment before use
    - Variable expense = pay only for what you need
  - Focus less on managing infrastructure and servers and focus more on applications and customers 
  - Economies of scale allows AWS to provide lower pay-as-you-go prices
  - Applications can be deployed across the world quickly, providing customers around the world with low-latency 
- **Differences between on-demand delivery and cloud deployments**
  - "On-demand delivery" indicates that resources are available as you need them, when you need them. Additionally, resources can be returned when not needed.
  
    | Cloud-based Deployment | On-Premises Deployment | Hybrid Deployment | 
    | --------------------- | --------------------- | ------------------- | 
    | Run all parts of application in the cloud | Deploy resourcs by using virtualization and resource management tools | Connect cloud-based resources to on-premises infrastructure | 
    | Migrate existing applications to the cloud | Increase resource utilization by using app mgmt and virtualization technologies | Integrate cloud-based resources with legacy IT applications | 
    | Design and build new applications in the cloud | Aka "private cloud." | | 

### Definitions
- **Cloud computing:** The on-demand delivery of IT resources over the internet with pay as you go pricing 

## Module 2 - Elastic Compute Cloud (EC2)
- EC2 is enabled by multi-tenancy: sharing underlying hardware between virtual machines (via hypervisor that manages)
### Benefits of Elastic Compute Cloud (EC2) 
- Highly flexible
- Cost-effective
- Quick 

### Identify different EC2 instance types 
- Each is grouped under an instance family
- Each instance family offers various combinations of CPU, storage, memory, and networking capacity

| Instance Family Type | Notes | 
| -------------------- | ------ | 
| General purpose | Balanced resources; <br>Diverse workloads; <br>Web servers; <br> Code repos | 
| Compute optimized | Compute intesive tasks; <br>Gaming servers; <br>High Performance Computing (HPC); <br>Scientific modeling; <br>Also useful for batch processing workloads that require processing many transactions in a single group | 
| Memory optimized | Designed to deliver fast performance for workloads that process large datasets in memory. <br>High performance database; <br>Workload that involves performing real-time processing of a large amount of unstructured data. | 
| Accelearated computing | Floating point number calculations; <br>Graphics processing; <br>Data pattern matching; <br>Utilize hardware accelerators (coprocessors) | 
| Storage optimized | Workloads that require high sequential read and write access to large datasets on local storage; <br>Distributed file systems; <br>Data warehousing applications; <br>High frequency online transaction processing systems; <br>Applications with high IOPS (I/O) requirements. | 
  
### Differentiate between various billing options for EC2
| Name of Billing Option | Description | Use cases | Other notes | 
| ---------------------- | ------------ | --------- | ----------- | 
| On-demand purchase | only pay for duration that instance is run (per hour or per second, depending on OS and build) | | | 
| Savings plan |low prices on EC2 prices, in exchange for commitment to usage for 1 or 3 year term. | | |
| Reserved instances | Requires 1 or 3 year commitment, *plus* payment in one of three ways. (1) All up front. (2) Partial upfront. (3) No upfront. | | | 
| Spot instances | Can save up to 90%, with the catch/ caveat that AWS can reclaim resources whenever needed, with only a 2 minute warning. | | | 
| Dedicated hosts | No shared-tenancy of the host. | Usually used for compliance reasons | | 
###  Summarize benefits of Amazon EC2 Auto Scaling 
### Summarize benefits of Elastic Load Balancing
### example uses for Elastic Load Balancing
### Differences between Amazon Simple Notification Service (SNS) and Simple Queue Service (SOS)
### Additional AWS compute options 
