# 🧱 GCP Fundamentals

## Cloud Computing Definition

1. Customers get computing resources **on-demand** and via **self-service**
2. Resources are accessed over the network
3. Cloud provider has a big pool of resources and allocates to customers out of the pool
4. Resources are **elastic**, and therefore scalable
5. Pay as you go (or reserve)

## GCP Computing Architecure

* IaaS ---> Hybrid ---> PaaS (App Engine) ---> Serverless logic (Cloud functions) ---> Automated elastic resources (Managed services)&#x20;
* Google network is made of up hundreds of thousands kilometers of fiber cable, including subsea cables, more than 90 Internet exchanges and more than 100 Internet Points of Presence.&#x20;

### Thinking of GCP Infrastructure

GCP infrastructure can be compared to the infrastructure of a city.&#x20;

* People in the city are like users
* Buildings, cars and bikes are like applications
* Everything that goes into supporting those applications for the users is the infrastructure&#x20;

## Regions and Zones :earth\_africa:

* Services can be zonal, regional, or managed by Google across regions&#x20;
* A zone is a deployment area for GCP resources within a region.&#x20;
  * Single failure domain within a region&#x20;
  * For more fault tolerant apps, deploy across multiple zones&#x20;
  * Google Compute Engine VM are specific zone
* Regions are independent geographic areas that are made up of _zones_.
  * Disaster recovery plan necessary to recover your application if an entire primary region is lost&#x20;
  * Regional resources are deployed with redundancy within a region
* Multi-regional resources are managed by Google to be redundant and distributed across regions. Some tradeoffs may be necessary in terms of latency or consistency. Examples:
  * Google App Engine&#x20;
  * Google Cloud Datastore&#x20;
  * Google Cloud Storage&#x20;
  * Google BigQuery&#x20;

| Term              | Definition                                                                                                                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Region            | Specific geographical location where resources can be run                                                                                                                                       |
| Point of Presence | Where Google's network is connected to the Internet. Greater PoPs bring traffic                                                                                                                 |
| Zone              | <ul><li>Deployment area for GCP resources</li><li>Does not necessarily correlate to one physical data center</li><li>Grouped in regions</li><li>Single failure domain within a region</li></ul> |
| Multi-region      | Encompasses multiple regions. Resources that are allocated as multi-region means that data/ services are redundant in at least two geographic locations separated at least by 160 km            |

## Pricing&#x20;

* Per-second billing for IaaS compute engine, K8, and more&#x20;
* Auto-applied sustained-use discounts for certain services
* Online pricing calculator can help estimate costs&#x20;
* Open APIs and Open source services give customers ability to run applications via other CSP if Google is no longer a good fit&#x20;

## Accessing GCP

### Cloud Platform Console

* Web based, administrative user interface&#x20;
* Offers access to Cloud Shell
* APIs managed (enabled/ disabled) from Console

### Cloud Shell and SDK

* Command-line interface (CLI)
* Use SDK from the shell without installing SDK locally

#### SDK

* Set of tools to manage resources and applications in GCP
  * gcloud tool - main CLI
  * gsutil - GCP Storage&#x20;
  * bq - BigQuery&#x20;
* SDK can be installed locally on machine and also as a Docker image&#x20;

### Cloud console Mobile App

* For iOS and Android&#x20;

### REST API

* For custom apps&#x20;
* JSON
* OAuth 2.0 for authentication and authorization
* Quotas and limits apply, and an increase can be increased&#x20;

#### APIs Explorer

* Interactive tool that lets you try APIs using a browser&#x20;

#### Client Libraries&#x20;

* Cloud Client Libraries (Google Recommended)&#x20;
* Google API Client Libraries
  * Open source&#x20;
  * Multiple languages supported&#x20;

## Security :closed\_lock\_with\_key:

### Overview

* Security is designed into every layer of GCP technical infrastructure.&#x20;

| Layer                   | Notable security mesaures                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------- |
| Operational Security    | IDS, insider threat risk reduction measures, employee Universal 2nd Factor (U2F) use, secure SDLC |
| Internet communication  | Google Front End service, DoS protection built in                                                 |
| Storage services        | Encryption at rest                                                                                |
| User Identity           | Central Identity service w/ U2F support                                                           |
| Service deployment      | Encryption of inter-service communication (via remote procedure - RPC- calls)                     |
| Hardware infrastructure | Hardware designed and built by Google, secure boot stack, premises security                       |

