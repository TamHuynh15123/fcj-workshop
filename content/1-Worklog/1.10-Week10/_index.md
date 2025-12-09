---
title: "Week 10 Worklog"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Finalize Coffee Cloud application and prepare for demo
* Conduct final testing and bug fixes
* Create documentation and presentation materials

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Conduct final end-to-end testing of Coffee Cloud <br> - Fix any remaining bugs or issues <br> - Verify all features work as expected                                                              | 02/09/2025 | 02/09/2025      | Testing checklist                         |
| 2   | - Optimize application for demo presentation <br> - Prepare sample data and test scenarios <br> - Ensure stable performance during demo                                                            | 03/09/2025 | 03/09/2025      | Demo preparation guide                    |
| 3   | - Create comprehensive documentation: <br>&emsp; + Architecture diagrams <br>&emsp; + User guides <br>&emsp; + Technical documentation                                                              | 04/09/2025 | 04/09/2025      | Documentation templates                   |
| 4   | - Prepare presentation materials <br> - Create demo script and walkthrough <br> - Practice presentation delivery                                                                                     | 05/09/2025 | 05/09/2025      | Presentation guidelines                    |
| 5   | - Final review and cleanup <br> - Verify all AWS resources are properly configured <br> - Prepare for project handover and demo                                                                    | 06/09/2025 | 06/09/2025      | Project review checklist                  |


### Week 10 Achievements:

* Successfully completed Coffee Cloud application development:
  * **Full-stack Application**: React frontend hosted on Amplify with Lambda backend
  * **Database Integration**: DynamoDB storing users, products, orders, and points data
  * **Authentication System**: Cognito-powered user management with role-based access
  * **Notification System**: Email confirmations via SES and real-time updates via SNS

* Conducted comprehensive final testing:
  * **User Journey Testing**: Complete flow from registration to order completion
  * **Cross-browser Testing**: Verified compatibility across different browsers and devices
  * **Performance Testing**: Confirmed acceptable response times under normal load
  * **Security Testing**: Verified proper authentication and data protection

* Created complete project documentation:
  * **Architecture Documentation**: Detailed system design and AWS services integration
  * **User Manual**: Step-by-step guides for customers, shippers, and administrators
  * **Technical Documentation**: API specifications, database schema, and deployment guides
  * **Cost Analysis**: Detailed breakdown of AWS costs and Free Tier usage

* Prepared professional demo presentation:
  * **Demo Script**: Structured walkthrough of key features and capabilities
  * **Sample Data**: Realistic test data showcasing system functionality
  * **Presentation Materials**: Professional slides explaining technical architecture

* Project ready for production deployment:
  * All critical features implemented and tested
  * Documentation complete for future maintenance
  * System optimized for AWS Free Tier usage
  * Monitoring and alerting configured for operational oversight

* Key learning outcomes achieved:
  * Hands-on experience with serverless architecture
  * Understanding of AWS cost optimization strategies
  * Knowledge of full-stack application deployment on AWS

* Created IAM roles for EC2 instances and a role for automated deployment tasks with scoped permissions.

* Wrote and tested a basic policy for an S3 read-only role and iterated on permissions to follow least-privilege.

* Next steps: explore Infrastructure-as-Code to codify these resources.
