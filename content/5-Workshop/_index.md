---
title: "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Coffee Cloud Platform - AWS Workshop Series

Các workshop thực hành xây dựng Coffee Shop Order Platform trên AWS từ đầu đến cuối.

## 🎯 Workshop Overview

Trong series workshop này, bạn sẽ học cách xây dựng một ứng dụng web full-stack trên AWS, bao gồm frontend với ReactJS + Amplify, authentication với Cognito, và nhiều tính năng nâng cao khác.

**Coffee Cloud Platform** là một ứng dụng đặt hàng cà phê online với các tính năng:
- 🛒 Đặt hàng và thanh toán online
- 👥 Hệ thống phân quyền 3 nhóm: Customer, Shipper, Admin
- ⭐ Tích điểm và đổi voucher
- 📍 Theo dõi giao hàng real-time với GPS
- 📊 Dashboard quản lý cho Admin

---

## 📚 Workshop Series

### Core Workshops (Bắt buộc)

#### 1. [Deploy ReactJS Frontend với AWS Amplify](5.1-amplify-frontend/)
⏱️ **90 phút** | 🎯 **Beginner-Intermediate**

Tạo và deploy ứng dụng ReactJS lên AWS Amplify với CI/CD tự động từ GitHub. Học cách setup pipeline, configure build settings, và optimize performance.

**Bạn sẽ học:**
- Tạo React app với Vite
- Setup Git repository
- Deploy lên AWS Amplify
- Configure CI/CD pipeline
- Environment variables và build optimization

---

#### 2. [Multi-Role Authentication với Amazon Cognito](5.2-cognito-auth/)
⏱️ **120 phút** | 🎯 **Intermediate**

Implement authentication system với Amazon Cognito hỗ trợ 3 nhóm người dùng: Customer, Shipper, và Admin. Học về JWT tokens, role-based access control, và secure authentication flow.

**Bạn sẽ học:**
- Tạo Cognito User Pool
- Configure user groups và permissions
- Integrate Cognito với React
- JWT authentication và token management
- Role-based dashboards


---

## 📋 Prerequisites

Trước khi bắt đầu, đảm bảo bạn có:
- ✅ AWS Account (Free Tier eligible)
- ✅ GitHub account
- ✅ Node.js 18+ và npm
- ✅ Git installed
- ✅ Code editor (VS Code recommended)
- ✅ Hiểu biết cơ bản về React và JavaScript

---

## 💰 Cost Estimation

Với **AWS Free Tier**, tổng chi phí workshops:

| Service | Free Tier | After Free Tier |
|---------|-----------|-----------------|
| **Amplify** | 1000 build minutes/month | $0.01/min |
| **Cognito** | 50,000 MAU | $0.0055/MAU |
| **Elastic Beanstalk** | 750 hours/month (t2.micro) | ~$10/month |
| **DynamoDB** | 25 GB storage | $0.25/GB |
| **S3** | 5 GB storage | $0.023/GB |
| **Location Service** | 50,000 requests/month | $0.0004/request |

**Total estimated cost:** $0-5/month trong giai đoạn học

---

## 🚀 Getting Started

Bắt đầu với [Workshop 1: Deploy Frontend với AWS Amplify](5.1-amplify-frontend/)

---

## 📖 Additional Resources

- [AWS Free Tier](https://aws.amazon.com/free/)
- [AWS Documentation](https://docs.aws.amazon.com/)
- [React Documentation](https://react.dev/)
- [Coffee Cloud Proposal](../2-Proposal/)

---

{{% notice tip %}}
💡 **Tip:** Làm các workshop theo thứ tự để hiểu rõ kiến trúc tổng thể. Mỗi workshop build trên kiến thức từ workshop trước.
{{% /notice %}}

{{% notice warning %}}
⚠️ **Note:** Remember to clean up resources sau mỗi workshop để tránh chi phí ngoài ý muốn. Instructions có trong phần Cleanup của mỗi workshop.
{{% /notice %}}
