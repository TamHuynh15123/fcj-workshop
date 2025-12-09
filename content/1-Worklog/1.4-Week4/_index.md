---
title: "Week 4 Worklog"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Set up DynamoDB database for Coffee Cloud project
* Learn DynamoDB basics and create tables for user and order data
* Set up AWS Cognito for user authentication

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Learn DynamoDB fundamentals <br> - Understand NoSQL concepts, primary keys, and indexes                                                                                                             | 22/07/2025 | 22/07/2025      | DynamoDB documentation                    |
| 2   | - Create DynamoDB tables for Coffee Cloud: <br>&emsp; + Users table <br>&emsp; + Products table <br>&emsp; + Orders table <br>&emsp; + Points table                                                 | 23/07/2025 | 23/07/2025      | DynamoDB console guide                    |
| 3   | - Configure table schemas and indexes <br> - Add sample data for testing <br> - Practice basic CRUD operations                                                                                        | 24/07/2025 | 24/07/2025      | DynamoDB SDK documentation                |
| 4   | - Learn AWS Cognito for user authentication <br> - Understand User Pools and Identity Pools                                                                                                           | 25/07/2025 | 25/07/2025      | Cognito documentation                     |
| 5   | - Create Cognito User Pool for Coffee Cloud <br> - Configure sign-up/sign-in settings <br> - Set up user groups (Customer, Shipper, Admin)                                                          | 26/07/2025 | 26/07/2025      | Cognito console guide                     |


### Week 4 Achievements:

* Successfully created DynamoDB tables for Coffee Cloud project:
  * **Users table**: Stores customer, shipper, and admin information
  * **Products table**: Coffee menu items with prices and descriptions  
  * **Orders table**: Order details and status tracking
  * **Points table**: Customer loyalty points system

* Configured proper primary keys and secondary indexes for efficient queries

* Added sample data to all tables for testing purposes

* Successfully set up AWS Cognito User Pool with the following configuration:
  * Email-based sign-in
  * Password policies for security
  * Three user groups: Customer, Shipper, Admin
  * Email verification for new accounts

* Tested basic DynamoDB operations using AWS console:
  * Create, read, update, delete operations
  * Query and scan operations
  * Understanding of capacity units and billing

* Learned DynamoDB best practices for cost optimization within Free Tier limits

* Acquired the ability to connect between the web interface and CLI to manage AWS resources in parallel.
* ...
