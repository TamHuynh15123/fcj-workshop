---
title: "Week 8 Worklog"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Learn AWS networking: VPC, subnets, routing, Internet Gateway, NAT, Security Groups and NACLs.
* Deploy networked resources and practice secure connectivity patterns.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Design VPC CIDR and subnet plan (public/private); document CIDR choices and rationale.                                                                                                                | 27/10/2025 | 27/10/2025      | VPC docs                                    |
| 3   | - Create VPC with public and private subnets; configure route tables and attach an Internet Gateway for public subnet.                                                                                 | 28/10/2025 | 28/10/2025      | VPC guide                                   |
| 4   | - Create private subnet components and a NAT Gateway (or NAT instance); test outbound connectivity from private instances.                                                                               | 29/10/2025 | 29/10/2025      | NAT docs                                    |
| 5   | - Design and apply Security Groups and Network ACLs; create rules to allow only necessary traffic (SSH via bastion, HTTP/HTTPS, DB ports).                                                              | 30/10/2025 | 30/10/2025      | Security groups docs                        |
| 6   | - Deploy a bastion host in the public subnet; test SSH proxy to private EC2; capture a simple network diagram and troubleshooting notes.                                                               | 31/10/2025 | 31/10/2025      | VPC/SSH best practices                      |


### Week 8 Achievements:

* Designed and created a VPC with public and private subnets, configured route tables and an Internet Gateway.

* Launched EC2 instances in public and private subnets and tested connectivity through a bastion/SSH proxy.

* Configured Security Groups and Network ACLs to restrict traffic according to least-privilege principles.

* Implemented a NAT gateway pattern to allow private instances to access the internet for updates.

* Documented VPC diagrams, CIDR choices, and common troubleshooting commands (e.g., traceroute, curl, iptables checks).

* Next steps: explore managed database services and backups.
