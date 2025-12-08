---
title: "Setup Git Repository"
weight: 3
chapter: false
pre: " <b> 5.1.3 </b> "
---

# Thiết lập Git Repository

Trong bước này, chúng ta sẽ khởi tạo Git repository và push code lên GitHub.

## 1. Tạo GitHub Repository

### 1.1 Create New Repository

1. Click **+** (góc phải trên) → **New repository**
2. Điền thông tin:
   - **Repository name**: `Proposal-AWS---Coffe---FE`
   - **Visibility**: **Public**
3. Click **Create repository**

![Create GitHub Repo](/images/5-Workshop/5.1-amplify-frontend/create-github-repo.png)

---

## 4. Push code lên GitHub

### 4.1 Add remote repository

Copy URL từ GitHub (dạng: `https://github.com/your-username/coffee-cloud-frontend.git`)

```powershell
git remote add origin https://github.com/YOUR-USERNAME/coffee-cloud-frontend.git
```

### 4.2 Rename branch to main

```powershell
git branch -M main
```

### 4.3 Push code

```powershell
git push -u origin main
```

Nếu GitHub yêu cầu authentication:
- **Username**: GitHub username của bạn
- **Password**: Sử dụng **Personal Access Token** (PAT) đã tạo ở Prerequisites, KHÔNG phải password GitHub

{{% notice tip %}}
💡 **Tip**: Nếu bạn chưa tạo Personal Access Token, xem lại [Prerequisites section](../5.1.2-prerequisites/#22-generate-personal-access-token-pat)
{{% /notice %}}

---

## 5. Verify trên GitHub

1. Refresh trang GitHub repository
2. Bạn sẽ thấy tất cả file đã được push:
   - `src/`
   - `public/`
   - `package.json`
   - `vite.config.js`
   - etc.

![GitHub Files](/images/5-Workshop/5.1-amplify-frontend/github-files.png)

---

## 6. (Optional) Tạo README.md

Tạo file `README.md` trong root folder:

```markdown
# Coffee Cloud Frontend

Coffee Shop Order Platform built with ReactJS + AWS Amplify

## 🚀 Features
- Browse coffee menu
- Order management
- User authentication (Coming in Workshop 2)
- Real-time order tracking (Coming in Workshop 5)

## 🛠️ Tech Stack
- **Frontend**: React 18 + Vite
- **Styling**: Bootstrap 5
- **Routing**: React Router v6
- **Hosting**: AWS Amplify
- **CI/CD**: AWS Amplify Pipeline

## 📦 Installation

\```bash
npm install
\```

## 🏃 Run Locally

\```bash
npm run dev
\```

## 🔨 Build

\```bash
npm run build
\```

## 📄 License
MIT
```

Commit và push:

```powershell
git add README.md
git commit -m "Add README"
git push
```

---

## 7. Troubleshooting

### Issue 1: Git authentication failed

**Solution**: Sử dụng Personal Access Token thay vì password:
1. Tạo PAT: GitHub → Settings → Developer settings → Personal access tokens
2. Copy token
3. Khi push, dùng token làm password

### Issue 2: Permission denied

**Solution**: Check repository ownership và access rights:
```powershell
git remote -v  # Verify remote URL
```

### Issue 3: File too large

**Solution**: Đảm bảo `.gitignore` đã exclude `node_modules/` và `dist/`:
```powershell
git rm -r --cached node_modules
git commit -m "Remove node_modules"
```

---

## Next Steps

Tiếp tục với [Deploy to AWS Amplify](../5.1.5-deploy-amplify/) để deploy ứng dụng lên AWS.
