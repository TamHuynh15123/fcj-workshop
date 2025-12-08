---
title: "Prerequisites"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Prerequisites

Before starting this workshop, make sure you have the following tools and accounts set up.

#### 1. AWS Account

You need an AWS account with permissions to create:
- ✅ Elastic Beanstalk applications and environments
- ✅ EC2 instances (t2.micro for free tier)
- ✅ Application Load Balancers
- ✅ DynamoDB tables
- ✅ IAM roles and policies
- ✅ CloudWatch logs

**Cost:** If using Free Tier, this workshop should cost **$0-2** for testing.

[Create AWS Account](https://aws.amazon.com/free/) if you don't have one.

#### 2. Development Tools

##### .NET 8.0 SDK
Required to build the Web API.

**Windows:**
```powershell
# Download and install from Microsoft
winget install Microsoft.DotNet.SDK.8
```

**Verify installation:**
```bash
dotnet --version
# Should show: 8.0.x
```

[Download .NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

##### AWS CLI (Optional)
Helpful for advanced configurations.

**Windows:**
```powershell
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```

**Mac:**
```bash
brew install awscli
```

**Configure AWS CLI:**
```bash
aws configure
# AWS Access Key ID: [Your Key]
# AWS Secret Access Key: [Your Secret]
# Default region: us-east-1
# Default output format: json
```

[AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

#### 3. Code Editor

**Visual Studio Code** (Recommended)
- Download from [code.visualstudio.com](https://code.visualstudio.com/)

**Recommended Extensions:**
- C# Dev Kit
- AWS Toolkit
- REST Client (for API testing)
- GitLens (for version control)

**OR Visual Studio 2022** (Alternative)
- Download from [visualstudio.microsoft.com](https://visualstudio.microsoft.com/)
- Select "ASP.NET and web development" workload

#### 4. Previous Workshop

⚠️ **Required:** You must have completed **Workshop 1: Deploy Frontend with Amplify**

Why? Because:
- Your frontend needs to connect to this backend API
- You need the Amplify URL for CORS configuration
- Understanding the frontend helps design proper API endpoints

If you haven't completed Workshop 1, go back and complete it first:
→ [Workshop 5.1: Deploy Frontend with Amplify](../5.1-amplify-frontend/)

#### 5. Knowledge Requirements

**Must Have:**
- ✅ Basic C# programming
- ✅ Understanding of REST APIs (GET, POST, PUT, DELETE)
- ✅ Basic command line usage
- ✅ Git basics (clone, commit, push)

**Nice to Have:**
- 🔸 AWS Console navigation
- 🔸 JSON data format
- 🔸 HTTP status codes (200, 400, 500, etc.)
- 🔸 Zip file operations

**Don't Worry If You're New To:**
- Elastic Beanstalk (we'll guide you step by step via Console)
- DynamoDB (we'll use simple operations)
- Auto-scaling configurations
- Load balancer setup

#### 6. System Requirements

**Minimum:**
- OS: Windows 10/11, macOS 10.15+, or Linux
- RAM: 4 GB
- Disk Space: 5 GB free
- Internet: Stable connection for downloads and AWS Console

**Recommended:**
- RAM: 8 GB
- Disk Space: 10 GB free
- CPU: 2+ cores

#### 7. Preparation Checklist

Before proceeding, check off each item:

```
□ AWS account created and accessible
□ .NET 8.0 SDK installed (dotnet --version works)
□ Code editor (VS Code or Visual Studio) installed
□ Workshop 1 completed (Frontend on Amplify)
□ Web browser for AWS Console access
□ At least 90 minutes of uninterrupted time
```

#### 8. Project Structure Preview

Here's what we'll build:

```
CoffeeCloudAPI/
├── Controllers/
│   ├── MenuController.cs
│   ├── OrderController.cs
│   └── HealthController.cs
├── Models/
│   ├── MenuItem.cs
│   ├── Order.cs
│   └── OrderItem.cs
├── Services/
│   ├── IMenuService.cs
│   ├── MenuService.cs
│   ├── IOrderService.cs
│   └── OrderService.cs
├── Program.cs
├── appsettings.json
└── CoffeeCloudAPI.csproj
```

#### 9. Costs Reminder

**Free Tier Coverage (First 12 months):**
- EC2: 750 hours/month of t2.micro
- ELB: 750 hours/month + 15 GB data
- DynamoDB: 25 GB storage + 25 WCU/RCU

**What This Means:**
- If you use 1 EC2 instance 24/7: **FREE**
- If you use 2 EC2 instances 24/7: **$8-16/month** (1 is free, 1 is paid)

**For This Workshop:**
We'll configure to stay in free tier during development and testing.

#### Ready?

✅ All prerequisites installed and configured?  
✅ Workshop 1 completed?  
✅ Have 90+ minutes available?  

Great! Let's create the .NET API! →

