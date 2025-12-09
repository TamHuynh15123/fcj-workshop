---
title: "Week 8 Worklog"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Set up notification services (SNS and SES) for Coffee Cloud
* Implement email notifications for orders and promotions
* Add push notifications for order status updates

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Learn AWS SNS (Simple Notification Service) basics <br> - Understand topics, subscriptions, and message formats <br> - Create SNS topic for order notifications                                   | 19/08/2025 | 19/08/2025      | SNS documentation                         |
| 2   | - Set up AWS SES (Simple Email Service) <br> - Verify email domain/address <br> - Create email templates for order confirmations                                                                     | 20/08/2025 | 20/08/2025      | SES documentation                         |
| 3   | - Integrate SNS with Lambda functions <br> - Send notifications when orders are created/updated <br> - Test notification delivery                                                                    | 21/08/2025 | 21/08/2025      | Lambda + SNS integration                  |
| 4   | - Implement email notifications with SES <br> - Send order confirmation emails <br> - Create promotional email templates                                                                             | 22/08/2025 | 22/08/2025      | SES email templates                       |
| 5   | - Test complete notification flow <br> - Verify email delivery and formatting <br> - Test SMS notifications (optional)                                                                              | 23/08/2025 | 23/08/2025      | End-to-end notification testing           |


### Week 8 Achievements:

* Successfully configured AWS SNS for Coffee Cloud notifications:
  * Created SNS topics for different notification types (orders, promotions, alerts)
  * Set up email subscriptions for admin notifications
  * Configured topic policies for secure access from Lambda functions

* Implemented AWS SES for email communications:
  * Verified sender email address for development
  * Created professional email templates for:
    - Order confirmation emails
    - Welcome emails for new users
    - Promotional newsletters
    - Password reset emails

* Integrated notification services with Lambda functions:
  * Order creation triggers automatic email confirmation
  * Order status updates send real-time notifications
  * Admin receives alerts for new orders and system issues

* Enhanced Coffee Cloud user experience:
  * Customers receive immediate order confirmations
  * Real-time updates on order preparation and delivery status
  * Professional-looking email templates with Coffee Cloud branding

* Tested notification reliability:
  * Email delivery working within SES sandbox limits
  * Proper error handling for failed notifications
  * Monitoring notification logs via CloudWatch

* Learned AWS communication services best practices:
  * Understanding SES sandbox vs production mode
  * SNS pricing and message limits
  * Proper IAM permissions for notification services

* Implemented a NAT gateway pattern to allow private instances to access the internet for updates.

* Documented VPC diagrams, CIDR choices, and common troubleshooting commands (e.g., traceroute, curl, iptables checks).

* Next steps: explore managed database services and backups.
