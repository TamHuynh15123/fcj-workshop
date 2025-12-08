---
title: "Yêu cầu trước khi bắt đầu"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Yêu cầu trước khi bắt đầu

Trước khi bắt đầu workshop này, hãy đảm bảo bạn đã có các công cụ và tài khoản sau.

#### 1. Tài khoản AWS

Bạn cần tài khoản AWS với quyền tạo:
- ✅ Elastic Beanstalk applications và environments
- ✅ EC2 instances (t2.micro cho free tier)
- ✅ Application Load Balancers
- ✅ DynamoDB tables
- ✅ IAM roles và policies
- ✅ CloudWatch logs

**Chi phí:** Nếu sử dụng Free Tier, workshop này sẽ tốn **$0-2** cho việc testing.

[Tạo tài khoản AWS](https://aws.amazon.com/free/) nếu bạn chưa có.

#### 2. Công cụ Phát triển

##### .NET 8.0 SDK
Cần thiết để xây dựng Web API.

**Windows:**
```powershell
# Download và cài đặt từ Microsoft
winget install Microsoft.DotNet.SDK.8
```

**Xác minh cài đặt:**
```bash
dotnet --version
# Nên hiện: 8.0.x
```

[Tải .NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

##### Docker Desktop
Cần thiết để container hóa ứng dụng.

**Windows/Mac:**
- Tải và cài đặt [Docker Desktop](https://www.docker.com/products/docker-desktop)
- Khởi động Docker Desktop
- Bật WSL2 backend (Windows)

**Xác minh cài đặt:**
```bash
docker --version
# Nên hiện: Docker version 24.x.x

docker run hello-world
# Nên pull và chạy thành công
```

##### AWS CLI
Cần thiết để tương tác với các dịch vụ AWS.

**Windows:**
```powershell
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```

**Mac:**
```bash
brew install awscli
```

**Cấu hình AWS CLI:**
```bash
aws configure
# AWS Access Key ID: [Your Key]
# AWS Secret Access Key: [Your Secret]
# Default region: us-east-1
# Default output format: json
```

**Xác minh:**
```bash
aws --version
# Nên hiện: aws-cli/2.x.x

aws sts get-caller-identity
# Nên hiện thông tin tài khoản AWS của bạn
```

[Hướng dẫn cài đặt AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

##### Elastic Beanstalk CLI (Tùy chọn nhưng Khuyến nghị)
Đơn giản hóa quá trình triển khai.

**Cài đặt:**
```bash
pip install awsebcli --upgrade --user
```

**Xác minh:**
```bash
eb --version
# Nên hiện: EB CLI 3.x.x
```

#### 3. Code Editor

**Visual Studio Code** (Khuyến nghị)
- Tải từ [code.visualstudio.com](https://code.visualstudio.com/)

**Extensions khuyến nghị:**
- C# Dev Kit
- Docker
- AWS Toolkit
- REST Client (để test API)

**HOẶC Visual Studio 2022** (Thay thế)
- Tải từ [visualstudio.microsoft.com](https://visualstudio.microsoft.com/)
- Chọn workload "ASP.NET and web development"

#### 4. Workshop trước đó

⚠️ **Bắt buộc:** Bạn phải hoàn thành **Workshop 1: Deploy Frontend với Amplify**

Tại sao? Bởi vì:
- Frontend của bạn cần kết nối với backend API này
- Bạn cần Amplify URL cho cấu hình CORS
- Hiểu frontend giúp thiết kế API endpoints phù hợp

Nếu bạn chưa hoàn thành Workshop 1, hãy quay lại và hoàn thành nó trước:
→ [Workshop 5.1: Deploy Frontend với Amplify](../5.1-amplify-frontend/)

#### 5. Yêu cầu Kiến thức

**Phải có:**
- ✅ Lập trình C# cơ bản
- ✅ Hiểu về REST APIs (GET, POST, PUT, DELETE)
- ✅ Sử dụng command line cơ bản
- ✅ Git cơ bản (clone, commit, push)

**Nên có:**
- 🔸 Khái niệm Docker (images, containers)
- 🔸 AWS cơ bản (EC2, Load Balancers)
- 🔸 Định dạng dữ liệu JSON
- 🔸 HTTP status codes (200, 400, 500, v.v.)

**Không cần lo nếu bạn mới với:**
- Elastic Beanstalk (chúng tôi sẽ hướng dẫn từng bước)
- DynamoDB (chúng tôi sẽ dùng các thao tác đơn giản)
- Cấu hình Auto-scaling
- Thiết lập Load balancer

#### 6. Yêu cầu Hệ thống

**Tối thiểu:**
- OS: Windows 10/11, macOS 10.15+, hoặc Linux
- RAM: 8 GB
- Disk Space: 10 GB trống
- Internet: Kết nối ổn định để tải

**Khuyến nghị:**
- RAM: 16 GB (để chạy Docker + IDE)
- Disk Space: 20 GB trống
- CPU: 4+ cores

#### 7. Checklist Chuẩn bị

Trước khi tiếp tục, kiểm tra từng mục:

```
□ Đã tạo và truy cập được tài khoản AWS
□ Đã cài .NET 8.0 SDK (dotnet --version hoạt động)
□ Đã cài và chạy Docker Desktop
□ Đã cài và cấu hình AWS CLI
□ Đã cài code editor (VS Code hoặc Visual Studio)
□ Đã hoàn thành Workshop 1 (Frontend trên Amplify)
□ Đã cài Git (git --version hoạt động)
□ Có ít nhất 2 giờ không bị gián đoạn
```

#### 8. Xem trước Cấu trúc Project

Đây là những gì chúng ta sẽ xây dựng:

```
CoffeeCloudAPI/
├── Controllers/
│   ├── MenuController.cs
│   ├── OrderController.cs
│   └── HealthController.cs
├── Models/
│   ├── MenuItem.cs
│   ├── Order.cs
│   └── OrderItem.cs
├── Services/
│   ├── IMenuService.cs
│   ├── MenuService.cs
│   ├── IOrderService.cs
│   └── OrderService.cs
├── Program.cs
├── appsettings.json
├── Dockerfile
└── .ebignore
```

#### 9. Nhắc nhở về Chi phí

**Free Tier Coverage (12 tháng đầu):**
- EC2: 750 giờ/tháng t2.micro
- ELB: 750 giờ/tháng + 15 GB data
- DynamoDB: 25 GB storage + 25 WCU/RCU

**Điều này có nghĩa là:**
- Nếu dùng 1 EC2 instance 24/7: **MIỄN PHÍ**
- Nếu dùng 2 EC2 instances 24/7: **$8-16/tháng** (1 miễn phí, 1 trả tiền)

**Cho Workshop này:**
Chúng ta sẽ cấu hình để ở trong free tier trong quá trình phát triển, sau đó bạn có thể mở rộng cho production.

#### Sẵn sàng?

✅ Đã cài và cấu hình tất cả prerequisites?  
✅ Đã hoàn thành Workshop 1?  
✅ Có 2+ giờ rảnh?  

Tuyệt! Hãy tạo .NET API! →

