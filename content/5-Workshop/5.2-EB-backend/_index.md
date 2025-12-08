---
title: "Deploy Backend với Elastic Beanstalk"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Deploy .NET Backend với AWS Elastic Beanstalk

#### Tổng quan

Trong workshop này, bạn sẽ học cách deploy ứng dụng backend .NET 8.0 cho Coffee Cloud Platform lên **AWS Elastic Beanstalk** thông qua AWS Console. API sẽ được test với **Swagger UI** tích hợp sẵn.

**AWS Elastic Beanstalk** là platform-as-a-service (PaaS) với những tính năng:
- 🚀 Auto-scaling dựa trên traffic
- ⚖️ Load balancing tự động
- 📊 Monitoring và health checks
- 📦 Deploy trực tiếp từ .NET publish
- 🆓 Free Tier: 750 hours/month (t2.micro)

#### Kiến trúc

```
ReactJS Frontend (Amplify)
         ↓ HTTPS API calls
Application Load Balancer
         ↓
   EC2 Instances (Auto Scaling)
   Running .NET 8.0 API
         ↓
    DynamoDB
```

#### Nội dung

1. [Workshop Overview](5.2.1-overview/)
2. [Prerequisites](5.2.2-prerequisites/)
3. [Create .NET API Project](5.2.3-create-api/)
4. [Publish Application](5.2.4-publish-app/)
5. [Deploy to Elastic Beanstalk](5.2.5-deploy-beanstalk/)
6. [Testing with Swagger](5.2.6-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **120-150 phút**

#### Yêu cầu
- ✅ Đã hoàn thành Workshop 1 (Amplify Frontend)
- ✅ AWS Account với quyền tạo Elastic Beanstalk
- ✅ .NET SDK 8.0 installed
- ✅ Trình duyệt web để truy cập AWS Console và Swagger

| Role | Permissions | Functions |
|------|-------------|-----------|
| **Customer** | Đặt hàng, xem lịch sử, tích điểm | Browse menu, Place orders, Track delivery, Redeem vouchers |
| **Shipper** | Xem đơn hàng, cập nhật trạng thái | Accept orders, Update delivery status, Navigate routes |
| **Admin** | Quản lý toàn bộ hệ thống | Manage products, View analytics, Manage users, Configure settings |
