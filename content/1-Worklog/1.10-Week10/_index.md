---
title: "Week 10 Worklog"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 10 Objectives:

* Learn monitoring and auditing with CloudWatch and CloudTrail.
* Understand IAM roles for services and create least-privilege policies for automation.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Read CloudWatch fundamentals and CloudTrail overview; plan which resources to monitor.                                                                                                              | 10/11/2025 | 10/11/2025      | CloudWatch & CloudTrail docs               |
| 3   | - Install and configure the CloudWatch Agent on EC2; collect system and application metrics (CPU, memory, disk).                                                                                      | 11/11/2025 | 11/11/2025      | CloudWatch agent guide                     |
| 4   | - Create CloudWatch dashboards with widgets for EC2 and RDS metrics; add custom metric graphs for application counters.                                                                                | 12/11/2025 | 12/11/2025      | CloudWatch dashboards docs                 |
| 5   | - Define CloudWatch alarms (CPU, memory via agent, disk) and create an SNS topic for notifications; test alarm triggering.                                                                             | 13/11/2025 | 13/11/2025      | CloudWatch Alarms & SNS docs               |
| 6   | - Enable CloudTrail for the account, configure trail to S3, validate events for console and API activity; review logs and identify suspicious events (if any).                                        | 14/11/2025 | 14/11/2025      | CloudTrail docs                            |


### Week 10 Achievements:

* Set up CloudWatch metrics and dashboards to monitor EC2, RDS, and custom application metrics.

* Defined CloudWatch Alarms for CPU, memory (via agent), and disk usage and configured SNS notifications.

* Enabled CloudTrail in the account to capture API activity and validated logs in an S3 bucket.

* Created IAM roles for EC2 instances and a role for automated deployment tasks with scoped permissions.

* Wrote and tested a basic policy for an S3 read-only role and iterated on permissions to follow least-privilege.

* Next steps: explore Infrastructure-as-Code to codify these resources.
