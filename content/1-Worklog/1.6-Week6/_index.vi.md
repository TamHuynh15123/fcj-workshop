---
title: "Worklog Tuần 6"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Thiết lập AWS Amplify cho hosting frontend Coffee Cloud
* Tạo ứng dụng React.js frontend
* Cấu hình CI/CD pipeline để deploy tự động

### Nhiệm vụ thực hiện trong tuần:
| Ngày | Nhiệm vụ                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Tìm hiểu cơ bản AWS Amplify <br> - Hiểu Amplify hosting và CI/CD features <br> - Ôn tập React.js cơ bản cho phát triển frontend                                                        | 05/08/2025 | 05/08/2025      | Tài liệu Amplify                     |
| 2   | - Tạo ứng dụng React.js mới cho Coffee Cloud <br> - Thiết lập cấu trúc project với components cho: login, menu, cart, orders                                                                   | 06/08/2025 | 06/08/2025      | Tài liệu React.js                    |
| 3   | - Khởi tạo Git repository cho project <br> - Push code ban đầu lên GitHub repository <br> - Thiết lập routing và navigation cơ bản                                                                | 07/08/2025 | 07/08/2025      | Tài liệu Git                         |
| 4   | - Kết nối React app với AWS Amplify <br> - Cấu hình automatic deployment từ GitHub <br> - Thiết lập custom domain (nếu có)                                                                     | 08/08/2025 | 08/08/2025      | Hướng dẫn Amplify console                     |
| 5   | - Test CI/CD pipeline bằng cách thay đổi code <br> - Cấu hình environment variables cho API endpoints <br> - Xác minh deployment thành công                                                              | 09/08/2025 | 09/08/2025      | Hướng dẫn Amplify deployment                  |


### Kết quả đạt được tuần 6:

* Thành công tạo ứng dụng React.js frontend cho Coffee Cloud với các tính năng:
  * **Trang Login/Registration**: Giao diện xác thực người dùng
  * **Trang Menu**: Hiển thị sản phẩm cà phê với giá và mô tả
  * **Giỏ hàng**: Thêm/bỏ items và tính tổng tiền
  * **Lịch sử đơn hàng**: Xem đơn hàng cũ và theo dõi trạng thái
  * **Hệ thống điểm**: Hiển thị điểm thưởng khách hàng

* Thiết lập AWS Amplify hosting với CI/CD pipeline tự động:
  * Kết nối GitHub repository với Amplify
  * Cấu hình automatic deployment khi commit code
  * Thiết lập environment-specific builds (dev/prod)
  * Cấu hình custom domain sẵn sàng cho tương lai

* Implement responsive design cho người dùng mobile và desktop

* Thành công test toàn bộ deployment process:
  * Thay đổi code trigger automatic builds
  * Build logs cho thấy deployment thành công
  * Ứng dụng live có thể truy cập qua Amplify URL

* Cấu hình environment variables để kết nối API Gateway endpoints

* Tìm hiểu lợi ích của Amplify cho frontend developers:
  * Không cần cấu hình server
  * Quản lý SSL certificate tự động
  * Global CDN để phân phối nội dung nhanh
  * Dễ dàng rollback về version trước

* Đã tạo và bảo mật AWS Free Tier account: bật MFA và tạo IAM user ban đầu.

* Thành thạo thao tác cơ bản trên AWS Management Console.

* Cài đặt và cấu hình AWS CLI (access key, secret key, region mặc định, output format).

* Thực hiện một số lệnh CLI cơ bản:
  * aws sts get-caller-identity
  * aws ec2 describe-instances
  * aws s3 ls

* Khởi tạo EC2, kết nối SSH và gắn EBS volume để thực hành.

* Ghi chú: sẽ tiếp tục ôn tập S3 và IAM trong các tuần tới.


