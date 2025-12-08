---
title: "Tổng quan Workshop"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Tổng quan Workshop

#### Bạn sẽ xây dựng gì

Trong workshop này, bạn sẽ tạo backend **Web API .NET 8.0** sẵn sàng cho production cho **Coffee Cloud Platform** và triển khai trực tiếp lên **AWS Elastic Beanstalk** qua **AWS Console**. API bao gồm **Swagger UI** để test và tài liệu hóa dễ dàng.

- ☕ **Quản lý Menu** - Lấy tất cả sản phẩm, lọc theo danh mục
- 🛒 **Xử lý Đơn hàng** - Tạo đơn hàng, cập nhật trạng thái, theo dõi đơn hàng
- 👤 **Quản lý Người dùng** - Vai trò Customer, Shipper, Admin
- 📊 **Phân tích** - Thống kê đơn hàng, báo cáo doanh thu
- 📝 **Swagger UI** - Tài liệu và testing API tương tác

#### Tổng quan Kiến trúc

```
┌─────────────────────────────────────────────────────┐
│           ReactJS Frontend (Amplify)                │
│         https://your-app.amplifyapp.com             │
└──────────────────┬──────────────────────────────────┘
                   │ HTTPS API Calls
                   ▼
┌─────────────────────────────────────────────────────┐
│      Application Load Balancer (ALB)                │
│         - Kiểm tra sức khỏe                         │
│         - Kết thúc SSL                              │
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

#### Công nghệ chính

| Công nghệ | Mục đích | Tại sao? |
|-----------|----------|----------|
| **.NET 8.0** | Framework Web API | Hiện đại, nhanh, đa nền tảng C# |
| **Swagger UI** | Tài liệu API | Testing tương tác, tài liệu tự động tạo |
| **Elastic Beanstalk** | Dịch vụ Platform | Tự động mở rộng, cân bằng tải, giám sát |
| **Application Load Balancer** | Phân phối Traffic | Khả dụng cao, hỗ trợ SSL |
| **DynamoDB** | Cơ sở dữ liệu NoSQL | Serverless, mở rộng, độ trễ thấp |
| **CloudWatch** | Giám sát | Logs, metrics, alarms |

#### Bạn sẽ học được gì

✅ **Phát triển Backend**
- Tạo RESTful API với .NET 8.0
- Triển khai các thao tác CRUD
- Cấu trúc controllers và services
- Xử lý lỗi và validation
- Cấu hình Swagger cho tài liệu API

✅ **Triển khai qua AWS Console**
- Publish ứng dụng .NET
- Tạo Elastic Beanstalk environment qua Console
- Cấu hình environment variables
- Thiết lập chính sách auto-scaling
- Giám sát sức khỏe ứng dụng

✅ **Testing & Tài liệu**
- Sử dụng Swagger UI để test API
- Test tất cả endpoints tương tác
- Xem tài liệu API
- Giám sát logs trong CloudWatch


#### Quy trình Workshop

```
Bước 1: Kiểm tra Yêu cầu
   ↓
Bước 2: Tạo .NET API Project
   ↓
Bước 3: Xây dựng Controllers & Services
   ↓
Bước 4: Test Locally với Swagger
   ↓
Bước 5: Publish Ứng dụng
   ↓
Bước 6: Tạo Elastic Beanstalk Environment
   ↓
Bước 7: Upload và Deploy qua Console
   ↓
Bước 8: Cấu hình Auto-Scaling
   ↓
Bước 9: Test với Swagger UI
```

#### Ước tính Chi phí

**Đủ điều kiện Free Tier:**
- Elastic Beanstalk: Không tính phí bổ sung
- EC2 t2.micro: 750 giờ/tháng (1 instance = miễn phí)
- DynamoDB: 25 GB storage, 25 WCU/RCU
- Data Transfer: 15 GB/tháng outbound

**Sau Free Tier:**
- 2 x t2.micro instances: ~$16/tháng
- Application Load Balancer: ~$16/tháng
- DynamoDB: Trả theo sử dụng (~$1-5/tháng cho apps nhỏ)

💡 **Mẹo:** Bạn có thể dùng 1 EC2 instance cho development/testing để ở trong free tier!

#### Bước tiếp theo

Sẵn sàng bắt đầu? Hãy kiểm tra các yêu cầu! →

