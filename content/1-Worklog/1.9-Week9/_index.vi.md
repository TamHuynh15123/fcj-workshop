---
title: "Worklog Tuần 9"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Tối ưu hiệu suất và bảo mật ứng dụng Coffee Cloud
* Thiết lập monitoring và logging cho ứng dụng
* Chuẩn bị cho việc triển khai production

### Nhiệm vụ thực hiện trong tuần:
| Ngày | Nhiệm vụ                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Tối ưu DynamoDB tables để hiệu suất tốt hơn <br> - Thiết lập indexes phù hợp cho các queries thường dùng <br> - Review và tối ưu hiệu suất Lambda function                              | 26/08/2025 | 26/08/2025      | Hướng dẫn tối ưu DynamoDB               |
| 2   | - Thiết lập CloudWatch monitoring cho tất cả services <br> - Tạo custom metrics cho business KPIs <br> - Cấu hình log groups cho Lambda functions                                                      | 27/08/2025 | 27/08/2025      | Tài liệu CloudWatch                  |
| 3   | - Triển khai IAM roles và policies phù hợp <br> - Tuân theo nguyên tắc least privilege <br> - Xoá các quyền không cần thiết                                                               | 28/08/2025 | 28/08/2025      | IAM best practices                        |
| 4   | - Thiết lập CloudWatch dashboards <br> - Monitor application health và performance <br> - Tạo alarms cho các metrics quan trọng                                                          | 29/08/2025 | 29/08/2025      | CloudWatch dashboards                     |
| 5   | - Tiến hành testing kỹ lưỡng tất cả tính năng <br> - Test các error scenarios và edge cases <br> - Tài liệu hóa các vấn đề đã biết và giới hạn                                                                  | 30/08/2025 | 30/08/2025      | Hướng dẫn Application testing                 |


### Kết quả đạt được tuần 9:

* Tối ưu hiệu suất ứng dụng Coffee Cloud:
  * **Tối ưu DynamoDB**: Thêm Global Secondary Indexes (GSI) để queries hiệu quả theo user ID và order status
  * **Hiệu suất Lambda**: Tối ưu function code và giảm cold start times
  * **Chiến lược Caching**: Triển khai caching cơ bản cho product data thường truy cập

* Thiết lập monitoring và logging toàn diện:
  * **CloudWatch Metrics**: Custom metrics cho orders per hour, user registrations, và error rates
  * **Log Analysis**: Centralized logging cho tất cả Lambda functions với structured log format
  * **Performance Monitoring**: Theo dõi API response times và database query performance

* Nâng cao tình bảo mật:
  * **IAM Optimization**: Tạo roles cụ thể cho từng service với quyền tối thiểu cần thiết
  * **Security Review**: Xoá các policies quá rộng rãi và cứng cố access controls
  * **Secrets Management**: Chuyển các cấu hình nhạy cảm sang environment variables

* Tạo operational dashboards:
  * **Business Metrics Dashboard**: View real-time đơn hàng, doanh thu, và hoạt động người dùng
  * **Technical Health Dashboard**: Hiệu suất hệ thống, error rates, và service availability
  * **Cost Monitoring Dashboard**: Theo dõi AWS resource usage và chi phí

* Hoàn thành comprehensive testing:
  * **Functional Testing**: Xác minh tất cả user flows hoạt động đúng
  * **Error Handling**: Test hành vi hệ thống dưới các failure scenarios
  * **Load Testing**: Testing cơ bản hiệu suất hệ thống dưới simulated load
  * **Security Testing**: Xác minh authentication và authorization hoạt động đúng

* Tài liệu hóa application architecture và deployment process cho việc bảo trì tương lai

* Đánh giá các lựa chọn sao lưu, bao gồm cross-region copy và chi phí liên quan.

* Ghi chú: tiếp tục cấu hình giám sát và cảnh báo cho DB bằng CloudWatch.


