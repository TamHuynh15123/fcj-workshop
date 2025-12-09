---
title: "Worklog Tuần 7"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Tích hợp React frontend với Lambda backend APIs
* Triển khai user authentication flow với Cognito
* Test các chức năng chính của Coffee Cloud

### Nhiệm vụ thực hiện trong tuần:
| Ngày | Nhiệm vụ                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Kết nối React frontend với API Gateway endpoints <br> - Cài đặt và cấu hình AWS SDK cho JavaScript <br> - Thiết lập API service layer trong React                                                      | 12/08/2025 | 12/08/2025      | Tài liệu AWS SDK                         |
| 2   | - Triển khai user login/registration flow <br> - Tích hợp Cognito authentication với React <br> - Test user session management                                                                      | 13/08/2025 | 13/08/2025      | Cognito JavaScript SDK                    |
| 3   | - Kết nối product listing với DynamoDB <br> - Triển khai shopping cart functionality <br> - Test add/remove items từ cart                                                                           | 14/08/2025 | 14/08/2025      | React state management                    |
| 4   | - Triển khai order creation flow <br> - Kết nối order processing với Lambda functions <br> - Test order placement và data storage                                                                      | 15/08/2025 | 15/08/2025      | Lambda integration                        |
| 5   | - Test points system functionality <br> - Triển khai order history display <br> - Test toàn bộ user journey từ registration đến order                                                              | 16/08/2025 | 16/08/2025      | End-to-end testing                        |


### Kết quả đạt được tuần 7:

* Thành công tích hợp React frontend với các dịch vụ AWS backend:
  * Cấu hình AWS SDK cho JavaScript trong ứng dụng React
  * Thiết lập API service layer để tách biệt mối quan tâm
  * Triển khai xử lý lỗi phù hợp cho API calls

* Hoàn thành tích hợp user authentication:
  * Người dùng có thể đăng ký tài khoản mới qua Cognito
  * Chức năng login/logout hoạt động đúng cách
  * Quản lý session với JWT tokens
  * Kiểm soát truy cập theo vai trò (Customer, Shipper, Admin)

* Triển khai các tính năng chính của Coffee Cloud:
  * **Hiển thị sản phẩm**: Menu cà phê tải từ DynamoDB
  * **Giỏ hàng**: Thêm/bỏ items với quản lý số lượng
  * **Xử lý đơn hàng**: Flow hoàn chỉnh từ cart đến database
  * **Hệ thống điểm**: Tính toán và hiển thị điểm tự động

* Hoàn thành end-to-end testing của user journey:
  * Đăng ký người dùng mới → Xác thực email → Đăng nhập → Duyệt menu → Thêm vào giỏ → Đặt hàng → Nhận điểm

* Sửa các vấn đề tích hợp và cải thiện trải nghiệm người dùng:
  * Loading states để feedback tốt hơn cho người dùng
  * Xác thực input ở cả frontend và backend
  * Thông báo lỗi phù hợp cho các thao tác thất bại