### Shared-responsibility&#x20;

![](<../../../.gitbook/assets/image (2) (1) (1) (1) (1).png>)

### Resource Hierarchy Levels

* Levels of hierarchy provide trust boundaries and resource isolation&#x20;
* ![](<../../../.gitbook/assets/image (1) (1) (1) (1).png>)
* ![](<../../../.gitbook/assets/image (1) (1).png>)
* Resources (VM, Storage Bucket, etc.) --> Project(s) --> Folder(s) --> Organization&#x20;
  * All resources are organized into projects.
  * Projects can optionally be organized into folders, which can also contain subfolders
  * Folders and projects can be grouped together under an organization node

#### Policies&#x20;

* Contains a set of roles and role members&#x20;
* Inherited downwards in the hierarchy&#x20;
* Each level in the hierarchy can have policies defined to apply permissions, etc.&#x20;
* Can also be applied to individual resources&#x20;
* Resource policies are a union of parent and resource&#x20;
* Less restrictive parent policies override a more restrictive resource policy&#x20;
  * For example, suppose that a policy applied on the “bookshelf” project gives user Patricio the right to modify a Cloud Storage bucket. But a policy at the organization level says that Patricio can only view Cloud Storage buckets, not change them. The more "generous" policy takes effect&#x20;

#### Projects

* All services and resources belong to a GCP console project&#x20;
* Projects are the main way to organize resources in GCP
* Usually it makes sense to group resources together via a project because they have common business objectives&#x20;
* Three identifying attributes:&#x20;

| Attribute      | Uniqueness         | Chosen / Assigned | Mutability |
| -------------- | ------------------ | ----------------- | ---------- |
| Project ID     | Globally unique    | Chosen by you     | Immutable  |
| Project name   | Need not be unique | Chosen by you     | Mutable    |
| Project number | Globally unique    | Assigned by GCP   | Immutable  |

* Projects are used for:
  * Tracking resource and quota usage&#x20;
  * Billing
  * Managing permissions and credentials&#x20;
  * Enabling services and APIs&#x20;
* _Google Cloud Resource Manager_ API is used to programmatically manage projects in GCP. Accessed via REST API or RPC API
  * Get a list of all projects associated with the account&#x20;
  * Create new projects&#x20;
  * Update existing projects&#x20;
  * Delete projects&#x20;
  * Recover projects&#x20;

#### Folders :file\_folder:

* Optional
* Group projects or other folders under an organization
* Use folders to assign policies via <mark style="color:green;">Cloud IAM folders</mark>&#x20;
  * Resources in a folder inherit IAM policies assigned to the folder&#x20;
  * Assigning policies to folders instead of individual resources or projects is less tedious and less prone to errors&#x20;
* &#x20;Administrative rights can be delegated using folders, enabling teams to work independently&#x20;

#### Organization Node&#x20;

* Root node for GCP resources, though not \*required\*&#x20;
* Centralized visibility of how resources are being used (assuming the company has a single org. node).&#x20;
* Notable roles:
  * Organization Policy Admin - Broad control over all cloud resources&#x20;
  * Project Creator - Fine-grained control of project creation&#x20;
    * Good way to control who can spend money&#x20;
* Two ways to get an organization node:
  * Existing G Suite customer&#x20;
  * Use Google Cloud Identity&#x20;

### Identity and Access Management (IAM) :unlock:

_<mark style="color:green;">\<Who></mark> <mark style="color:blue;">\<can do what></mark>  <mark style="color:red;">\<on which resource></mark>_&#x20;

* IAM policies let admins authorize who can take what actions on specific resources&#x20;

#### <mark style="color:green;">Who can IAM policies apply to?</mark>&#x20;

Four types of principals (identity types)

| Principal Type                                  | Example                                   |
| ----------------------------------------------- | ----------------------------------------- |
| <p>Google account or<br>Cloud identity user</p> | <p>test@gmail.com<br>test@example.com</p> |
| Service account                                 | test@project\_id.iam.gserviceaccount.com  |
| Google group                                    | test@googlegroups.com                     |
| <p>Cloud Identity or <br>G Suite domain</p>     | example.com                               |

<details>

<summary>Notes on service accounts </summary>

