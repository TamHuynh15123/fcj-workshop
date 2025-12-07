---
title: "Week 9 Worklog"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Explore AWS database services (RDS, Aurora, DynamoDB) and data backup strategies.
* Practice deploying a managed database and connecting it securely from application hosts.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Study AWS managed database options and when to use RDS vs DynamoDB; read RDS best practices.                                                                                                        | 03/11/2025 | 03/11/2025      | RDS docs, DynamoDB docs                    |
| 3   | - Create an RDS subnet group and parameter group; launch an RDS (MySQL) instance in private subnet with Multi-AZ disabled for cost reasons.                                                         | 04/11/2025 | 04/11/2025      | RDS launch guide                           |
| 4   | - Configure security group rules to allow DB traffic only from application EC2; connect from bastion/EC2 to test DB connection and run simple queries.                                               | 05/11/2025 | 05/11/2025      | RDS connection docs                        |
| 5   | - Explore DynamoDB: create a sample table, experiment with read/write capacity (on-demand vs provisioned), and run basic CRUD via CLI.                                                              | 06/11/2025 | 06/11/2025      | DynamoDB docs                              |
| 6   | - Configure automated snapshots for RDS, test a snapshot restore to a new instance; document retention strategy and cross-region copy options.                                                     | 07/11/2025 | 07/11/2025      | Backup & snapshot docs                     |


### Week 9 Achievements:

* Deployed an Amazon RDS (MySQL) instance in a private subnet and confirmed secure connection from an application EC2 instance.

* Experimented with DynamoDB for a simple key-value use-case and compared provisioning vs. on-demand modes.

* Configured automated snapshots and tested a point-in-time recovery process for RDS.

* Reviewed backup retention and cross-region copy options; documented cost/benefit trade-offs.

* Next steps: monitoring and logging (CloudWatch & CloudTrail) and implementing alerting.
