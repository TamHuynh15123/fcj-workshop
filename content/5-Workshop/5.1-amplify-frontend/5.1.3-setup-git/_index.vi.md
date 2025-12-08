---
title: "Thiết lập Git Repository"
weight: 3
chapter: false
pre: " <b> 5.1.3 </b> "
---

# Thiết lập Git Repository

Trong bước này, chúng ta sẽ khởi tạo Git repository và push code lên GitHub.

## 1. Khởi tạo Git Repository

### 1.1 Khởi tạo Git

Trong thư mục `coffee-cloud-frontend`:

```powershell
git init
```

### 1.2 Tạo .gitignore

File `.gitignore` đã được tạo tự động bởi Vite. Kiểm tra nội dung:

```powershell
cat .gitignore
```

Đảm bảo file có các dòng sau:

```
# Logs
logs
*.log
npm-debug.log*

# Dependencies
/node_modules

# Production build
/dist
/build

# Misc
.DS_Store
*.pem

# Environment variables
.env
.env.local
.env.*.local

# IDE
.vscode/
.idea/
```

---

## 2. Commit đầu tiên

### 2.1 Thêm files

```powershell
git add .
```

### 2.2 Commit

```powershell
git commit -m "Initial commit: Coffee Cloud frontend with React + Vite"
```

---

## 3. Tạo GitHub Repository

### 3.1 Đăng nhập GitHub

1. Truy cập [https://github.com](https://github.com)
2. Đăng nhập vào tài khoản của bạn

### 3.2 Tạo Repository mới

1. Click **+** (góc phải trên) → **New repository**
2. Điền thông tin:
   - **Repository name**: `coffee-cloud-frontend`
   - **Description**: `Coffee Cloud Platform - ReactJS Frontend`
   - **Visibility**: **Public** (hoặc Private nếu muốn)
   - **⚠️ KHÔNG chọn**: "Initialize with README" (vì đã có code local)
3. Click **Create repository**

![Create GitHub Repo](/images/5-Workshop/5.1-amplify-frontend/create-github-repo.png)

---

## 4. Push code lên GitHub

### 4.1 Thêm remote repository

Copy URL từ GitHub (dạng: `https://github.com/your-username/coffee-cloud-frontend.git`)

```powershell
git remote add origin https://github.com/TEN-BAN/coffee-cloud-frontend.git
```

### 4.2 Đổi tên branch sang main

```powershell
git branch -M main
```

### 4.3 Push code

```powershell
git push -u origin main
```

Nếu GitHub yêu cầu xác thực:
- **Username**: Tên người dùng GitHub của bạn
- **Password**: Sử dụng **Personal Access Token** (PAT) đã tạo ở Prerequisites, KHÔNG phải mật khẩu GitHub

{{% notice tip %}}
💡 **Mẹo**: Nếu bạn chưa tạo Personal Access Token, xem lại [phần Prerequisites](../5.1.2-prerequisites/#22-tạo-personal-access-token-pat)
{{% /notice %}}

---

## 5. Kiểm tra trên GitHub

1. Làm mới trang GitHub repository
2. Bạn sẽ thấy tất cả file đã được push:
   - `src/`
   - `public/`
   - `package.json`
   - `vite.config.js`
   - etc.

![GitHub Files](/images/5-Workshop/5.1-amplify-frontend/github-files.png)

---

## 6. (Tùy chọn) Tạo README.md

Tạo file `README.md` trong thư mục gốc:

```markdown
# Coffee Cloud Frontend

Nền tảng đặt hàng Coffee Shop xây dựng với ReactJS + AWS Amplify

## 🚀 Tính năng
- Xem thực đơn coffee
- Quản lý đơn hàng
- Xác thực người dùng (Sắp có ở Workshop 2)
- Theo dõi đơn hàng thời gian thực (Sắp có ở Workshop 5)

## 🛠️ Công nghệ
- **Frontend**: React 18 + Vite
- **Styling**: Bootstrap 5
- **Routing**: React Router v6
- **Hosting**: AWS Amplify
- **CI/CD**: AWS Amplify Pipeline

## 📦 Cài đặt

\```bash
npm install
\```

## 🏃 Chạy Local

\```bash
npm run dev
\```

## 🔨 Build

\```bash
npm run build
\```

## 📄 Giấy phép
MIT
```

Commit và push:

```powershell
git add README.md
git commit -m "Add README"
git push
```

---

## 7. Xử lý sự cố

### Vấn đề 1: Git authentication failed

**Giải pháp**: Sử dụng Personal Access Token thay vì mật khẩu:
1. Tạo PAT: GitHub → Settings → Developer settings → Personal access tokens
2. Copy token
3. Khi push, dùng token làm mật khẩu

### Vấn đề 2: Permission denied

**Giải pháp**: Kiểm tra quyền sở hữu repository và quyền truy cập:
```powershell
git remote -v  # Kiểm tra remote URL
```

### Vấn đề 3: File quá lớn

**Giải pháp**: Đảm bảo `.gitignore` đã loại trừ `node_modules/` và `dist/`:
```powershell
git rm -r --cached node_modules
git commit -m "Remove node_modules"
```

---

## Bước tiếp theo

Tiếp tục với [Deploy lên AWS Amplify](../5.1.5-deploy-amplify/) để deploy ứng dụng lên AWS.
