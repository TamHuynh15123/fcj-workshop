---
title: "Worklog Tuần 11"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 11:

* Tìm hiểu Infrastructure as Code (IaC) cơ bản và thực hành với CloudFormation và Terraform.
* Tự động hóa việc tạo một stack nhỏ bao gồm networking, compute và storage.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Đọc về CloudFormation và xem ví dụ template; xác định các tài nguyên sẽ đưa vào stack đơn giản (VPC + EC2).                                                                             | 17/11/2025   | 17/11/2025      | CloudFormation docs                        |
| 3   | - Viết CloudFormation template để tạo VPC, public subnet và EC2; validate template bằng cfn-lint hoặc console.                                                                             | 18/11/2025   | 18/11/2025      | CFN template examples                      |
| 4   | - Cài Terraform; viết cấu hình Terraform ban đầu (provider, VPC, EC2) và chạy plan để so sánh workflow với CloudFormation.                                                                  | 19/11/2025   | 19/11/2025      | Terraform docs                             |
| 5   | - Modularize Terraform: tạo module nhỏ cho EC2 (biến cho AMI, instance type, security group) và sử dụng tfstate để theo dõi tài nguyên.                                                     | 20/11/2025   | 20/11/2025      | Terraform modules guide                    |
| 6   | - Thử huỷ stack cho cả CloudFormation và Terraform; đảm bảo không còn tài nguyên thừa (EBS, Elastic IP); ghi lại khác biệt của hai công cụ.                                               | 21/11/2025   | 21/11/2025      | IaC teardown best practices                |


### Kết quả đạt được tuần 11:

* Nắm được các khái niệm cơ bản của CloudFormation và viết template để tạo VPC, public subnet và EC2 instance.

* Cài đặt và sử dụng Terraform để provision lại cùng stack, so sánh cách quản lý state và workflow.

* Tham số hoá template và viết module nhỏ để tái sử dụng IaC; ghi lại quy trình triển khai.

* Thực hành huỷ stack và xác minh tài nguyên (EBS, Elastic IP) được dọn sạch.

* Ghi chú: áp dụng IaC cho bài mini-project cuối khóa.