* Identity that enables server-to-server interactions in a project&#x20;
* Authenticates from one service to another&#x20;
* Identified with an _email address_
* Use cryptographic keys to access resources instead of passwords&#x20;
* Service accounts are also a resource, meaning IAM policies can be attached to the account, allowing for different administrators to have different kinds of access to the account&#x20;
* Example usecase:&#x20;
  * &#x20;Application running in a virtual machine that needs to store data in Google Cloud Storage. But you don’t want to let just anyone on the Internet have access to that data; only that virtual machine. So you’d create a service account to authenticate your VM to Cloud Storage.

</details>

#### <mark style="color:blue;">Can do what?</mark>&#x20;

* Defined by an _<mark style="color:blue;">IAM role,</mark> which is a collection of permissions_&#x20;
* _<mark style="color:blue;"></mark>_![](<../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png>)_<mark style="color:blue;"></mark>_

_Three kinds of IAM roles to define who <mark style="color:blue;">can do what</mark>_&#x20;

{% tabs %}
{% tab title="Primitive" %}
* Broad roles
* Apply across all GCP services in a project
* Fixed & "course-grained" level of access roles, known as _basic roles_
  * Owner
  * Editor
  * Viewer&#x20;
* May be too broad if several people are working on a sensitive-data project together
{% endtab %}

{% tab title="Predefined" %}
* Apply to a particular GCP service within a project
* Fine-grained permissions to take actions on services
* &#x20;Example:
  * compute.instances.delete
  * compute.instances.get
  * compute.instances.list
  * compute.instances.SetMachineType
  * compute.instances.start
{% endtab %}

{% tab title="Custom/ Precise" %}
* Finest-grain of permissions&#x20;
* Enables least-privilege model
* Example: an "instanceOperator" role can be defined to allow some users to stop and start Compute Engine VMs, but not reconfigure them
* _Cannot be used at the folder level_; only project or organization level&#x20;
* With custom roles, admins need to manage the permissions that make up the custom roles, which could be burdensome&#x20;
{% endtab %}
{% endtabs %}

#### _<mark style="color:red;">On which resource</mark>_

* When you give a user, group, or service account a role on a specific element of the resource hierarchy, the resulting policy applies to the element you chose&#x20;

## List of Services&#x20;

### Compute&#x20;

* Compute Engine
* Kubernetes Engine
* App Engine&#x20;
* Cloud Functions&#x20;

### Storage&#x20;

* Bigtable&#x20;
* Cloud Storage&#x20;
* Cloud SQL
* Cloud Spanner
* Cloud Datastore&#x20;

### Big Data&#x20;

* BigQuery
* Pub/Sub
* Dataflow&#x20;
* Dataproc
* Datalab

### Machine learning

* Natural Language API
* Vision API
* Machine Learning
* Speech API
* Translate API

## Compute Engine&#x20;

### Overview&#x20;

* VMs can be built using GCP Compute Engine services&#x20;
* VMs can be created with GCP console or gcloud CLI tool
* Import images, create custom, or use common "cots" images&#x20;
* Choose pre-configured machine type, or custom define resources required&#x20;
* Many GCP zones have GPUs available for use&#x20;
* Storage options&#x20;
  * "Standard" / default: Persistent storage SSD
  * If high performing scratch space required - attach local SSD, but beware that the data here does not persist VM termination&#x20;
* Snapshots&#x20;
* Pre-emptable VMs&#x20;
  * Potentially good for batch jobs or any other work that can be interrupted&#x20;
  * Good for cost-savings&#x20;
* Auto-scaling feature&#x20;

### Notes on building a VM

{% hint style="info" %}
Startup scripts can be configured when building a VM if you know that you want certain packages to be installed or commands to be run during creation of the VM. (i.e. `apt-get install apache2 php php-mysql -y`)
{% endhint %}

### Virtual Private Cloud (VPC)

* VPC networks connect GCP resources to each other and/or to the internet
* Like on-prem networks, VPCs can be configured with&#x20;
  * firewall rules to restrict access where desired
  * static routes can be configured to route traffic to specific destinations&#x20;
* A new user getting started in GCP can create their own custom VPC or use the default&#x20;
* Firewall rules&#x20;
  * metadata tags can be used to apply firewall rules to resources (i.e. web servers can be tagged "web", and 80/443 traffic will be allowed for this tag)&#x20;

#### Scope

* VPCs have global scope and can have subnets in any GCP region worldwide
* Subnets can span the zones that make up a region (in other words, subnets have regional scope)
* Resources in different zones can still live on the same subnet

#### Scale

