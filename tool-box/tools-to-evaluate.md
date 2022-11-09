---
description: >-
  A list of tools that I want to test out. Each tested tool will have it's own
  page.
---

# Tools to evaluate

## AWS

### IAM Evaluation

* [ ] [Cloudsplaining](https://github.com/salesforce/cloudsplaining/) - Cloudsplaining identifies violations of least privilege in AWS IAM policies and generates a pretty HTML report with a triage worksheet. It can scan all the policies in your AWS account or it can scan a single policy file. Cloudsplaining also identifies IAM Roles that can be assumed by AWS Compute Services (such as EC2, ECS, EKS, or Lambda), as they can present greater risk than user-defined roles - especially if the AWS Compute service is on an instance that is directly or indirectly exposed to the internet.
* [ ] [CloudMapper](https://github.com/duo-labs/cloudmapper) - Parts of this tool are no longer maintained. CloudMapper helps you analyze your Amazon Web Services (AWS) environments. The original purpose was to generate network diagrams and display them in your browser (functionality no longer maintained).
* [ ] IamVulnerable - IAMVulnerable uses the Terraform binary and your AWS credentials to deploy over 250 IAM resources into your selected AWS account. Within minutes, you can start learning how to identify and exploit vulnerable IAM configurations that allow for privilege escalation.
* [ ] [Pmapper](https://github.com/nccgroup/PMapper) - Principal Mapper, also known as PMapper, is a script and library for identifying risks in the configuration of AWS Identity and Access Management (IAM) for an AWS account or an AWS organization. It models the different IAM Users and Roles in an account as a directed graph, which enables checks for privilege escalation and for alternate paths an attacker could take to gain access to a resource or action in AWS.

#### Pentesting tools

* [ ] [awspx](https://github.com/WithSecureLabs/awspx) - awspx is a A graph-based tool for visualizing effective access and resource relationships in AWS environments.
* [ ] Pacu

#### Vulnerable by design

* [ ] [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat/) - CloudGoat is Rhino Security Labs' "Vulnerable by Design" AWS deployment tool. It allows you to hone your cloud cybersecurity skills by creating and completing several "capture-the-flag" style scenarios.
* [ ] [Sadcloud](https://github.com/nccgroup/sadcloud) - Sadcloud is a tool for standing up (and tearing down!) purposefully insecure cloud infrastructure.

### Blue Team Tools

* [GitHub - chainguard-dev/osquery-defense-kit](https://github.com/chainguard-dev/osquery-defense-kit) - Production-ready detection & response queries for osquery

### GCP

#### IAM Evaluation

* [ ] [GCP Scanner](https://github.com/google/gcp\_scanner)- GCP Scanner is a GCP resource scanner that can help determine what level of access certain credentials posses on GCP. The scanner is designed to help security engineers with evaluating impact of a certain VM/container compromise, GCP service account or OAuth2 token key leak.

#### Vulnerable by design

* [ ] GCP Goat -&#x20;

### Multi-cloud

* [ ] CloudSploit - CloudSploit is a cloud scanner to detect security risks in cloud infrastructure accounts. AWS, GCP, Azure, GitHub
* [ ] [ScoutSuite](https://github.com/nccgroup/ScoutSuite) - ScoutSuite is an open source multi-cloud security-auditing tool, which enables security posture assessment of cloud environments. Using the APIs exposed by cloud providers, Scout Suite gathers configuration data for manual inspection and highlights risk areas.

### Terraform

* [x] [infracost.io](https://www.infracost.io/docs/) - Tool to run inside repository/ directory to estimate cloud infrastructure cost of Terraform template
* [x] [TerraGoat](https://github.com/bridgecrewio/terragoat) - TerraGoat is a learning and training project that demonstrates how common configuration errors can find their way into production cloud environments. AWS, GCP, Azu
