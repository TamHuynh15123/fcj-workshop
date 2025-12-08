---
title: "Deploy Frontend với AWS Amplify"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Deploy ReactJS Frontend với AWS Amplify

#### Tổng quan

Trong workshop này, bạn sẽ học cách deploy ứng dụng ReactJS cho Coffee Cloud Platform lên **AWS Amplify** với tính năng CI/CD tự động. AWS Amplify giúp bạn dễ dàng host static website và tự động build + deploy mỗi khi bạn push code lên Git repository.

**AWS Amplify** là dịch vụ fully-managed giúp deploy và host các ứng dụng web frontend với những tính năng:
- 🚀 Automatic CI/CD pipeline từ Git repository
- 🔒 Built-in SSL certificate miễn phí
- 🌍 Global CDN với performance cao
- 💰 Free tier: 1000 build minutes/month, 15GB storage

#### Kiến trúc

```
GitHub Repository → AWS Amplify → CloudFront CDN → Users
     ↓ (push code)      ↓ (auto build)    ↓ (distribute)
```

#### Nội dung

1. [Workshop Overview](5.1.1-overview/)
2. [Prerequisites](5.1.2-prerequisites/)
3. [Setup Git Repository](5.1.3-setup-git/)
4. [Deploy to AWS Amplify](5.1.4-deploy-amplify/)
5. [Configure Build Settings](5.1.5-configure-build/)
6. [Testing & Verification](5.1.6-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **60-90 phút**

#### Yêu cầu
- ✅ AWS Account (Free Tier eligible)
- ✅ GitHub account
- ✅ Node.js 18+ và npm
- ✅ Git installed
- ✅ Code editor (VS Code recommended)
