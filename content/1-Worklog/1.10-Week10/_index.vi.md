---
title: "Worklog Tuần 10"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 10:

* Tìm hiểu giám sát và audit với CloudWatch và CloudTrail.
* Tạo IAM role cho dịch vụ và viết policy theo nguyên tắc least-privilege.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Đọc về CloudWatch & CloudTrail; lên kế hoạch các tài nguyên cần monitor.                                                                                                                 | 10/11/2025   | 10/11/2025      | CloudWatch & CloudTrail docs               |
| 3   | - Cài đặt và cấu hình CloudWatch Agent trên EC2; thu thập metrics hệ thống và ứng dụng (CPU, memory, disk).                                                                                 | 11/11/2025   | 11/11/2025      | CloudWatch agent guide                     |
| 4   | - Tạo dashboard CloudWatch: thêm widgets cho EC2 và RDS; thêm biểu đồ custom metric cho ứng dụng.                                                                                          | 12/11/2025   | 12/11/2025      | CloudWatch dashboards docs                 |
| 5   | - Định nghĩa CloudWatch alarms (CPU, memory qua agent, disk) và tạo SNS topic để nhận cảnh báo; test trigger alarm.                                                                          | 13/11/2025   | 13/11/2025      | CloudWatch Alarms & SNS docs               |
| 6   | - Bật CloudTrail, cấu hình trail tới S3, kiểm tra logs cho hoạt động console và API; rà soát các event nghi vấn.                                                                             | 14/11/2025   | 14/11/2025      | CloudTrail docs                            |


### Kết quả đạt được tuần 10:

* Thiết lập CloudWatch metrics và dashboard để giám sát EC2, RDS và metric ứng dụng.

* Tạo CloudWatch Alarms cho CPU, memory (sử dụng agent) và disk usage; cấu hình SNS để gửi thông báo.

* Kích hoạt CloudTrail để ghi lại hoạt động API và lưu trữ log vào S3.

* Tạo IAM role cho EC2 và role cho automation với quyền giới hạn.

* Soạn và thử nghiệm policy S3 read-only, điều chỉnh quyền để tuân theo least-privilege.

* Ghi chú: tiếp tục ghi IaC để tự động hóa các cấu hình này.


