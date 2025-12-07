---
title: "Week 7 Worklog"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Learn AWS Identity and Access Management (IAM) fundamentals.
* Explore S3: buckets, versioning, lifecycle rules, and using S3 for static website hosting.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Review IAM concepts and best practices; read AWS IAM guide; identify required roles for upcoming labs.                                                                                              | 20/10/2025 | 20/10/2025      | AWS IAM docs                               |
| 3   | - Create IAM groups and users; attach AWS managed policies; create a policy for least-privilege CLI usage and test with aws iam simulate-principal-policy.                                            | 21/10/2025 | 21/10/2025      | IAM policy docs                             |
| 4   | - Create an IAM role for EC2 (assume-role) for limited S3 access; attach role to an instance profile for later testing.                                                                                | 22/10/2025 | 22/10/2025      | IAM roles docs                              |
| 5   | - S3: create bucket with encryption (SSE-S3), enable public access block; practice put/get object via CLI and console.                                                                                 | 23/10/2025 | 23/10/2025      | S3 docs                                     |
| 6   | - Enable S3 versioning and lifecycle rule; deploy a static site to S3 and verify hosting and bucket policy; document steps and troubleshooting notes.                                                 | 24/10/2025 | 24/10/2025      | S3 static hosting guide                     |


### Week 7 Achievements:

* Studied IAM concepts: users, groups, roles, policies, and best practices for least privilege.

* Created IAM users and groups, attached managed policies, and generated access keys for CLI use.

* Practiced S3 operations: created buckets, uploaded objects, enabled versioning, and added a lifecycle rule to transition objects to STANDARD_IA.

* Deployed a simple static website to an S3 bucket and verified public access settings and bucket policy.

* Documented IAM and S3 commands and common troubleshooting steps for permissions and public access.

* Next steps: study VPC fundamentals and network security groups.
