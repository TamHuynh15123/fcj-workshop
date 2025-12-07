---
title: "Week 6 Worklog"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Onboard with the First Cloud Journey team and understand internship expectations.
* Learn AWS fundamentals: core service categories, account setup, Console and AWS CLI usage.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Onboarding meeting with mentor and team; read internship rules; set communication channels (Slack/Email).                                                                                             | 13/10/2025 | 13/10/2025      | internal docs                              |
| 3   | - Study AWS service categories (Compute, Storage, Networking, Database). Take notes and map services to use-cases; review CloudJourney modules.                                                           | 14/10/2025 | 14/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create AWS Free Tier account; enable MFA on root; create an IAM admin user; install & configure AWS CLI; verify aws sts get-caller-identity.                                                          | 15/10/2025 | 15/10/2025      | AWS Console, AWS CLI docs                  |
| 5   | - Learn EC2 components: AMIs, instance types, EBS, key pairs, security groups. Prepare key-pair and security-group rules for SSH (port 22).                                                           | 16/10/2025 | 16/10/2025      | EC2 docs                                   |
| 6   | - Launch a t2.micro EC2 instance (Amazon Linux/Ubuntu), connect via SSH, attach an additional EBS volume, format & mount it; create snapshot for practice.                                            | 17/10/2025 | 17/10/2025      | EC2/EBS docs                               |


### Week 6 Achievements:

* Gained a clear understanding of AWS core service groups and their use-cases:
  * Compute (EC2, Lambda)
  * Storage (S3, EBS)
  * Networking (VPC, Subnet, Route)
  * Database (RDS, DynamoDB)

* Created and secured an AWS Free Tier account, including enabling MFA and creating an initial IAM user.

* Navigated the AWS Management Console and located core services.

* Installed and configured the AWS CLI (access key, secret key, default region, output format).

* Performed basic CLI operations:
  * aws sts get-caller-identity
  * aws ec2 describe-instances
  * aws s3 ls

* Launched an EC2 instance, connected via SSH, and attached an EBS volume for practice.

* Next steps: practice with S3 and IAM, and save CLI snippets for repeatable tasks.
