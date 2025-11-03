---
title: "Week 11 Worklog"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 11 Objectives:

* Learn Infrastructure as Code (IaC) basics and practice with CloudFormation and Terraform.
* Automate the creation of a small, repeatable stack that includes networking, compute, and storage.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Read CloudFormation basics and review example templates; identify resources to include in a simple stack (VPC + EC2).                                                                               | 17/11/2025 | 17/11/2025      | CloudFormation docs                        |
| 3   | - Author a CloudFormation template to create a VPC, public subnet and an EC2 instance; validate the template with cfn-lint or the console.                                                           | 18/11/2025 | 18/11/2025      | CFN template examples                      |
| 4   | - Install Terraform locally; write initial Terraform configuration (provider, VPC, EC2) and plan the deployment; compare with CloudFormation approach.                                               | 19/11/2025 | 19/11/2025      | Terraform docs                             |
| 5   | - Modularize Terraform: create a small module for EC2 (variables for AMI, instance type, security group) and use tfstate to track resources.                                                        | 20/11/2025 | 20/11/2025      | Terraform modules guide                    |
| 6   | - Test stack teardown for both CloudFormation and Terraform; ensure orphan resources (EBS volumes, Elastic IPs) are removed; document differences in workflow.                                       | 21/11/2025 | 21/11/2025      | IaC teardown best practices                |


### Week 11 Achievements:

* Learned CloudFormation basics and authored a template to create a VPC, public subnet, and an EC2 instance.

* Installed Terraform and used it to provision the same small stack, comparing workflow differences and state handling.

* Implemented parameterization and small modules to make IaC reusable and documented the deployment steps.

* Verified proper teardown by destroying stacks and ensuring resources (EBS volumes, elastic IPs) were cleaned up.

* Next steps: apply IaC to the final mini-project and prepare a short demo of automated deployment.
