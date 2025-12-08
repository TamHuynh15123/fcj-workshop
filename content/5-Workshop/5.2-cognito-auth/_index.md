---
title: "Multi-Role Authentication với Cognito"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Amazon Cognito Authentication - 3 User Roles

#### Tổng quan

Trong workshop này, bạn sẽ học cách implement authentication system với **Amazon Cognito** cho Coffee Cloud Platform. Hệ thống hỗ trợ 3 nhóm người dùng khác nhau: **Customer**, **Shipper**, và **Admin**, mỗi nhóm có quyền truy cập và chức năng riêng.

**Amazon Cognito** là dịch vụ quản lý user authentication và authorization với những tính năng:
- 👥 User Pool với multi-group support
- 🔐 Secure authentication với JWT tokens
- 📧 Email verification và password reset
- 🆓 Free Tier: 50,000 MAU (Monthly Active Users)
- 🔑 Social login (Google, Facebook) - optional

#### Kiến trúc

```
ReactJS Frontend ←→ Amazon Cognito User Pool
                         ├── Customer Group
                         ├── Shipper Group  
                         └── Admin Group
                              ↓ JWT Token
                         Backend API (Workshop 3)
```

#### Nội dung

1. [Workshop Overview](5.2.1-overview/)
2. [Prerequisites](5.2.2-prerequisites/)
3. [Create Cognito User Pool](5.2.3-create-user-pool/)
4. [Configure User Groups](5.2.4-configure-groups/)
5. [Integrate with React Frontend](5.2.5-integrate-frontend/)
6. [Testing & Verification](5.2.6-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **90-120 phút**

#### Yêu cầu
- ✅ Đã hoàn thành Workshop 1 (Amplify Frontend)
- ✅ AWS Account với quyền tạo Cognito User Pool
- ✅ Frontend app đang chạy trên Amplify
- ✅ Hiểu biết cơ bản về JWT và authentication flow

#### User Roles trong Coffee Cloud

| Role | Permissions | Functions |
|------|-------------|-----------|
| **Customer** | Đặt hàng, xem lịch sử, tích điểm | Browse menu, Place orders, Track delivery, Redeem vouchers |
| **Shipper** | Xem đơn hàng, cập nhật trạng thái | Accept orders, Update delivery status, Navigate routes |
| **Admin** | Quản lý toàn bộ hệ thống | Manage products, View analytics, Manage users, Configure settings |
