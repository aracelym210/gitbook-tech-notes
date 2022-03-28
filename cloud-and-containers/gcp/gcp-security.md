# GCP Security

## Google's Approach to Security

* Operational Security&#x20;
* Internet Communication
* Storage Services
* User Identity
* Service Deployment&#x20;
* Hardware Infrastructure&#x20;

## VPC Security&#x20;

* Define resources on a logically isolated network&#x20;
* Firewall rules&#x20;

### Operational monitoring&#x20;

* GCP Stackdriver service enables debugging, monitoring and diagnostics for apps on GCP

### Compliance&#x20;

* GCP products regularly undergo verification of security privacy and compliance controls, and achieves certifications against global standards&#x20;

### Shared Security&#x20;

#### Data access&#x20;

* It is the responsibility of the customer to properly implement controls to restrict data access

#### Security Assessment/ Pen-testing&#x20;

* GCP does not require notification for penetration testing, but users must make sure they comply with Acceptable Use Policy (AUP)

## Threats & Mitigation

### Denial of Service (DoS)

* GCP HTTPS load balancing provides built-in defense&#x20;
* Central DoS mitigation service&#x20;

### Google Cloud Armor

* Web application firewall to protect against xss, SQL injection, and more.&#x20;
* Works in conjunction with Global HTTP/S load balancing&#x20;
* Based on same technologies and global infrastructure used to protect popular Google services

### Physical Security&#x20;

* Data centers protected with layered security model
* Limited access -- <1% Googlers have access to data center

### Data access

* All data at rest is chunked and automatically encrypted&#x20;

### Data in transit

* Different measures are applied depending on physical location&#x20;

### Server and software stack security&#x20;

* Trusted server boot w/ Google-made "Titan" chip&#x20;

### Data disposal

Data deleted from all Google systems as soon as reasonably possible, with a max period of 180 days&#x20;

## Access transparency&#x20;

### Data ownership

* Cloud platform customers own their data, not Google
* Google does not scan customer data for advertisements, nor is it sold to 3rd parties&#x20;
*

## References&#x20;

* Cloudskillsboost - **** Security in Google Cloud
* [GCP IAM Docs](https://cloud.google.com/iam/docs/overview)
