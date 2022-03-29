---
description: Notes on Google Virtual Private Cloud
---

# 🌐 GCP VPC

* Comprehensive set of Google managed networking objects&#x20;
  * Projects
  * Networks&#x20;
    * default
    * auto
    * custom
  * Subnetworks&#x20;
  * Regions & zones&#x20;
  * Internal and external IP addressing&#x20;
  * Routes & firewall rules&#x20;

## Projects, Networks and Subnets&#x20;

### Projects

* Projects are the key organizer of resources in GCP
* Associates objects and services with billing&#x20;

### Networks&#x20;

* Networks are contained within projects&#x20;
* Default network quota per project is five networks&#x20;
  * Additional can be requested through the cloud console&#x20;
* Networks can be _shared_ with other projects or _peered_ with networks in other projects&#x20;
* Networks are global resources, meaning they span across all GCP regions&#x20;
* Like in on-premise networking, networks can be segregated into subnets&#x20;
* Instances in separate regions, because of Google private network, these instances can still talk to each other without going through the internet&#x20;

{% hint style="info" %}
Three types of network in GCP:&#x20;

1. Default
2. Auto Mode (not recommended for production)
3. Custom Mode
{% endhint %}

{% tabs %}
{% tab title="Default" %}
* Every project is provided w/ default VPC network
* One subnet per region
* Default firewall rules:&#x20;
  * Allow ingress ICMP, ORDP and SSH from \*&#x20;
  * Allows intranetwork traffic from within the default network&#x20;
{% endtab %}

{% tab title="Auto Mode" %}
* Default network _is_ an auto mode network
* One subnet per region is automatically created&#x20;
  * predefined IPs with /20 mask that can expand to /16
  * All subnets fit within 10.128.0.0/9
* Not recommended for production (convert to custom mode instead)
{% endtab %}

{% tab title="Custom Mode" %}
* No default subnets created&#x20;
* Full control of IP ranges&#x20;
* Regional IP allocation
* Expandable to IP ranges specified&#x20;
  * Cannot overlap between subnets of the same network&#x20;
* You can convert auto mode network to custom mode network, but you cannot do the reverse&#x20;
{% endtab %}
{% endtabs %}

## IP addresses

* Every VM that starts up and any service that depends on a VM gets assigned an internal IP address&#x20;
  * i.e. App Engine, GKE
* DNS is scoped to the network
  * Can translate VM names of hosts in same network
  * Cannot translate VM names in a different network&#x20;
* By default, external IP addresses are ephemeral&#x20;

### Alias IP ranges&#x20;

* Useful if you have multiple services running on a VM and you want to assign a different IP address to each service
  * Sounds like an A record / CNAME record?&#x20;
* Essentially, you can configure multiple IP addresses representing containers or applications hosted in a VM

![](<../../.gitbook/assets/image (3) (1) (1) (1).png>)

## DNS&#x20;

* Each VM instance has a metadata server that also acts as a DNS resolver for that instance. This metadata server handles all DNS queries for local network resources and routes all other queries to Google's public DNS servers&#x20;

### Resolution for internal addresses&#x20;

* Each instance has a hostname that can be resolved to an internal IP address
  * Hostname is same as instance name&#x20;
* Name resolution handled by internal dns resolver
  * Provided as part of Compute Engine (169.254.169.254)
  * routes other queries to Google's public DNS servers for public name resolution
* Instance is not aware of external IP address assigned to it&#x20;
  * External IP address is unknown to the OS of the VM. Running `ifconfig`, for example, will only return the internal IP address.&#x20;
    * External IPs are _mapped_ to the VM's internal address transparently by VPC
* The network stores a lookup table that matches external IP addresses with the internal IP addresses of relevant instances&#x20;

### Resolution for external addresses&#x20;

* Managed GCP service, Cloud DNS
* Public DNS records are not published automatically&#x20;
* DNS records for external addresses can be published using existing DNS servers
* DNS zones can be hosted using Cloud DNS

#### Cloud DNS

* Scalable, reliable and managed authoritative dns service&#x20;
* 100% up-time SLA for domains configured in cloud dns

## Routes and Firewall rules&#x20;

### Cloud Routes&#x20;

* Route is mapping of IP address to a destination&#x20;
* Route is created when a network or when a subnet is created&#x20;
* each route may apply to one or more instances&#x20;
  * if network and instance tags match
  * If network matches and there are no instance tags specified, the route applies to all instances in that network&#x20;
* Instance routing tables&#x20;
* Need to have a firewall rule to match your route or else no traffic will flow&#x20;

### Cloud Firewall rules&#x20;

{% hint style="info" %}
**All VPCs** have 2 implied firewall rules&#x20;

1. All all outbound traffic&#x20;
2. Block all incoming traffic&#x20;
{% endhint %}

{% hint style="info" %}
Default VPCs have additional allow rules&#x20;

1. `default-allow-internal`
2. `default-allow-ssh`
3. `default-allow-rdp`
4. `default-allow-icmp`
{% endhint %}

