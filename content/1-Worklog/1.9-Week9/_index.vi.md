---
title: "Worklog Tuần 9"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 9:

* Tìm hiểu các dịch vụ cơ sở dữ liệu của AWS (RDS, Aurora, DynamoDB) và chiến lược backup.
* Triển khai cơ sở dữ liệu quản lý và kết nối an toàn từ host ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu các dịch vụ database quản lý (RDS, DynamoDB), so sánh use-case và best practices.                                                                                              | 03/11/2025   | 03/11/2025      | RDS docs, DynamoDB docs                    |
| 3   | - Tạo RDS subnet group và parameter group; khởi tạo RDS (MySQL) trong private subnet (Multi-AZ tắt để tiết kiệm chi phí).                                                                  | 04/11/2025   | 04/11/2025      | RDS launch guide                           |
| 4   | - Cấu hình security group để chỉ cho phép traffic tới DB từ EC2 ứng dụng; kiểm tra kết nối DB từ EC2/bastion và chạy một vài query test.                                                  | 05/11/2025   | 05/11/2025      | RDS connection docs                        |
| 5   | - Tìm hiểu DynamoDB: tạo bảng mẫu, thử nghiệm CRUD, so sánh chế độ on-demand vs provisioned.                                                                                              | 06/11/2025   | 06/11/2025      | DynamoDB docs                              |
| 6   | - Thiết lập snapshot tự động cho RDS; thực hành restore snapshot sang instance mới; ghi nhận chiến lược retention và lựa chọn cross-region.                                                  | 07/11/2025   | 07/11/2025      | Backup & snapshot docs                     |


### Kết quả đạt được tuần 9:

* Triển khai Amazon RDS (MySQL) trong private subnet và xác thực kết nối an toàn từ EC2.

* Thử nghiệm DynamoDB cho trường hợp key-value và so sánh hai chế độ provisioned vs on-demand.

* Cấu hình snapshot tự động cho RDS và thực hành phục hồi point-in-time.

* Đánh giá các lựa chọn sao lưu, bao gồm cross-region copy và chi phí liên quan.

* Ghi chú: tiếp tục cấu hình giám sát và cảnh báo cho DB bằng CloudWatch.


