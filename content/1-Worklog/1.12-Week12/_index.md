---
title: "Week 12 Worklog"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 12 Objectives:

* Deliver the final mini-project: integrate core services into a small, documented architecture.
* Perform cleanup, document learned skills, and reflect on improvements and next learning steps.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Finalize mini-project architecture and create a deployment checklist; draw architecture diagram and list IaC responsibilities.                                                                      | 24/11/2025 | 24/11/2025      | Project notes                              |
| 3   | - Implement IaC templates (Terraform or CloudFormation) for final stack components: VPC, subnets, EC2, RDS, S3; parameterize inputs for reuse.                                                       | 25/11/2025 | 25/11/2025      | IaC templates                              |
| 4   | - Deploy the final stack in a test account/environment; run smoke tests for application connectivity and data flow.                                                                                    | 26/11/2025 | 26/11/2025      | Deployment logs                             |
| 5   | - Add monitoring and alarms for core components; prepare README with deployment and rollback steps; seed database with sample data if needed.                                                           | 27/11/2025 | 27/11/2025      | README, CloudWatch config                   |
| 6   | - Cleanup temporary resources (test buckets, instances, temporary IAM keys); finalize deliverables: IaC templates, architecture diagram, and demo notes.                                              | 28/11/2025 | 28/11/2025      | Project deliverables                        |


### Week 12 Achievements:

* Completed a final mini-project that combined S3 (static content), an EC2 application host, and an RDS database behind a private subnet.

* Automated deployment steps with Terraform/CloudFormation scripts and included a README with usage instructions.

* Performed resource cleanup: deleted test buckets/instances, revoked temporary IAM keys, and removed unused snapshots.

* Prepared a short reflection on lessons learned, challenges faced, and next steps (e.g., containerization, CI/CD, security hardening).

* Final deliverables: IaC templates, architecture diagram, and a short demo recording (links saved to project notes).