* Due to the nature and scope of VPC, networks and subnets can be dynamically scaled.&#x20;
  * If VPC has some virtual machines already configured to use IP addresses from a specific subnet, and that subnet size is increased, the existing VMs will not be affected&#x20;
* Recommendations:
  * Big VMs for in-memory DB and CPU intensive analytics&#x20;
  * Many VMs for fault tolerance and elasticity&#x20;

#### Cloud Load Balancing&#x20;

* Single, global anycast IP frontloads all of backend resources&#x20;
* Various load balancing options

{% tabs %}
{% tab title="Global HTTP(S)" %}
**Use case:** Load balancing for web applications ****&#x20;

**Capability & Caveats:**&#x20;

* Load balance layer 7 traffic based on load
* Different URLs can be routed to different back ends
* Traffic is balanced across regions&#x20;
{% endtab %}

{% tab title="Global SSL Proxy" %}
**Use case:** SSL (layer 4) balancing of non-HTTPS SSL traffic&#x20;

**Capability & Caveats:**&#x20;

* Only _specific_ port numbers supported&#x20;
{% endtab %}

{% tab title="Global TCP Proxy" %}
**Use case:** Layer 4 load balancing of non-SSL TCP traffic&#x20;

**Capability & Caveats:**&#x20;

* TCP only&#x20;
* Specific port numbers&#x20;
{% endtab %}

{% tab title="Regional" %}
**Use case:** Load balancing of any traffic (TCP, UDP)

**Capability & Caveat:**&#x20;

* Supported on _any_ port number&#x20;
* TCP or UDP&#x20;
{% endtab %}

{% tab title="Regional internal" %}
**Use case:** Load balancing of traffic inside a VPC

**Capability & Caveat:**&#x20;

* Use for internal tiers of multi-tier applications&#x20;
{% endtab %}
{% endtabs %}

#### Cloud DNS&#x20;

* Highly available, low latency, and scalable&#x20;
* Create managed DNS zones, then add, edit and delete DNS records&#x20;
* Programmatically manage zones and records using CLI or RESTful API

#### Cloud CDN (Content Delivery Network)

* Google globally distributed edge cache content geographically closer to your users&#x20;
* HTTPS cloud load balancing required, then enable Cloud CDN
* CDN Interconnect parter program with Google allows customers to continue to use external/ third-party CDN services&#x20;

#### Connecting other networks with GCP

* VPN using IPSEC using "Cloud Router"&#x20;
* Direct peering&#x20;
  * Relies on the customer being within a Google Point of Presence (of which there are many)
* Carrier peering&#x20;
  * If customer is not near a Google PoP, they can partner with a local carrier to provide that connection&#x20;
* Dedicated interconnect&#x20;
  * direct, private connections to Google&#x20;
  * SLA available&#x20;

## Storage&#x20;

