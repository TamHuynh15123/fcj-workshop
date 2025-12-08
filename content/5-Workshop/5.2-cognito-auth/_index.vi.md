---
title: "Multi-Role Authentication với Cognito"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Amazon Cognito Authentication - 3 Nhóm Người Dùng

#### Tổng quan

Trong workshop này, bạn sẽ học cách triển khai hệ thống xác thực với **Amazon Cognito** cho Coffee Cloud Platform. Hệ thống hỗ trợ 3 nhóm người dùng khác nhau: **Customer**, **Shipper**, và **Admin**, mỗi nhóm có quyền truy cập và chức năng riêng.

**Amazon Cognito** là dịch vụ quản lý xác thực và phân quyền người dùng với những tính năng:
- 👥 User Pool với hỗ trợ nhiều nhóm
- 🔐 Xác thực an toàn với JWT tokens
- 📧 Xác minh email và đặt lại mật khẩu
- 🆓 Free Tier: 50,000 MAU (Monthly Active Users)
- 🔑 Đăng nhập mạng xã hội (Google, Facebook) - tùy chọn

#### Kiến trúc

```
ReactJS Frontend ←→ Amazon Cognito User Pool
                         ├── Nhóm Customer
                         ├── Nhóm Shipper  
                         └── Nhóm Admin
                              ↓ JWT Token
                         Backend API (Workshop 3)
```

#### Nội dung

1. [Tổng quan Workshop](5.2.1-overview/)
2. [Yêu cầu trước khi bắt đầu](5.2.2-prerequisites/)
3. [Tạo Cognito User Pool](5.2.3-create-user-pool/)
4. [Cấu hình User Groups](5.2.4-configure-groups/)
5. [Tích hợp với React Frontend](5.2.5-integrate-frontend/)
6. [Kiểm tra và xác minh](5.2.6-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **90-120 phút**

#### Yêu cầu
- ✅ Đã hoàn thành Workshop 1 (Amplify Frontend)
- ✅ Tài khoản AWS với quyền tạo Cognito User Pool
- ✅ Ứng dụng frontend đang chạy trên Amplify
- ✅ Hiểu biết cơ bản về JWT và authentication flow

#### Vai trò người dùng trong Coffee Cloud

| Vai trò | Quyền hạn | Chức năng |
|---------|-----------|-----------|
| **Customer** | Đặt hàng, xem lịch sử, tích điểm | Xem menu, Đặt hàng, Theo dõi giao hàng, Đổi voucher |
| **Shipper** | Xem đơn hàng, cập nhật trạng thái | Nhận đơn, Cập nhật trạng thái giao hàng, Điều hướng |
| **Admin** | Quản lý toàn bộ hệ thống | Quản lý sản phẩm, Xem báo cáo, Quản lý người dùng, Cấu hình |
