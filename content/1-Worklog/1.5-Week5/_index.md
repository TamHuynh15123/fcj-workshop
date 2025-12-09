---
title: "Week 5 Worklog"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Set up AWS Lambda functions for Coffee Cloud backend
* Learn serverless architecture concepts
* Create basic API endpoints using Lambda and API Gateway

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Learn AWS Lambda fundamentals <br> - Understand serverless computing benefits <br> - Learn about Lambda triggers and runtime environments                                                           | 29/07/2025 | 29/07/2025      | Lambda documentation                      |
| 2   | - Create first Lambda function for user registration <br> - Set up function in Node.js runtime <br> - Test function using Lambda console                                                             | 30/07/2025 | 30/07/2025      | Lambda console guide                      |
| 3   | - Create Lambda functions for: <br>&emsp; + User authentication <br>&emsp; + Product listing <br>&emsp; + Order creation <br>&emsp; + Points calculation                                            | 31/07/2025 | 31/07/2025      | Lambda best practices                     |
| 4   | - Learn AWS API Gateway basics <br> - Understand REST API concepts <br> - Create API Gateway for Coffee Cloud                                                                                         | 01/08/2025 | 01/08/2025      | API Gateway documentation                 |
| 5   | - Connect Lambda functions to API Gateway <br> - Create REST endpoints for all functions <br> - Test API calls using Postman                                                                        | 02/08/2025 | 02/08/2025      | API Gateway integration guide            |


### Week 5 Achievements:

* Successfully created AWS Lambda functions for Coffee Cloud backend:
  * **User Registration**: Handles new user sign-up with Cognito integration
  * **User Authentication**: Validates login credentials and returns JWT tokens  
  * **Product Management**: Retrieves coffee menu from DynamoDB
  * **Order Processing**: Creates new orders and updates inventory
  * **Points System**: Calculates and updates customer loyalty points

* Set up API Gateway with RESTful endpoints:
  * POST /api/auth/register
  * POST /api/auth/login
  * GET /api/products
  * POST /api/orders
  * GET /api/points/{userId}

* Configured Lambda function permissions and IAM roles for DynamoDB access

* Tested all API endpoints using Postman and verified proper error handling

* Learned serverless architecture benefits:
  * No server management required
  * Automatic scaling based on demand
  * Pay-per-request pricing model
  * High availability within AWS Free Tier limits

* Implemented basic security measures including CORS configuration and input validation

* Successfully created and configured an AWS Free Tier account.

* Became familiar with the AWS Management Console and learned how to find, access, and use services via the web interface.

* Installed and configured AWS CLI on the computer, including:
  * Access Key
  * Secret Key
  * Default Region
  * ...

* Used AWS CLI to perform basic operations such as:

  * Check account & configuration information
  * Retrieve the list of regions
  * View EC2 service
  * Create and manage key pairs
  * Check information about running services
  * ...

* Acquired the ability to connect between the web interface and CLI to manage AWS resources in parallel.
* ...
