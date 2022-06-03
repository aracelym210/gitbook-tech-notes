---
description: >-
  Notes on Cloud Identity and Access Management -- WHO can do WHAT on which
  RESOURCE
---

# Cloud IAM

## Fundamentals&#x20;

### IAM Objects

* Organization
* Folders
* Projects
* Resources
* Roles
* Members

### IAM Resource Manager&#x20;

* Resources in GCP are managed hierarchically&#x20;
* Policies can be set at each level - resource, projects, folders, organization
  * Policy contains a set of _roles_ and _members_

| Hierarchical Objects | Definition                                                                                                    | Inheritance Notes                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Organization         | <p>Represents your company. </p><p></p>                                                                       | IAM roles granted at this level are inherited by all resources under the org                                                                                                                                                   |
| Folders              | <p>Optional method of further organizing resources and projects.</p><p></p>                                   | IAM roles granted at this level are inherited by all resources contained within that folder                                                                                                                                    |
| Projects             | Represent a trust boundary within the company. Services within the same project have a default level of trust | If the resource hierarchy is changes, the policies applies to the project will also change. (i.e. if you move a project under a different organization, the IAM policies applied will change to that of the new organization.  |
| Resources            |                                                                                                               |                                                                                                                                                                                                                                |
| Members              |                                                                                                               |                                                                                                                                                                                                                                |
| Roles                |                                                                                                               |                                                                                                                                                                                                                                |



![](<../../.gitbook/assets/Screen Shot 2022-03-24 at 10.53.28 AM.png>)

{% hint style="warning" %}
<mark style="color:orange;">**Child policies cannot restrict access granted by a parent.**</mark>** ** For example, if editor role was granted to folder Dept. X, and viewer role is granted for the Bookshelf project, the policy applied by the parent of Dept. X will trump the policy set for the Bookshelf project. In other words -- you will still be able to edit the Bookshelf project.&#x20;
{% endhint %}

{% hint style="success" %}
<mark style="color:green;">**Best practice:**</mark> Follow the principle of least privilege which applies to identities, roles and resources.
{% endhint %}

### IAM Members (WHO)

#### Five types of members&#x20;

| Member Type            | Definition                                                                                 | Notes                                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| Google accounts        | Any person who interacts with GCP                                                          | Any email address that is associated with a google account can be an identity. This includes gmail.com or other domains |
| Service accounts       | Account that belongs to an application, not individual user                                | Two types of service accounts -- Google-managed and user-managed                                                        |
| Google groups          | Named collection of Google accounts and service accounts                                   | Convenient way to apply access controls to whole groups of users or service accounts                                    |
| Gsuite domains         | Virtual group of all Google accounts have been created  in an organization's gsuite domain |                                                                                                                         |
| Cloud identity domains | Represents a virtual group of all google accounts in an organization                       | Cloud identity domain users do not have access to g suite applications and features                                     |

#### Service accounts&#x20;

![](<../../.gitbook/assets/image (12) (1).png>)

### IAM Roles (WHAT)

#### Three kinds of roles&#x20;

| Role              | Definition                                            | Notes                                                                                                                                                                                                                                                 |
| ----------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Basic roles       | Original roles available in cloud console             | <ul><li>Owner - full admin access </li><li>Editor - modify and delete access </li><li>Viewer - Read-only access</li><li>Billing admin - manage billing &#x26; +/- admins</li><li>A project can have more than one of the roles defined here</li></ul> |
| Pre-defined roles | Roles that are made up of collections of permissions  | <ul><li>Permissions are classes and methods in APIs</li><li>Users can have multiple roles </li></ul><p><code>service.resource.verb</code></p>                                                                                                         |
| Custom roles      | Self-explanatory                                      | Best way to enforce least-privilege                                                                                                                                                                                                                   |

#### Network-related IAM roles

![There are other network-related roles than those listed here](<../../.gitbook/assets/image (6) (1).png>)

### IAM Policies

* Specifies access control policies for cloud resources&#x20;
* A policy consists of a list of bindgins, which binds a list of members to a role
* A policy is a collection of access statements attached to a resource&#x20;
* Each policy contains a&#x20;
  * set of roles
  * role members

#### Organization Policy&#x20;

_An organization policy let's admins set restrictions on specific resources to determine how they can be configured_ &#x20;

| Term                                | Definition                                                                                                  | Notes                                                                                             |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Organization Policy                 | A configuration of restrictions                                                                             |                                                                                                   |
| Organization Policy _Administrator_ | Configures constraints across entire resource hierarchy. An org policy admin defines the org policy         |                                                                                                   |
| Organization Policy _Service_       | Gives centralized and programmatic control over your org's cloud resources                                  |                                                                                                   |
| Constraint                          | Particular type of restriction against one or more of GCP service. It defines what behaviors are controlled | <p>Examples include:<br>- Disable VM serial port access<br>- Disable service account creation</p> |

![](<../../.gitbook/assets/Screen Shot 2022-03-24 at 1.48.08 PM.png>)

### Firewall Rules&#x20;

* Protect VM instances from unapproved connections&#x20;

{% hint style="success" %}
Filtering by service accounts is considered more secure than filtering by tags
{% endhint %}

![](<../../.gitbook/assets/Screen Shot 2022-03-24 at 2.03.53 PM.png>)

## IAM Labels&#x20;

### Label use cases&#x20;

* Team or cost center labels (budgeting purposes)
* Component labels (front end, dashboard, etc.)
* Environment or stage labels (Production, Test, etc.)&#x20;
* State labels (i.e. Active or Archive)&#x20;
* Virtual machine labels (distinguish VMs that are identical)&#x20;

## IAM Recommender

* Helps enforce principle of least privilege by ensuring members have only the permissions that they actually need.&#x20;
* Recommender will suggest that you revoke an existing role when it has been in effect for 90 days or more and when it has not been used within the past 90 days&#x20;

## IAM Troubleshooter

* Policy troubleshooter helps to more closely examine policies that govern user access to a particular resource&#x20;
* To generate a report, need the email address of the user who needs access and the full name of the resource they need access to, and the permission you want to check against&#x20;
* iam.securityReviewer role is needed for maximum effectiveness of the report&#x20;
* Access Policy Troubleshooter by:
  * console
  * gcloud CLI
  * Policy Troubleshooter API

## IAM Audit Logs

* Cloud audit logs maintain three logs for each project, folder, and organization
  * Admin activity&#x20;
  * Data access
  * System events

### Admin activity audit logs&#x20;

* Logs when administrative actions modify configs or metadata&#x20;
* Logs are always written and cannot be disabled&#x20;
* Must have IAM role Logging/ Logs viewer or project/ viewer&#x20;

### Data access audit logs

* Records changes to private cloud resources&#x20;
* Does not record changes to publicly shared assets (i.e. PDF file in a publicly available storage bucket)&#x20;
* Not enabled by default&#x20;

### System event audit logs&#x20;

* Driven by Google Systems&#x20;
* Always written and cannot be disabled&#x20;

## IAM Best Practices :white\_check\_mark:

* Principle of least privilege&#x20;
  * Check when implementing parent policies, that you do not inadvertently grant more access to a child resource that you intended&#x20;
* Assign roles to groups instead of individual users&#x20;
* Try to use predefined roles that are managed by Google because they offer less overhead&#x20;
* Export Audit logs to Google Cloud Storage or to Big Query&#x20;



## References&#x20;

* Cloudskillsboost - **** Networking in Google Cloud
* Cloudskillsboost - **** Security in Google Cloud
* [GCP IAM Docs](https://cloud.google.com/iam/docs/overview)
