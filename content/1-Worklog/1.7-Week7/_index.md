---
title: "Week 7 Worklog"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Integrate React frontend with Lambda backend APIs
* Implement user authentication flow with Cognito
* Test core Coffee Cloud functionalities

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Connect React frontend to API Gateway endpoints <br> - Install and configure AWS SDK for JavaScript <br> - Set up API service layer in React                                                      | 12/08/2025 | 12/08/2025      | AWS SDK documentation                     |
| 2   | - Implement user login/registration flow <br> - Integrate Cognito authentication with React <br> - Test user session management                                                                      | 13/08/2025 | 13/08/2025      | Cognito JavaScript SDK                    |
| 3   | - Connect product listing to DynamoDB <br> - Implement shopping cart functionality <br> - Test add/remove items from cart                                                                           | 14/08/2025 | 14/08/2025      | React state management                    |
| 4   | - Implement order creation flow <br> - Connect order processing to Lambda functions <br> - Test order placement and data storage                                                                      | 15/08/2025 | 15/08/2025      | Lambda integration                        |
| 5   | - Test points system functionality <br> - Implement order history display <br> - Test complete user journey from registration to order                                                              | 16/08/2025 | 16/08/2025      | End-to-end testing                        |


### Week 7 Achievements:

* Successfully integrated React frontend with AWS backend services:
  * Configured AWS SDK for JavaScript in React application
  * Set up API service layer for clean separation of concerns
  * Implemented proper error handling for API calls

* Completed user authentication integration:
  * Users can register new accounts through Cognito
  * Login/logout functionality working properly
  * Session management with JWT tokens
  * Role-based access control (Customer, Shipper, Admin)

* Implemented core Coffee Cloud features:
  * **Product Display**: Coffee menu loaded from DynamoDB
  * **Shopping Cart**: Add/remove items with quantity management
  * **Order Processing**: Complete order flow from cart to database
  * **Points System**: Automatic points calculation and display

* Completed end-to-end testing of user journey:
  * New user registration → Email verification → Login → Browse menu → Add to cart → Place order → Earn points

* Fixed integration issues and improved user experience:
  * Loading states for better user feedback
  * Input validation on both frontend and backend
  * Proper error messages for failed operations

* Deployed a simple static website to an S3 bucket and verified public access settings and bucket policy.

* Documented IAM and S3 commands and common troubleshooting steps for permissions and public access.

* Next steps: study VPC fundamentals and network security groups.