* VPC network functions as a distributed firewall&#x20;
* Rules are applied to the network as a whole
* Protect VM instances from unapproved connections&#x20;
* Connections allowed or denied at the instance level&#x20;
* Stateful&#x20;
* Implied deny all ingress and allow all egress&#x20;

#### Rule attributes&#x20;

* direction&#x20;
* source or destination&#x20;
* protocol and port&#x20;
* action
* priority
* rule assignment&#x20;

![](<../../.gitbook/assets/image (4) (1) (1) (1).png>)

#### Firewall best practices&#x20;

{% hint style="success" %}
1. Principle of least privilege&#x20;
2. Minimize direct exposure to/from Internet&#x20;
3. Explicit deny as last rule (lowest priority)
4. Develop standard naming convention&#x20;
5. Consider service account firewall rules instead of tag-based rules
   1. tag-based rules requires less privileges&#x20;
   2. One issue with tags is that they must be added to instances and could possibly be added or removed inadvertently. Firewall rules can also be applied to instances by the service account used. These rules will be applied automatically to all instances that use the specified service account.
{% endhint %}

#### Default-deny traffic&#x20;

![](<../../.gitbook/assets/image (11).png>)

#### Firewall insights&#x20;

* Help better understand and optimize firewall rules&#x20;
* Helps to analyze the way that firewall rules are being used&#x20;
  * identify firewall misconfigs&#x20;
  * id security attacks
  * optimize firewall rules and tighten security boundaries&#x20;

## Multiple network interfaces

* VPC networks are isolated by default&#x20;
* Internal IP address communication is not allowed between networks unless you set up a mechanism such as VPC peering or VPN.
* Additional network interfaces can be setup on an instance which will enable you to create configurations that allow the instance to connect directly to several VPC networks
* Each interface can have external IP addresses

### Usecase for multiple interfaces

* Network appliances such as IDS, firewall, load balancing, etc.&#x20;

### Limitations&#x20;

![](<../../.gitbook/assets/image (11) (1) (1).png>)

## VPC Interconnect Peering

### VPC Network Peering&#x20;

* Allows connection of two non-overlapping VPC networks, which enables resources in the separate networks to communicate over private IP space&#x20;
* Do not need to be in same project or the same organization&#x20;
* Rules need to be configured in each network&#x20;
* Up to 25 peers allowed&#x20;

#### Pros:

* Decreased network latency&#x20;
* Increased security due to minimizing exposure to internet&#x20;
* Reduced egress cost&#x20;

### Shared VPCs

* Makes a VPC network shareable across several projects in the organization&#x20;
* Requires host project within the same organization&#x20;

![](<../../.gitbook/assets/image (10).png>)

### Cloud Interconnect&#x20;

* Dedicated interconnect: direct physical connection between on-prem and GCP VPC networks
* Partner Interconnect

## Load balancing&#x20;

### Managed Instance Groups

* Identical instances can be deployed based on an instance template&#x20;
* Manager ensures all instances are in a running state&#x20;
* Typically used with autoscaler load-balancer
* Regional managed instance groups are generally recommended over zonal instance groups&#x20;
* Dynamically add/remove instances based on changes in load
  * Define autoscaling policy

### HTTP load balancing&#x20;

* Global&#x20;
* Apps are available to customers at a single anycast IP address, simplifying DNS
* No pre-warming required&#x20;
* URL maps can be configured to route URLs to specific instances, though requests are generally routed to closest instance with capacity to serve

#### Architecture of HTTP load balancer&#x20;

| Term                   | Definition                                                                                                             | Notes                                                                                                                                   |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Global Forwarding Rule | Directs request from internet to target HTTP proxy                                                                     |                                                                                                                                         |
| Target Proxy           | Checks each request against url map to determine appropriate backend service for the request                           |                                                                                                                                         |
| URL Map                |                                                                                                                        |                                                                                                                                         |
| Backend Service        | Directs each request to appropriate backend depending on capacity, zone, and instance health of attached backends      | <ul><li>(Optional) session affinity</li><li>Timeout setting determines how long the backend server will wait before a timeout</li></ul> |
| Health Check           | Pulls instances configured to the backend services to determine which instances are healthy enough to service requests |                                                                                                                                         |
| Session affinity       | Attempts to send all requests from the same client to the same service.                                                | Overrides the default round-robin algorithm                                                                                             |
|                        |                                                                                                                        |                                                                                                                                         |

### HTTPS load balancing

Very similar to HTTP load balancer with a few differences&#x20;

* Target HTTPS proxy
* At least one signed SSL cert installed
* SSL session terminates _at_ load balancer&#x20;
* QUIC transport layer protocol&#x20;

#### SSL certificates&#x20;

* target proxy can be configured with up to 10 SSL certificates&#x20;

### SSL load balancing&#x20;

* Cloud-SSL proxy is intended for non-HTTPS traffic&#x20;

#### Defining SSL policy

* Specifies the min TLS version clients can connect with&#x20;
* Profile of SSL policy features (3 GCP managed/ pre-configured profiles)
  * Compatible -- allows broadest set of clients
  * Modern -- Wide set
  * Restricted -- Support reduced set of SSL/ TLS features intended to meet more strict compliance requirements&#x20;
