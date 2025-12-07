---
title: "Worklog Tuần 12"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---
### Mục tiêu tuần 12:

* Hoàn thành mini-project: tích hợp các dịch vụ cốt lõi thành một kiến trúc nhỏ có tài liệu.
* Thực hiện dọn dẹp tài nguyên, tổng kết kiến thức đã học và chuẩn bị báo cáo/giới thiệu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Hoàn thiện sơ đồ kiến trúc mini-project và checklist triển khai; chuẩn bị phân công IaC.                                                                                                 | 24/11/2025   | 24/11/2025      | Project notes                              |
| 3   | - Viết template IaC (Terraform/CloudFormation) cho các thành phần: VPC, subnet, EC2, RDS, S3; tham số hoá để tái sử dụng.                                                                 | 25/11/2025   | 25/11/2025      | IaC templates                              |
| 4   | - Triển khai stack thử nghiệm; chạy smoke tests để kiểm tra kết nối giữa các thành phần và luồng dữ liệu.                                                                                  | 26/11/2025   | 26/11/2025      | Deployment logs                             |
| 5   | - Thiết lập giám sát và cảnh báo cho các thành phần chính; viết README hướng dẫn deploy/rollback; nếu cần seed DB thì thực hiện.                                                            | 27/11/2025   | 27/11/2025      | README, CloudWatch config                   |
| 6   | - Dọn dẹp tài nguyên tạm (buckets thử nghiệm, instances, access key tạm); hoàn thiện deliverables: IaC templates, sơ đồ kiến trúc, ghi chú demo.                                         | 28/11/2025   | 28/11/2025      | Project deliverables                        |


### Kết quả đạt được tuần 12:

* Hoàn thành mini-project: tích hợp S3 (static content), EC2 (ứng dụng) và RDS (database) trong private subnet.

* Viết script và template IaC (Terraform/CloudFormation) để tự động hóa triển khai; thêm README hướng dẫn.

* Thực hiện cleanup tài nguyên: xóa bucket thử nghiệm, instance tạm, thu hồi access key và xóa snapshot không cần thiết.

* Soạn phần tổng kết: bài học chính, khó khăn gặp phải và hướng học tiếp (containerization, CI/CD, hardening).

* Bản giao nộp: IaC templates, sơ đồ kiến trúc và ghi chú demo (link lưu trong tài liệu dự án).