* [Storage Overview ](./#storage)
* [Cloud Bigtable](./#google-cloud-bigtable)
* [Cloud SQL](./#undefined)
* [Cloud Datastore](./#cloud-datastore)

### Google Cloud Storage

* Fully managed, scalable service to store _objects_ (arbitrary number of bytes)
* Comprised of buckets to store objects
  * Access controls available for buckets&#x20;
    * ACL: Scope (who) + permission (what actions can be performed)&#x20;
  * Pick a region for your bucket that makes sense&#x20;
  * Globally unique name&#x20;
  * Storage class&#x20;

{% hint style="info" %}
_**When creating a bucket...**_

* Give it a globally unique name
* Specify geographic location for bucket and contents
* Choose a default storage class&#x20;
{% endhint %}

* Storage objects are immutable&#x20;
  * feature available to record history (object versioning).&#x20;
  * without versioning, new always overrides new&#x20;
* lifecycle management is available&#x20;
  * i.e. keeps only last 3 versions; delete all before \<specified date>; keep only last 12 months, etc.&#x20;
* Always encrypts data at rest and in transit
* Not a file system!&#x20;

### Four Cloud Storage classes&#x20;

{% tabs %}
{% tab title="Multi-regional" %}
**Intent:**&#x20;

* High performance obj storage
* Geo-redundant (at a slightly higher price point)
  * data is stored in at least two geographic locations separated by at least 160 km in the specified broad region (i.e. Asia, EU, USA)
* Frequently accessed data&#x20;

**Availability SLA:** 99.95%

**Access APIs:** Consistent APIs

**Access time:** Millisecond access

**Storage Price:** Price per GB stored per month

**Retrieval Price:** Total price per GB transferred

**Use cases:**

* Content storage & delivery&#x20;
* Website content
* Interactive workloads
* Data in mobile or gaming apps&#x20;
{% endtab %}

{% tab title="Regional" %}
**Intent:**&#x20;

* High performance obj storage
* Data that is accessed frequently within a single region

**Availability SLA:** 99.9%

**Access APIs:** Consistent APIs

**Access time:** Millisecond access

**Storage Price:** Price per GB stored per month

**Retrieval Price:** Total price per GB transferred

**Use cases:**

* In-region analytics&#x20;
* Transcoding
* Store data close to other resources that are using the data (i.e. Compute Engine VM or Kubernetes Engine clusters)
{% endtab %}

{% tab title="Nearline" %}
**Intent:**&#x20;

* Backup/ archival storage
* Low-cost, infrequently accessed data&#x20;

**Availability SLA:** 99%

**Access APIs:** Consistent APIs

**Access time:** Millisecond access

**Storage Price:** Price per GB stored per month

**Retrieval Price:**  Total price per GB transferred

**Use cases:**

* Long-tail content&#x20;
* pulling data once a month or less for analysis
* Backups
{% endtab %}

{% tab title="Coldline" %}
**Intent:**&#x20;

* Backup/ archival storage (very-low cost)

**Availability SLA:** 99%

**Access APIs:** Consistent APIs

**Access time:** Millisecond access

**Storage Price:** Price per GB stored per month

**Retrieval Price:** Total price per GB transferred&#x20;

**Use cases:**&#x20;

* Archiving
* Disaster recovery
* Data that is planned to be accessed for once a year or less&#x20;
{% endtab %}
{% endtabs %}

### Bring data into Cloud Storage

* Online transfer
* Storage Transfer Service
* Transfer appliance&#x20;
* Via various GCP products and services&#x20;
  * Import and export tables to Cloud storage _from BigQuery_
  * Store _App Engine logs, Cloud DS backups, objects used by App Engine applications like images_&#x20;
  * Store instance startup scripts, Compute Engine images and objects used by _Compute Engine_ apps&#x20;
  *

#### Online transfer&#x20;

* self-managed movement of data either via the GCP console, or _gsutil_ (Cloud Storage command from Cloud SDK)

#### Storage Transfer Service

* Schedule and manage batch transfers to Cloud storage from various endpoints
  * Another cloud provider
  * Different cloud storage region
  * HTTPS endpoint&#x20;
* Good for transferring TB or PB of data&#x20;

#### Transfer Appliance&#x20;

* Rackable, high-capacity storage server leased from Google Cloud
* Load with data in your data center, then ship it to an upload facility to be uploaded to Cloud Storage&#x20;
* Service is in beta at the time of these notes&#x20;

## Google Cloud Bigtable&#x20;

### Cloud Bigtable is...

* NoSQL database&#x20;
  * Not a relational database
  * Not every row (entry) needs to have the same column&#x20;
  * More like a dictionary/[ hash table](https://en.wikipedia.org/wiki/Hash\_table#:\~:text=In%20computing%2C%20a%20hash%20table,desired%20value%20can%20be%20found.) or JSON structure&#x20;
* Fully managed database service&#x20;
* Ideal for apps that need high throughput and scalability for non-structured key/value pair data&#x20;
* Ideal for large quantities of semi-structured or structured data (> 1 TB)
* Used in many of Google's core services such as: Gmail, Search, Maps, and Google Analytics
* Same API as HBase (native Hadoop database), which enables portability between HBase and Bigtable&#x20;
* Encrypted in-transit and at-rest by default
* Able to restrict access via Role-based ACLs
* Use cases:
  * Marketing data&#x20;
  * Financial data such as transaction histories, stock prices, exchange rates
  * IoT data&#x20;
  * Time-series data&#x20;
  * Running machine learning algorithms on the data&#x20;

### Bigtable Access Patterns&#x20;

#### Application API

* Data can be read from and written to Bigtable through a data service layer such as&#x20;
  * Managed VMs
  * HBase REST Server
  * Java Server using HBase client
* Typical usecase for this is serving data to applications, dashboards and data services&#x20;

#### Streaming&#x20;

* Cloud Dataflow Streaming service
* Spark streaming&#x20;
* Storm

#### Batch Processing&#x20;

* Hadoop MapReduce
* Dataflow
* Spark

## Cloud SQL

### Cloud SQL is...

* _**Managed**_ Relational Database Services (RDBMS)
  * MySQL
  * PostgreSQL
* Advantages of using RDBMS as a service (versus BYO in Compute Engine VM)
  * Automatic replication
  * Managed backups (on-demand or scheduled)
  * Vertical and horizontal scaling&#x20;
  * Google security
  * Accessible from other GCP services and third-party services/ tools&#x20;

### Cloud Spanner is...

* Horizontally scalable RDBMS
* Supports...
  * Automatic replication
  * Strong transactional "global consistency"
  * HA managed instances&#x20;
* Use cases&#x20;
  * Outgrown relational db&#x20;
  * Financial apps&#x20;
  * Inventory apps&#x20;

## Cloud Datastore&#x20;

_Highly scalable, NoSQL DB_

### Usecases

* Designed for application backends&#x20;
* Store structured data from app engine applications&#x20;

### Supported Features&#x20;

* [ACID](https://en.wikipedia.org/wiki/ACID) Transactions&#x20;
* Fully managed&#x20;
* Redundancy&#x20;
* Distributed architecture automatically manages scaling&#x20;

### Benefits&#x20;

* Schemaless&#x20;
* Free daily quota&#x20;
* Accessible via RESTful API

## Comparing Storage Options

|                           | Cloud Datastore                                                                   | Bigtable                                                                                       | Cloud Storage                                                        | Cloud SQL                                                   | Cloud Spanner                                                     | BigQuery                                                          |
| ------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Type**                  | NoSQL document                                                                    | NoSQL wide column                                                                              | Blobstore                                                            | Relational SQL for OLTP                                     | Relational SQL for OLTP                                           | Relational SQL for OLAP                                           |
| **Best for**              | <ul><li>Semi-structured application data</li><li>Durable key-value data</li></ul> | <ul><li>"Flat" data</li><li>Heavy read/ write</li><li>Events</li><li>Analytical data</li></ul> | <ul><li>Structured and unstructured binary or object data </li></ul> | <ul><li>Web frameworks</li><li>Existing apps</li></ul>      | <ul><li>Large-scale database applications (> ~2TB)</li></ul>      | <ul><li>Interactive querying</li><li>Offline analytics </li></ul> |
| **Use cases**             | <ul><li>Getting started </li><li>App engine applications</li></ul>                | <ul><li>AdTech</li><li>Financial data</li><li>IoT data</li></ul>                               | <ul><li>Images</li><li>Large media files</li><li>Backups</li></ul>   | <ul><li>User credentials </li><li>Customer orders</li></ul> | <ul><li>Whenever high I/O/ global consistency is needed</li></ul> | <ul><li>Data warehousing</li></ul>                                |
| **Transactions**          | Yes                                                                               | Single-row                                                                                     | No                                                                   | Yes                                                         | Yes                                                               | No                                                                |
| **Complex Query Support** | No                                                                                | No                                                                                             | No                                                                   | Yes                                                         | Yes                                                               | Yes                                                               |
| **Capacity**              | TB +                                                                              | PB +                                                                                           | PB +                                                                 | Up to \~10 TB                                               | PBs                                                               | PB +                                                              |
| **Unit size**             | 1 MB / entity                                                                     | <p>~ 10 MB / cell<br>~ 100 MB / row</p>                                                        | 5 TB/ object                                                         | Determined by DB engine                                     | 10,240 MiB/ row                                                   | 10 MB / row                                                       |
|                           |                                                                                   |                                                                                                |                                                                      |                                                             |                                                                   |                                                                   |

## Containers in GCP

* Recall GCP services Compute Engine -- IaaS offering, and GCP App Engine -- PaaS offering

### [Containers](../google-kubernetes-engine.md#containers-are...)&#x20;

#### What are they?

* get independent scalability of workloads, similar to PaaS, and also an abstraction of hardware, similar to IaaS
* Containers run as processes (compare with boot time of an OS)
* OS virtualization (vs. hardware virtualization as with a VM)
* Tools to build and run containers&#x20;
  * [Docker](../../docker/docker.md#dockerfile)&#x20;
  * GCP Service - Google Container Builder
* Loosely coupled to environment&#x20;
  * Consumes less resources and less error-prone than deploying an app in a VM
  * Easy to move around&#x20;
  * Abstract underlying OS details away from app
* Each container _does not_ have it's own instance of the OS

#### Why are they useful?&#x20;

* Scalable and flexible&#x20;
* Abstraction makes code very portable&#x20;
* Apps can be moved with minimal re-work effort (i.e. between dev-test-prod or between local host and cloud)

#### How are they managed at scale?&#x20;

Following a microservices architecture, containers running specific services of your app can start, stop, scale as needed.&#x20;

_Kubernetes_ is a tool that helps to manage the moving parts that come with the scenario mentioned above&#x20;

* Orchestrate many containers on many hosts
* Scale
* Roll out new versions, or roll back to an old version

### [Kubernetes](../../kubernetes.md) and [GKE](../google-kubernetes-engine.md)

* Kubernetes is an open source orchestrator to better manage and scale applications&#x20;
* Containers can be deployed on a set of _nodes_ called a _cluster_&#x20;
  * Cluster is a set of master components that control the system as a whole and set of nodes.&#x20;
  * A cluster can be thought of as a group of machines where Kubernetes can schedule workloads
  * In kubernetes - node represents a computing instance&#x20;
* Pod - smallest deployable unit inside kubernetes&#x20;
  * running process inside of cluster&#x20;
  * Multiple containers with a hard dependencies can be packaged into a single pod which will be able to communicate locally on&#x20;
* Deployment&#x20;
  * `rollingUpdate` is an attribute of a deployment that allows you to tell kubernetes how you want to roll out updates to your app to your users. This is a way to mitigate risk so that updates can be pushed safely without suffering downtime&#x20;
* Service&#x20;
  * groups a set of pods together and provides a stable endpoint to access (i.e. a public IP managed by a load-balancer)&#x20;
* Configuration files
  * Tells kubernetes what you want desired state of the app to look like&#x20;
  * .yaml file to declaritively tell kubuernetes how to manage your service&#x20;

#### Google Kubernetes Engine (GKE)

* Resources used to build Kubernetes Engine clusters come from Compute Engine
  * Because of this, GKE gets to take advantage of Compute Engine's and Google VPC capabilities
* The Kubernetes Engine team at Google periodically performs automatic upgrades of customer clusters to newer, stable versions of Kubernetes&#x20;

#### How to get a kubernetes cluster?&#x20;

* GCP managed service provides Kubernetes Engine&#x20;
  * use console&#x20;
  * or use gcloud&#x20;

### Anthos&#x20;

* Google's modern solution for hybrid and multi-cloud systems and services management&#x20;
* Built on Kubernetes and GKE foundation&#x20;

## App Engine

* GCP App Engine service is a PaaS for building scalable applications&#x20;
* Application infrastructure is managed for you, enabling developers to focus on innovating applications&#x20;
  * For example, App Engine manages the hardware and networking infrastructure required to run code
* Especially suited for web applications and mobile backends or other applications where the workload is highly variable
  * App Engine will scale applications automatically in response to the amount of traffic it receives&#x20;

### App Engine Standard Environment&#x20;

* Easily deploy and scale
* Free daily quota, and additional resources are priced by usage&#x20;
* SDK available for dev, test and deployment&#x20;
* Based on container instances running on Google's Infrastructure&#x20;

#### Preconfigured runtimes available in STD env

* Java
* Python
* Go
* PHP

{% hint style="info" %}
If you want to code in a language not covered in the preconfigured runtimes, use of the App Engine flexible environment would be a better option
{% endhint %}

#### Sandbox constraints

* Use of the App Engine Standard environment requires your code to run in a sandbox, which imposes some constraints to be aware of&#x20;
  * No writing to local file system (must use db service instead)
  * Requests time out at 60 seconds
  * 3rd party software installation is limited

### App Engine Flexible Environment

* Gives more flexibility and control over runtimes for apps&#x20;
  * Owners can control the geographic region where they run&#x20;
* Allows you specify which _Docker container_ to run your apps on&#x20;
* Allows SSH access

### App Engine Std. vs Flexible vs Kubernetes

![](<../../../.gitbook/assets/image (1).png>)

![](<../../../.gitbook/assets/image (2) (1) (1) (1).png>)

## Cloud Endpoints and Apigee Edge

### Cloud Endpoints

* helps to create an maintain APIs for your applications&#x20;
* Control access and validate calls with JSON web tokens and Google API keys
  * id web and mobile users with Auth0 and Firebase authentication
* Generate client libs&#x20;
* Supports multiple GCP services/ runtime environments
  * App Engine Flexible Environment
  * Kubernetes engine
  * Compute engine&#x20;

### Apigee Edge

* Helps to secure and monetize APIs&#x20;
* A platform for making APIs available to customers and partners
  * i.e. paying for access to an API such as a Threat Intel provider, or exclusive data from ESPN.com&#x20;
  * Good to use if you want to gradually decompose a pre-existing monolithic application, not implemented in GCP, into microservices



## Development in the Cloud

### Cloud Source Repositories&#x20;

* GCP managed Git repository service

### Cloud Functions&#x20;

* Single purpose functions that responds to events without a server or runtime&#x20;
* Cloud functions are written in JS
* Use beyond the perpetual monthly free tier is billed in 100 ms increments&#x20;

## Deployment: Infra as Code

### Deployment Manager

* GCP Infrastructure management service
* To use it, create a .yaml or python template file describing what the components of the environment&#x20;
* templates can be stored and placed under version control in Cloud Source Repos
* quickly deploy functional software packages by using pre-defined templates with Deployment Manager service&#x20;
* templates are combo of yaml, python and jinja2

## Monitoring: Proactive Instrumentation

### Stackdriver

_GCP monitoring and logging service_&#x20;

* Provides insights into:
  * health
  * availability&#x20;
*   Core Components&#x20;

    * Monitoring
      * create dashboards and alerts&#x20;
    * Logging
      * view, search and filter logs from your application
      * define metrics based on logs&#x20;
    * Trace
    * Error reporting
    * Debugger



## Big Data and ML in GCP

Big data services are fully managed and scalable&#x20;

* Only pay for resources you consume

### Cloud Dataproc

* Managed way to run Hadoop, Spark, Hive, Pig
* Map/ Reduce&#x20;
* Easily migrate on-prem Hadoop jobs to cloud&#x20;
* Save money with pre-emptible instances for batch processing
* Billed by the second (subj. to 1 min minimum)&#x20;
* Once data is in a cluster, use Spark ML libraries to discover patterns&#x20;
* Good for there is a dataset of a known size

### Cloud Dataflow

* Good for streaming data or handling a dataset of an unknown size
* Managed data pipelines&#x20;
* Reads from a source (source) --> processes in a variety of ways (transforms) --> writes/ outputs to a storage solution (sink)
* used for&#x20;
  * extract/ transform/ load (ETL)
  * data analysis&#x20;
  * real-time applications such as gaming&#x20;

### BigQuery

* Fully managed data warehouse (pb scale)
* No cluster maintenance is required&#x20;
* Use SQL queries to query data&#x20;
* Free monthly quotas&#x20;
* scalable&#x20;
* 99.9 sla
* only pay for queries when they are run&#x20;
* price reduction for longterm storage (first reduction at 90 days)

### Cloud Pub/Sub

_Pub = Publishers ; Sub = Subscribers_&#x20;

* Simple, reliable, scalable foundation for stream analytics&#x20;
* Messaging service
* Building block for apps where data arrives at high and unpredictable rates&#x20;
  * i.e. IoT, Marketing analytics&#x20;
* Subscribers can be configured on push/ pull basis

### Cloud Datalab

* Built on Jupyter lab/ jupyter notebook&#x20;
* Integrates with other GCP services
  * BigQuery
  * Compute Engine
  * Cloud Storage
* Easily deploy models to BigQuery&#x20;

### Machine Learning Platform

* Available as a cloud service&#x20;
* TensorFlow is an open source machine learning software library that is useful for building ML apps
* Fully managed machine learning service
  * Cloud ML service
* Pre-trained machine learning models as a service using various APIs
  * Speech
    * convert audio to text
  * Vision
    * gain insight
    * detect inappropriate content&#x20;
    * analyze sentiment&#x20;
    * extract text&#x20;
  * Natural Language API
    * reveal structure and meaning of text
    * extract info about items mentioned in text docs, news articles, and blog posts&#x20;
  * Translation API
  *   Video intelligence api (beta)

      * annotate contents of videos
      * detect scene changes
      * flag inappropriate content&#x20;



#### Cloud Machine Learning Platform Use cases

**Structured data**

* classification and regression
* recommendation
* anomaly detection&#x20;

#### Unstructured data&#x20;

* Image analytics&#x20;
* Text analytics&#x20;

## References:

* Cloudskillboost Google Course: Google Cloud Fundamentals: Core Infrastructure
