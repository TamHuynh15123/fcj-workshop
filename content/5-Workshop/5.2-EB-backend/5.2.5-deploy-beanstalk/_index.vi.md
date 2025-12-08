---
title: "Triển khai lên Elastic Beanstalk"
weight: 5
chapter: false
pre: " <b> 5.2.5 </b> "
---

# Triển khai lên AWS Elastic Beanstalk

Bây giờ hãy triển khai .NET API của bạn lên Elastic Beanstalk sử dụng AWS Console.

#### Bước 1: Truy cập Elastic Beanstalk Console

1. Đăng nhập vào [AWS Console](https://console.aws.amazon.com/)
2. Tìm **"Elastic Beanstalk"** trong thanh tìm kiếm phía trên
3. Click **Elastic Beanstalk** service

#### Bước 2: Tạo Application Mới

1. Click nút **"Create Application"**
2. Điền thông tin application:

**Application information:**
- **Application name:** `CoffeeCloudAPI`
- **Application tags (tùy chọn):** 
  - Key: `Project`, Value: `CoffeeCloud`
  - Key: `Environment`, Value: `Production`

#### Bước 3: Cấu hình Environment

**Environment information:**
- **Environment name:** `coffeecloud-api-env` (hoặc tên bạn muốn)
- **Domain:** Tự động tạo (như `coffeecloud-api-env.ap-southeast-1.elasticbeanstalk.com`)
  - Kiểm tra tính khả dụng
  - Đây sẽ là URL API của bạn!

**Platform:**
- **Platform:** `.NET on Windows Server`
- **Platform branch:** `.NET 8 running on 64bit Windows Server 2022`
- **Platform version:** Latest (Khuyến nghị)

#### Bước 4: Upload Application Code

**Application code:**
- Chọn **"Upload your code"**
- **Version label:** `v1.0.0` (hoặc ngày hiện tại như `2025-12-08`)
- **Source code origin:** Choose file
- Click **"Choose file"** và chọn file `CoffeeCloudAPI.zip` của bạn

⚠️ **Quan trọng:** Đảm bảo bạn upload file ZIP, không phải thư mục!

#### Bước 5: Cấu hình Service Access

**Service role:**
- Nếu lần đầu: Click **"Create and use new service role"**
- Role name: `aws-elasticbeanstalk-service-role` (tự động tạo)

**EC2 key pair (tùy chọn):**
- Chọn existing hoặc bỏ qua (không cần cho deployment cơ bản)

**EC2 instance profile:**
- Nếu lần đầu: Click **"Create new instance profile"**
- Dùng: `aws-elasticbeanstalk-ec2-role`

#### Bước 6: Thiết lập Networking (Tùy chọn)

**Virtual Private Cloud (VPC):**
- Dùng default VPC (khuyến nghị cho testing)

**Public IP address:**
- ✅ Activate (cần thiết cho truy cập internet)

Bỏ qua các tùy chọn networking khác.

#### Bước 7: Cấu hình Instance

**Instance types:**
- Chọn: `t2.micro` (Đủ điều kiện Free Tier!)
- Xóa các instance types khác

**Root volume:**
- Type: `General Purpose (SSD)`
- Size: `10 GB` (mặc định)

#### Bước 8: Cấu hình Auto-Scaling

**Environment type:**
- Chọn: **Load balanced** (cho production với auto-scaling)
- HOẶC **Single instance** (rẻ hơn cho testing, không có load balancer)

**Cho Load Balanced (Khuyến nghị):**
- **Instances:**
  - Min: `1`
  - Max: `4`
- **Scaling triggers:**
  - Metric: `CPUUtilization`
  - Upper threshold: `80`
  - Lower threshold: `20`

**Cho Single Instance (Free Tier):**
- Chỉ 1 instance, không scaling
- Tốt cho testing/development

#### Bước 9: Cấu hình Health Monitoring

**Health reporting:**
- System: `Enhanced` (khuyến nghị)

**Health check path:**
- Path: `/api/health`
- Timeout: `5` giây
- Interval: `30` giây

Sử dụng HealthController chúng ta đã tạo!

#### Bước 10: Cấu hình Environment Properties

Cuộn xuống phần **Environment properties** và thêm:

| Name | Value |
|------|-------|
| `ASPNETCORE_ENVIRONMENT` | `Production` |
| `ASPNETCORE_URLS` | `http://+:5000` |

Tùy chọn - cho CORS (nếu kết nối với frontend cụ thể):
| Name | Value |
|------|-------|
| `AllowedOrigins` | `https://your-app.amplifyapp.com` |

#### Bước 11: Review và Create

1. Review tất cả cài đặt
2. Click **"Submit"**
3. Đợi environment được tạo (5-10 phút)

Bạn sẽ thấy:
- 🔄 **Creating environment** (vàng)
- 🔄 **Launching instances**
- 🔄 **Running deployment**
- ✅ **Environment created successfully** (xanh)

#### Bước 12: Lấy API URL

Sau khi deployment hoàn tất:

1. Bạn sẽ thấy domain ở phía trên:
   ```
   http://coffeecloud-api-env.ap-southeast-1.elasticbeanstalk.com
   ```

2. **Test Swagger UI:**
   ```
   http://coffeecloud-api-env.ap-southeast-1.elasticbeanstalk.com/swagger
   ```

**Định dạng domain ví dụ:**
```
http://[environment-name].[region].elasticbeanstalk.com
http://fixenv-env.eba-vgperhwx.ap-southeast-1.elasticbeanstalk.com
```

#### Bước 13: Xác minh Deployment

Click vào URL environment và test:

1. **Health Check:**
   ```
   http://your-domain.elasticbeanstalk.com/api/health
   ```
   Nên trả về:
   ```json
   {
     "status": "Healthy",
     "timestamp": "2025-12-08T10:30:00Z",
     "version": "1.0.0",
     "service": "Coffee Cloud API"
   }
   ```

2. **Swagger UI:**
   ```
   http://your-domain.elasticbeanstalk.com/swagger
   ```
   Nên hiển thị tài liệu API tương tác

3. **Menu API:**
   ```
   http://your-domain.elasticbeanstalk.com/api/menu
   ```
   Nên trả về JSON menu items

#### Bước 14: Cấu hình CORS cho Amplify

Nếu cần kết nối với Amplify frontend, cập nhật CORS:

1. Vào tab **Configuration**
2. Click **Software** → **Edit**
3. Thêm environment property:
   - Name: `AllowedOrigins`
   - Value: `https://your-app.amplifyapp.com,https://dev.your-app.amplifyapp.com`
4. Click **Apply**

#### Các Vấn đề Thường gặp

**Vấn đề: Environment health màu đỏ/degraded**
- Kiểm tra CloudWatch Logs: Configuration → Software → View logs
- Xác minh phiên bản .NET 8.0 SDK
- Kiểm tra `web.config` có trong ZIP không

**Vấn đề: 502 Bad Gateway**
- Application không khởi động
- Kiểm tra logs cho .NET errors
- Xác minh tất cả dependencies có đủ

**Vấn đề: Không truy cập được /swagger**
- Kiểm tra Swagger có bật trong production không
- Xác minh app chạy đúng port (5000)
- Kiểm tra security group cho phép HTTP traffic

#### API của bạn đã Live! 🚀

Bây giờ bạn có:
- ✅ Live API tại: `http://[your-env].elasticbeanstalk.com`
- ✅ Swagger UI tại: `http://[your-env].elasticbeanstalk.com/swagger`
- ✅ Auto-scaling đã cấu hình
- ✅ Health monitoring đang hoạt động
- ✅ CloudWatch logging đã bật

**Tiếp theo:** Hãy test tất cả API endpoints với Swagger! →

