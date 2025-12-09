---
title: "Worklog Tuần 8"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Thiết lập dịch vụ notification (SNS và SES) cho Coffee Cloud
* Triển khai email notifications cho đơn hàng và khuyến mãi
* Thêm push notifications cho cập nhật trạng thái đơn hàng

### Nhiệm vụ thực hiện trong tuần:
| Ngày | Nhiệm vụ                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Tìm hiểu AWS SNS (Simple Notification Service) cơ bản <br> - Hiểu topics, subscriptions, và message formats <br> - Tạo SNS topic cho order notifications                                   | 19/08/2025 | 19/08/2025      | Tài liệu SNS                         |
| 2   | - Thiết lập AWS SES (Simple Email Service) <br> - Xác minh email domain/address <br> - Tạo email templates cho order confirmations                                                                     | 20/08/2025 | 20/08/2025      | Tài liệu SES                         |
| 3   | - Tích hợp SNS với Lambda functions <br> - Gửi notifications khi orders được tạo/cập nhật <br> - Test notification delivery                                                                    | 21/08/2025 | 21/08/2025      | Lambda + SNS integration                  |
| 4   | - Triển khai email notifications với SES <br> - Gửi order confirmation emails <br> - Tạo promotional email templates                                                                             | 22/08/2025 | 22/08/2025      | SES email templates                       |
| 5   | - Test toàn bộ notification flow <br> - Xác minh email delivery và formatting <br> - Test SMS notifications (tùy chọn)                                                                              | 23/08/2025 | 23/08/2025      | End-to-end notification testing           |


### Kết quả đạt được tuần 8:

* Thành công cấu hình AWS SNS cho Coffee Cloud notifications:
  * Tạo SNS topics cho các loại notification khác nhau (orders, promotions, alerts)
  * Thiết lập email subscriptions cho admin notifications
  * Cấu hình topic policies để truy cập an toàn từ Lambda functions

* Triển khai AWS SES cho email communications:
  * Xác minh sender email address cho development
  * Tạo professional email templates cho:
    - Email xác nhận đơn hàng
    - Email chào mừng người dùng mới
    - Newsletter khuyến mãi
    - Email reset mật khẩu

* Tích hợp notification services với Lambda functions:
  * Tạo đơn hàng trigger email xác nhận tự động
  * Cập nhật trạng thái đơn hàng gửi notifications real-time
  * Admin nhận alerts cho đơn hàng mới và system issues

* Nâng cao trải nghiệm người dùng Coffee Cloud:
  * Khách hàng nhận xác nhận đơn hàng ngay lập tức
  * Cập nhật real-time về chuẩn bị và giao hàng
  * Email templates chuyên nghiệp với branding Coffee Cloud

* Test độ tin cậy notification:
  * Email delivery hoạt động trong giới hạn SES sandbox
  * Xử lý lỗi phù hợp cho failed notifications
  * Monitor notification logs qua CloudWatch

* Học AWS communication services best practices:
  * Hiểu SES sandbox vs production mode
  * SNS pricing và message limits
  * IAM permissions phù hợp cho notification services

* Áp dụng NAT gateway để cho phép instances trong private subnet truy cập internet khi cần.

* Lưu lại sơ đồ VPC và các lệnh kiểm tra mạng (traceroute, curl) phục vụ việc debug.


