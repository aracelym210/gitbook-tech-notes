---
description: Notes on Google Virtual Private Cloud
---

# GCP VPC

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

![](<../../.gitbook/assets/image (3) (1) (1).png>)

## DNS&#x20;

### Resolution for internal addresses&#x20;

* Each instance has a hostname that can be resolved to an internal IP address
  * Hostname is same as instance name&#x20;
* Name resolution handled by internal dns resolver
  * Provided as part of Compute Engine (169.254.169.254)
  * routes other queries to Google's public DNS servers for public name resolution
* Instance is not aware of external IP address assigned to it&#x20;
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

![](<../../.gitbook/assets/image (4) (1).png>)

## Network pricing

* GCP pricing calculator&#x20;
  * Web-based tool  that you use to specify the expected consumption of certain services and resources, and then it provides you with an estimated cost&#x20;

![I believe this presentation was created in 2019](../../.gitbook/assets/image.png)

![I believe this presentation was created in 2019](<../../.gitbook/assets/image (3) (1).png>)

## "Common" Network Designs&#x20;

### Availability&#x20;

* If availability is a high priority, you can place two VMs into multiple zones, but within the same subnet&#x20;
* Allocating VMs on a single subnet to separate zones gives improved availability without additional security complexity&#x20;

![](<../../.gitbook/assets/image (4).png>)

### Globalization

* place resources in different regions to create a higher degree of failure independence&#x20;
* design robust systems with resources spread across different failure domains&#x20;
* HTTP load balancer allows you to route traffic to the region that is closest to the user&#x20;

![](<../../.gitbook/assets/image (3).png>)

### Security when designing networks&#x20;

* Only assign internal IP address to VM whenever possible&#x20;

#### Cloud NAT&#x20;

_GCP managed network address translation service is "Cloud NAT"_

* Cloud NAT allows you to provision app instances without public IP addresses while also allowing them to access the internet in a controlled and efficient manner&#x20;
* Outbound NAT vs. Inbound NAT
*   Hosts outside of VPC network cannot directly access any o the private instances behind the cloud NAT gateway&#x20;

    * Helps keep VPC networks isolated and secure&#x20;



![](<../../.gitbook/assets/image (2).png>)

#### Private Google Access

_Allows VMs that only have internal IP addresses to reach external IP addresses of Google APIs and services \*\*without going through the internet\*\*_

* Need to enable this if your private VM needs access to a cloud storage bucket&#x20;
* Enabled on a subnet-by-subnet basis

![](<../../.gitbook/assets/image (5).png>)

## References&#x20;

* Cloudskillsboost - Essential Google Cloud Infrastructure: Foundation
