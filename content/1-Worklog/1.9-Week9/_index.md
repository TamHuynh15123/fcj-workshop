---
title: "Week 9 Worklog"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Optimize Coffee Cloud application performance and security
* Set up monitoring and logging for the application
* Prepare for production deployment

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Optimize DynamoDB tables for better performance <br> - Set up proper indexes for common queries <br> - Review and optimize Lambda function performance                                              | 26/08/2025 | 26/08/2025      | DynamoDB optimization guide               |
| 2   | - Set up CloudWatch monitoring for all services <br> - Create custom metrics for business KPIs <br> - Configure log groups for Lambda functions                                                      | 27/08/2025 | 27/08/2025      | CloudWatch documentation                  |
| 3   | - Implement proper IAM roles and policies <br> - Follow least privilege principle <br> - Remove unnecessary permissions                                                                               | 28/08/2025 | 28/08/2025      | IAM best practices                        |
| 4   | - Set up CloudWatch dashboards <br> - Monitor application health and performance <br> - Create alarms for critical metrics                                                                          | 29/08/2025 | 29/08/2025      | CloudWatch dashboards                     |
| 5   | - Conduct thorough testing of all features <br> - Test error scenarios and edge cases <br> - Document known issues and limitations                                                                  | 30/08/2025 | 30/08/2025      | Application testing guide                 |


### Week 9 Achievements:

* Optimized Coffee Cloud application performance:
  * **DynamoDB Optimization**: Added Global Secondary Indexes (GSI) for efficient queries by user ID and order status
  * **Lambda Performance**: Optimized function code and reduced cold start times
  * **Caching Strategy**: Implemented basic caching for frequently accessed product data

* Set up comprehensive monitoring and logging:
  * **CloudWatch Metrics**: Custom metrics for orders per hour, user registrations, and error rates
  * **Log Analysis**: Centralized logging for all Lambda functions with structured log format
  * **Performance Monitoring**: Track API response times and database query performance

* Enhanced security posture:
  * **IAM Optimization**: Created specific roles for each service with minimal required permissions
  * **Security Review**: Removed overly permissive policies and hardened access controls
  * **Secrets Management**: Moved sensitive configuration to environment variables

* Created operational dashboards:
  * **Business Metrics Dashboard**: Real-time view of orders, revenue, and user activity
  * **Technical Health Dashboard**: System performance, error rates, and service availability
  * **Cost Monitoring Dashboard**: Track AWS resource usage and costs

* Completed comprehensive testing:
  * **Functional Testing**: Verified all user flows work correctly
  * **Error Handling**: Tested system behavior under various failure scenarios
  * **Load Testing**: Basic testing of system performance under simulated load
  * **Security Testing**: Verified authentication and authorization work properly

* Documented application architecture and deployment process for future maintenance

* Reviewed backup retention and cross-region copy options; documented cost/benefit trade-offs.

* Next steps: monitoring and logging (CloudWatch & CloudTrail) and implementing alerting.