* 4th, custom profile available&#x20;

## Cloud Armor

* Works with global HTTPS load balancing to provide built-in defenses against DDoS attacks&#x20;
* Restrict or allow access to load balancer at the edge of your network (as close to the user)&#x20;
* Security policies with deny and allow rules&#x20;
  * block by IP&#x20;
  * custom configure which HTTP error code is returned&#x20;

### Cloud Armor web-app firewall&#x20;

![](<../../.gitbook/assets/image (7).png>)

* Findings are automatically sent to Security Command Center (if enabled/ in use)&#x20;

### Network endpoint groups

* Specifies a group of backend endpoints or services&#x20;
* Used as backend for certain load balancers&#x20;
* Zonal, internet and serverless endpoint types&#x20;

![](<../../.gitbook/assets/image (11) (1).png>)

### Cloud CDN

* Content delivery network as a service using Google's globally distributed edge points of presence (PoP)
* Cache miss vs Cache hit&#x20;
* Certain information can be cached, but some cannot&#x20;
* Cloud CDN cache modes (3) control factors to determine if your content is cached or not.&#x20;

### SSL/TCP proxy load balancing&#x20;

#### SSL

* Global load balancing for encrypted, non-HTTP traffic&#x20;
* Terminates SSL sessions at load balancing layer
* Automatically routes traffic to closes region that has capacity&#x20;
* Only need to update customer facing certificate in one place&#x20;
* GCP automatically patches load balancers, reducing overhead of managing the security of the load balancers&#x20;

#### TCP

* Global load balancing for unencrypted, non-HTTP traffic&#x20;
* Terminates TCP sessions at load balancing layer
* Automatically routes traffic to closes region that has capacity&#x20;
* GCP automatically patches load balancers&#x20;

### Network load balancing&#x20;

* Regional, non-proxied load balancer&#x20;
* Forwarding rules balance loads on systems&#x20;
* UDP and certain TCP/SSL ports&#x20;
* Able to service instance group backends or target pool resource backends&#x20;

#### Target pool resource&#x20;

* Defines a group of instances that receives incoming traffic from forwarding rules&#x20;
* Must be in the same region&#x20;

### Internal load balancing&#x20;

* TCP/ UDP, regional load balancing service&#x20;
* Internal / private&#x20;
* Software-defined, fully distributed load balancing&#x20;
* Built on top of Andromeda, which is Google's network virtualization stack&#x20;

### Choosing a load balancer&#x20;

* HTTPS, SSL Proxy, TCP proxy services support IPv6

![](<../../.gitbook/assets/image (6).png>)

## Network pricing :moneybag:

* GCP pricing calculator&#x20;
  * Web-based tool  that you use to specify the expected consumption of certain services and resources, and then it provides you with an estimated cost&#x20;

![I believe this presentation was created in 2019](../../.gitbook/assets/image.png)

![I believe this presentation was created in 2019](<../../.gitbook/assets/image (3) (1) (1).png>)

## "Common" Network Designs&#x20;

### Availability&#x20;

* If availability is a high priority, you can place two VMs into multiple zones, but within the same subnet&#x20;
* Allocating VMs on a single subnet to separate zones gives improved availability without additional security complexity&#x20;

![](<../../.gitbook/assets/image (4) (1) (1).png>)

### Globalization :earth\_americas:

* place resources in different regions to create a higher degree of failure independence&#x20;
* design robust systems with resources spread across different failure domains&#x20;
* HTTP load balancer allows you to route traffic to the region that is closest to the user&#x20;

![](<../../.gitbook/assets/image (3) (1).png>)

### Security when designing networks&#x20;

* Only assign internal IP address to VM whenever possible&#x20;
  * The default setting for a VM instance is to have an ephemeral external IP address. This behavior can be changed with a policy constraint at the organization or project level.

#### Cloud NAT&#x20;

_GCP managed network address translation service is "Cloud NAT"_

* Cloud NAT allows you to provision app instances without public IP addresses while also allowing them to access the internet in a controlled and efficient manner&#x20;
* Outbound NAT vs. Inbound NAT
*   Hosts outside of VPC network cannot directly access any o the private instances behind the cloud NAT gateway&#x20;

    * Helps keep VPC networks isolated and secure&#x20;



![](<../../.gitbook/assets/image (2) (1) (1).png>)

#### Private Google Access

_Allows VMs that only have internal IP addresses to reach external IP addresses of Google APIs and services \*\*without going through the internet\*\*_

* Need to enable this if your private VM needs access to a cloud storage bucket&#x20;
* Enabled on a subnet-by-subnet basis

![](<../../.gitbook/assets/image (5) (1) (1).png>)

## Best Practices

## References&#x20;

* Cloudskillsboost - Essential Google Cloud Infrastructure: Foundation
* Cloudskillsboost - **** Networking in Google Cloud
* Cloudskillsboost - **** Security in Google Cloud
