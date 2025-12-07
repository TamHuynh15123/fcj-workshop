---
title: "Worklog Tuần 6"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hoàn tất quy trình onboarding với nhóm First Cloud Journey và nắm rõ nội quy thực tập.
* Nắm kiến thức nền tảng về AWS: các nhóm dịch vụ chính, thiết lập tài khoản, sử dụng Console và AWS CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Họp onboarding với mentor và team; đọc các nội quy thực tập; thiết lập kênh giao tiếp (Slack/Email).                                                                                       | 13/10/2025   | 13/10/2025      | internal docs                              |
| 3   | - Nghiên cứu các nhóm dịch vụ AWS (Compute, Storage, Networking, Database); ghi chú và map use-case; xem lại tài liệu CloudJourney.                                                          | 14/10/2025   | 14/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo AWS Free Tier; bật MFA cho tài khoản root; tạo IAM admin user; cài & cấu hình AWS CLI; kiểm tra bằng lệnh aws sts get-caller-identity.                                                | 15/10/2025   | 15/10/2025      | AWS Console, AWS CLI docs                  |
| 5   | - Học các khái niệm EC2: AMI, instance type, EBS, key pair, security group. Chuẩn bị key-pair và security group cho SSH (port 22).                                                         | 16/10/2025   | 16/10/2025      | EC2 docs                                   |
| 6   | - Khởi tạo EC2 t2.micro, kết nối SSH, gắn thêm EBS volume, format & mount; tạo snapshot để luyện tập.                                                                                        | 17/10/2025   | 17/10/2025      | EC2/EBS docs                               |


### Kết quả đạt được tuần 6:

* Nắm được các nhóm dịch vụ chính của AWS và ứng dụng cơ bản:
  * Compute (EC2, Lambda)
  * Storage (S3, EBS)
  * Networking (VPC, Subnet)
  * Database (RDS, DynamoDB)

* Đã tạo và bảo mật AWS Free Tier account: bật MFA và tạo IAM user ban đầu.

* Thành thạo thao tác cơ bản trên AWS Management Console.

* Cài đặt và cấu hình AWS CLI (access key, secret key, region mặc định, output format).

* Thực hiện một số lệnh CLI cơ bản:
  * aws sts get-caller-identity
  * aws ec2 describe-instances
  * aws s3 ls

* Khởi tạo EC2, kết nối SSH và gắn EBS volume để thực hành.

* Ghi chú: sẽ tiếp tục ôn tập S3 và IAM trong các tuần tới.


