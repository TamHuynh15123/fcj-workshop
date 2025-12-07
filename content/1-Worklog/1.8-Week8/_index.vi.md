---
title: "Worklog Tuần 8"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Tìm hiểu mạng lưới AWS: VPC, subnet, route table, Internet Gateway, NAT, Security Group và NACL.
* Triển khai tài nguyên trong VPC và thực hành mẫu kết nối an toàn (bastion host).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Lên kế hoạch CIDR và sơ đồ subnet (public/private); ghi chú lý do chọn CIDR.                                                                                                              | 27/10/2025   | 27/10/2025      | VPC docs                                    |
| 3   | - Tạo VPC với public và private subnets; cấu hình route table và gắn Internet Gateway cho public subnet.                                                                                    | 28/10/2025   | 28/10/2025      | VPC guide                                   |
| 4   | - Thiết lập private subnet và NAT Gateway (hoặc NAT instance); kiểm tra kết nối outbound từ instances trong private subnet.                                                                 | 29/10/2025   | 29/10/2025      | NAT docs                                    |
| 5   | - Thiết kế và áp dụng Security Groups & Network ACLs; tạo rule chỉ mở traffic cần thiết (SSH qua bastion, HTTP/HTTPS, port DB).                                                            | 30/10/2025   | 30/10/2025      | Security groups docs                        |
| 6   | - Triển khai bastion host trên public subnet; thử SSH proxy tới private EC2; vẽ sơ đồ mạng và ghi lại note debug.                                                                           | 31/10/2025   | 31/10/2025      | VPC/SSH best practices                      |


### Kết quả đạt được tuần 8:

* Thiết kế và tạo VPC gồm public và private subnets, cấu hình route table và Internet Gateway.

* Khởi tạo EC2 trong public/private subnet và kiểm tra kết nối qua bastion host/SSH proxy.

* Cấu hình Security Groups và Network ACLs để giới hạn lưu lượng theo nguyên tắc least-privilege.

* Áp dụng NAT gateway để cho phép instances trong private subnet truy cập internet khi cần.

* Lưu lại sơ đồ VPC và các lệnh kiểm tra mạng (traceroute, curl) phục vụ việc debug.


