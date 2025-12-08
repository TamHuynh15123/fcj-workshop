---
title: "Workshop Overview"
weight: 1
chapter: false
pre: " <b> 5.1.1 </b> "
---

# Workshop Overview

#### Mục tiêu Workshop

Sau khi hoàn thành workshop này, bạn sẽ có thể:
- ✅ Tạo ứng dụng ReactJS từ đầu
- ✅ Setup Git repository và push code lên GitHub
- ✅ Kết nối GitHub repository với AWS Amplify
- ✅ Deploy ứng dụng với CI/CD tự động
- ✅ Truy cập ứng dụng qua HTTPS URL
- ✅ Hiểu về build process và environment variables

#### Coffee Cloud Frontend - Tính năng cơ bản

Trong workshop này, chúng ta sẽ tạo giao diện cơ bản cho Coffee Cloud Platform bao gồm:
- 🏠 **Homepage**: Giới thiệu về Coffee Cloud
- 📋 **Menu Page**: Danh sách sản phẩm coffee
- 👤 **Login Page**: Trang đăng nhập (sẽ tích hợp Cognito ở Workshop 2)

#### Công nghệ sử dụng

- **Frontend Framework**: ReactJS 
- **Build Tool**: Create React App
- **Version Control**: Git + GitHub
- **Hosting**: AWS Amplify
- **CDN**: CloudFront (tự động từ Amplify)

#### Kiến trúc triển khai

```
┌─────────────────┐
│  Developer      │
│  (Your Laptop)  │
└────────┬────────┘
         │ git push
         ▼
┌─────────────────┐
│  GitHub         │
│  Repository     │
└────────┬────────┘
         │ webhook trigger
         ▼
┌─────────────────┐
│  AWS Amplify    │
│  - Build        │
│  - Deploy       │
└────────┬────────┘
         │ distribute
         ▼
┌─────────────────┐
│  CloudFront CDN │
│  (Global)       │
└────────┬────────┘
         │ HTTPS
         ▼
┌─────────────────┐
│  End Users      │
└─────────────────┘
```

#### Quy trình CI/CD tự động

1. Developer push code lên GitHub
2. GitHub webhook trigger AWS Amplify build
3. Amplify tự động:
   - Pull code từ GitHub
   - Chạy `npm install`
   - Chạy `npm run build`
   - Deploy build artifacts lên CloudFront CDN
4. Website tự động cập nhật (2-3 phút)

#### Chi phí dự kiến

Với **AWS Free Tier**, workshop này **hoàn toàn miễn phí**:
- ✅ 1000 build minutes/month (Free Tier)
- ✅ 15GB storage (Free Tier)
- ✅ 15GB data transfer out (Free Tier)

Sau khi hết Free Tier:
- Build: ~$0.01/minute
- Hosting: ~$0.15/GB stored/month
- Data transfer: ~$0.15/GB served

**Estimated cost**: Dưới $1/month cho traffic nhỏ


{{% notice tip %}}
💡 **Tip:** Nên tạo Git repository trước khi bắt đầu code để có thể commit thường xuyên
{{% /notice %}}

#### Next Steps

Bắt đầu với [Prerequisites](../5.1.2-prerequisites/) để chuẩn bị môi trường làm việc.
