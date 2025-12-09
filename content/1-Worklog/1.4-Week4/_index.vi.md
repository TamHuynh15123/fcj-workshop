---
title: "Worklog Tuần 4"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Thiết lập database DynamoDB cho dự án Coffee Cloud
* Tìm hiểu cơ bản về DynamoDB và tạo bảng cho dữ liệu người dùng và đơn hàng
* Thiết lập AWS Cognito cho xác thực người dùng

### Nhiệm vụ thực hiện trong tuần:
| Ngày | Nhiệm vụ                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Tìm hiểu cơ bản DynamoDB <br> - Hiểu khái niệm NoSQL, primary keys, và indexes                                                                                                                     | 22/07/2025 | 22/07/2025      | Tài liệu DynamoDB                         |
| 2   | - Tạo bảng DynamoDB cho Coffee Cloud: <br>&emsp; + Bảng Users <br>&emsp; + Bảng Products <br>&emsp; + Bảng Orders <br>&emsp; + Bảng Points                                                        | 23/07/2025 | 23/07/2025      | Hướng dẫn DynamoDB console                |
| 3   | - Cấu hình schema bảng và indexes <br> - Thêm dữ liệu mẫu để test <br> - Thực hành các thao tác CRUD cơ bản                                                                                        | 24/07/2025 | 24/07/2025      | Tài liệu DynamoDB SDK                     |
| 4   | - Tìm hiểu AWS Cognito cho xác thực người dùng <br> - Hiểu User Pools và Identity Pools                                                                                                              | 25/07/2025 | 25/07/2025      | Tài liệu Cognito                          |
| 5   | - Tạo Cognito User Pool cho Coffee Cloud <br> - Cấu hình thiết lập sign-up/sign-in <br> - Thiết lập user groups (Customer, Shipper, Admin)                                                        | 26/07/2025 | 26/07/2025      | Hướng dẫn Cognito console                 |

### Thành tích tuần 4:

* Thành công tạo các bảng DynamoDB cho dự án Coffee Cloud:
  * **Bảng Users**: Lưu thông tin customer, shipper, và admin
  * **Bảng Products**: Menu cà phê với giá cả và mô tả
  * **Bảng Orders**: Chi tiết đơn hàng và theo dõi trạng thái
  * **Bảng Points**: Hệ thống điểm thưởng khách hàng

* Cấu hình primary keys và secondary indexes phù hợp để query hiệu quả

* Thêm dữ liệu mẫu vào tất cả bảng để phục vụ testing

* Thành công thiết lập AWS Cognito User Pool với cấu hình:
  * Đăng nhập bằng email
  * Chính sách mật khẩu bảo mật
  * Ba user groups: Customer, Shipper, Admin
  * Xác thực email cho tài khoản mới

* Test các thao tác DynamoDB cơ bản sử dụng AWS console:
  * Thao tác tạo, đọc, cập nhật, xóa
  * Query và scan operations
  * Hiểu về capacity units và billing

* Học DynamoDB best practices để tối ưu chi phí trong giới hạn Free Tier


