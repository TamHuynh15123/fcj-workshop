---
title: "Workshop Overview"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Workshop Overview

#### What You'll Build

In this workshop, you'll create a production-ready **.NET 8.0 Web API** backend for **Coffee Cloud Platform** and deploy it directly to **AWS Elastic Beanstalk** via AWS Console. The API includes **Swagger UI** for easy testing and documentation.

- ☕ **Menu Management** - Get all products, filter by category
- 🛒 **Order Processing** - Create orders, update status, track orders
- 👤 **User Management** - Customer, Shipper, Admin roles
- 📊 **Analytics** - Order statistics, revenue reports
- 📝 **Swagger UI** - Interactive API documentation and testing

#### Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│           ReactJS Frontend (Amplify)                │
│         https://your-app.amplifyapp.com             │
└──────────────────┬──────────────────────────────────┘
                   │ HTTPS API Calls
                   ▼
┌─────────────────────────────────────────────────────┐
│      Application Load Balancer (ALB)                │
│         - Health checks                             │
│         - SSL termination                           │
└──────────────────┬──────────────────────────────────┘
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
┌──────────────┐      ┌──────────────┐
│ EC2 Instance │      │ EC2 Instance │
│   (t2.micro) │      │   (t2.micro) │
│              │      │              │
│  .NET 8.0    │      │  .NET 8.0    │
│  Web API     │      │  Web API     │
│              │      │              │
│  + Swagger   │      │  + Swagger   │
└──────┬───────┘      └──────┬───────┘
       │                     │
       └──────────┬──────────┘
                  ▼
          ┌───────────────┐
          │   DynamoDB    │
          │               │
          │ - MenuItems   │
          │ - Orders      │
          │ - Users       │
          └───────────────┘
```

#### Key Technologies

| Technology | Purpose | Why? |
|------------|---------|------|
| **.NET 8.0** | Web API Framework | Modern, fast, cross-platform C# |
| **Swagger UI** | API Documentation | Interactive testing, auto-generated docs |
| **Elastic Beanstalk** | Platform Service | Auto-scaling, load balancing, monitoring |
| **Application Load Balancer** | Traffic Distribution | High availability, SSL support |
| **DynamoDB** | NoSQL Database | Serverless, scalable, low latency |
| **CloudWatch** | Monitoring | Logs, metrics, alarms |

#### What You'll Learn

✅ **Backend Development**
- Create RESTful API with .NET 8.0
- Implement CRUD operations
- Structure controllers and services
- Handle errors and validation
- Configure Swagger for API documentation

✅ **AWS Console Deployment**
- Publish .NET application
- Create Elastic Beanstalk environment via Console
- Configure environment variables
- Set up auto-scaling policies
- Monitor application health

✅ **Testing & Documentation**
- Use Swagger UI for API testing
- Test all endpoints interactively
- View API documentation
- Monitor logs in CloudWatch

#### Workshop Flow

```
Step 1: Prerequisites Check
   ↓
Step 2: Create .NET API Project
   ↓
Step 3: Build Controllers & Services
   ↓
Step 4: Test Locally with Swagger
   ↓
Step 5: Publish Application
   ↓
Step 6: Create Elastic Beanstalk Environment
   ↓
Step 7: Upload and Deploy via Console
   ↓
Step 8: Configure Auto-Scaling
   ↓
Step 9: Test with Swagger UI
```

#### Cost Estimation

**Free Tier Eligible:**
- Elastic Beanstalk: No additional charge
- EC2 t2.micro: 750 hours/month (1 instance = free)
- DynamoDB: 25 GB storage, 25 WCU/RCU
- Data Transfer: 15 GB/month outbound

**After Free Tier:**
- 2 x t2.micro instances: ~$16/month
- Application Load Balancer: ~$16/month
- DynamoDB: Pay per use (~$1-5/month for small apps)

💡 **Tip:** You can use 1 EC2 instance for development/testing to stay in free tier!

#### Next Steps

Ready to begin? Let's check the prerequisites! →

