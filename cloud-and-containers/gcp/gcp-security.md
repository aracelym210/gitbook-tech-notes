# 🔒 GCP Security

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

## Cloud Identity

* Google Cloud Identity is an Identity as a Service Solution&#x20;
* Manage users, groups, domain-wide security settings&#x20;
* Tied to a unique DNS domain&#x20;
* Do not need to use GSuite services, but can be combined with existing GSuite subscriptions
* Free and premium edition&#x20;
* Each cloud identity account is associated with _one_ organization&#x20;

### GCP Directory Sync (GCDS)&#x20;

#### Syncing with MS Active Directory&#x20;

* GCP Directory Sync (GCDS) can syncronize GSuite accounts to match data in existing Active Directory or LDAP
* One way synchronization. AD/ LDAP is updated and GCDS periodically syncs with AD.

#### Managed Microsoft AD&#x20;

* Runs actual Microsoft AD controllers&#x20;

## GCP Authentication&#x20;

* two primary ways to handle google user authentication: Google authentication and SSO
* Google Auth -- Google password stored within Google's infrastructure&#x20;
* SAML is supported for SSO
  * Google operates as a service provider and SSO system operates as an identity provider&#x20;

## Managing GCP permissions

* Use groups to help manage permissions!&#x20;
* High risk areas may want to assign individual permissions directly instead of groups&#x20;
* General principle is to add no more than 3 admins to the Organization&#x20;

## References&#x20;

* Cloudskillsboost - **** Security in Google Cloud
* [GCP IAM Docs](https://cloud.google.com/iam/docs/overview)
