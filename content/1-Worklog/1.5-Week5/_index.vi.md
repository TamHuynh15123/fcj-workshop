---
title: "Worklog Tuần 5"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

Mục tiêu tuần 5:
- Bắt đầu học cách dịch và viết blog kỹ thuật về AWS
- Tìm hiểu về các dịch vụ Security và Monitoring của AWS
- Thực hành với CloudWatch và IAM

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo |
|------|----------|--------------|---------------|-------------------|
| 1 | Tìm hiểu AWS IAM:<br>- Users, Groups, Roles<br>- Policies và Permissions<br>- Best practices for IAM | 6/10/2025 | 6/10/2025 | AWS Documentation, CloudJourney |
| 2 | Thực hành với IAM:<br>- Tạo users và groups<br>- Gán policies<br>- Thực hành với roles | 7/10/2025 | 7/10/2025 | AWS Console |
| 3 | Tìm hiểu Amazon CloudWatch:<br>- Metrics và Logs<br>- Alarms và Notifications<br>- Monitoring EC2 và RDS | 8/10/2025 | 8/10/2025 | AWS Documentation |
| 4 | Bắt đầu dịch blog đầu tiên:<br>- Chọn blog AWS phù hợp (cơ bản)<br>- Dịch 50% nội dung<br>- Review với mentor | 9/10/2025 | 9/10/2025 | AWS Blog, Mentor guidance |
| 5 | Làm việc nhóm và hoàn thiện:<br>- Chia sẻ tiến độ dịch blog<br>- Hoàn thiện bài dịch<br>- Planning cho workshop | 10/10/2025 | 12/10/2025 | Team collaboration |

### Thành tích tuần 5:

* Thành công tạo AWS Lambda functions cho Coffee Cloud backend:
  * **User Registration**: Xử lý đăng ký người dùng mới với tích hợp Cognito
  * **User Authentication**: Xác thực thông tin đăng nhập và trả về JWT tokens
  * **Product Management**: Lấy menu cà phê từ DynamoDB
  * **Order Processing**: Tạo đơn hàng mới và cập nhật inventory
  * **Points System**: Tính toán và cập nhật điểm thưởng khách hàng

* Thiết lập API Gateway với các RESTful endpoints:
  * POST /api/auth/register
  * POST /api/auth/login
  * GET /api/products
  * POST /api/orders
  * GET /api/points/{userId}

* Cấu hình quyền Lambda function và IAM roles cho truy cập DynamoDB

* Test tất cả API endpoints sử dụng Postman và xác minh xử lý lỗi đúng cách

* Tìm hiểu lợi ích của serverless architecture:
  * Không cần quản lý server
  * Tự động scale theo nhu cầu
  * Mô hình giá pay-per-request
  * Tính khả dụng cao trong giới hạn AWS Free Tier

* Triển khai các biện pháp bảo mật cơ bản bao gồm cấu hình CORS và xác thực input


