---
title: "Worklog Tuần 7"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Tìm hiểu về IAM (Identity and Access Management) và các nguyên tắc bảo mật cơ bản.
* Thực hành S3: tạo bucket, bật versioning, lifecycle rule và hosting trang web tĩnh.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Ôn tập các khái niệm IAM và best practices; đọc hướng dẫn IAM của AWS; xác định các role cần thiết cho lab.                                                                                | 20/10/2025   | 20/10/2025      | AWS IAM docs                               |
| 3   | - Tạo IAM groups và users; gán AWS managed policies; viết policy tối thiểu cho CLI và kiểm tra bằng aws iam simulate-principal-policy.                                                         | 21/10/2025   | 21/10/2025      | IAM policy docs                             |
| 4   | - Tạo IAM role cho EC2 (assume-role) để cấp quyền S3 có giới hạn; gắn role vào instance profile để test.                                                                                     | 22/10/2025   | 22/10/2025      | IAM roles docs                              |
| 5   | - S3: tạo bucket với mã hoá SSE-S3, bật public access block; thực hành put/get object bằng CLI và console.                                                                                  | 23/10/2025   | 23/10/2025      | S3 docs                                     |
| 6   | - Bật versioning và lifecycle rule cho bucket; triển khai trang tĩnh lên S3, kiểm tra hosting và bucket policy; viết lại các bước và lưu note xử lý sự cố.                                    | 24/10/2025   | 24/10/2025      | S3 static hosting guide                     |


### Kết quả đạt được tuần 7:

* Hiểu và thực hành các khái niệm IAM: user, group, role, policy; áp dụng nguyên tắc least-privilege.

* Tạo IAM user, group và cấp quyền phù hợp; tạo access key để sử dụng CLI.

* Thực hành các thao tác S3: tạo bucket, upload object, bật versioning và thêm lifecycle rule.

* Triển khai trang web tĩnh trên S3, kiểm tra public access và cấu hình bucket policy phù hợp.

* Lưu lại các lệnh và policy mẫu để tái sử dụng ở các bài thực hành sau.


