---
title: "Week 6 Worklog"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Set up AWS Amplify for Coffee Cloud frontend hosting
* Create React.js frontend application
* Configure CI/CD pipeline for automatic deployment

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Learn AWS Amplify fundamentals <br> - Understand Amplify hosting and CI/CD features <br> - Review React.js basics for frontend development                                                        | 05/08/2025 | 05/08/2025      | Amplify documentation                     |
| 2   | - Create new React.js application for Coffee Cloud <br> - Set up project structure with components for: login, menu, cart, orders                                                                   | 06/08/2025 | 06/08/2025      | React.js documentation                    |
| 3   | - Initialize Git repository for the project <br> - Push initial code to GitHub repository <br> - Set up basic routing and navigation                                                                | 07/08/2025 | 07/08/2025      | Git documentation                         |
| 4   | - Connect React app to AWS Amplify <br> - Configure automatic deployment from GitHub <br> - Set up custom domain (if available)                                                                     | 08/08/2025 | 08/08/2025      | Amplify console guide                     |
| 5   | - Test CI/CD pipeline by making code changes <br> - Configure environment variables for API endpoints <br> - Verify deployment success                                                              | 09/08/2025 | 09/08/2025      | Amplify deployment guide                  |


### Week 6 Achievements:

* Successfully created React.js frontend application for Coffee Cloud with the following features:
  * **Login/Registration page**: User authentication interface
  * **Menu page**: Display coffee products with prices and descriptions
  * **Shopping cart**: Add/remove items and calculate totals
  * **Order history**: View past orders and track status
  * **Points system**: Display customer loyalty points

* Set up AWS Amplify hosting with automatic CI/CD pipeline:
  * Connected GitHub repository to Amplify
  * Configured automatic deployment on code commits
  * Set up environment-specific builds (dev/prod)
  * Custom domain configuration ready for future use

* Implemented responsive design for mobile and desktop users

* Successfully tested the complete deployment process:
  * Code changes trigger automatic builds
  * Build logs show successful deployment
  * Live application accessible via Amplify URL

* Configured environment variables for API Gateway endpoints connection

* Learned Amplify benefits for frontend developers:
  * No server configuration required
  * Automatic SSL certificate management
  * Global CDN for fast content delivery
  * Easy rollback to previous versions

* Created and secured an AWS Free Tier account, including enabling MFA and creating an initial IAM user.

* Navigated the AWS Management Console and located core services.

* Installed and configured the AWS CLI (access key, secret key, default region, output format).

* Performed basic CLI operations:
  * aws sts get-caller-identity
  * aws ec2 describe-instances
  * aws s3 ls

* Launched an EC2 instance, connected via SSH, and attached an EBS volume for practice.

* Next steps: practice with S3 and IAM, and save CLI snippets for repeatable tasks.
