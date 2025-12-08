---
title: "Deploy to AWS Amplify"
weight: 4
chapter: false
pre: " <b> 5.1.4 </b> "
---

# Deploy lên AWS Amplify

Trong bước này, chúng ta sẽ kết nối GitHub repository với AWS Amplify và deploy ứng dụng.

## 1. Truy cập AWS Amplify Console

### 1.1 Đăng nhập AWS Console

1. Truy cập [https://console.aws.amazon.com](https://console.aws.amazon.com)
2. Đăng nhập với AWS Account
3. Chọn region: **US East (N. Virginia) us-east-1** (hoặc region bạn muốn)

### 1.2 Mở AWS Amplify

1. Trong search bar, gõ "**Amplify**"
2. Click **AWS Amplify**

![AWS Amplify Console](/images/5-Workshop/5.1-amplify-frontend/amplify-console.png)

---

## 2. Create New App

### 2.1 Start với Amplify Hosting

1. Click **Get Started** trong phần **Amplify Hosting**
2. Hoặc click **New app** → **Host web app**

![New App](/images/5-Workshop/5.1-amplify-frontend/new-app.png)

### 2.2 Chọn Git provider

1. Chọn **GitHub**
2. Click **Continue**

![Select GitHub](/images/5-Workshop/5.1-amplify-frontend/select-github.png)

### 2.3 Authorize GitHub

1. Click **Authorize AWS Amplify**
2. Đăng nhập GitHub nếu được yêu cầu
3. Grant permissions cho AWS Amplify

{{% notice info %}}
📝 **Note**: AWS Amplify cần quyền truy cập repository để pull code và setup webhooks
{{% /notice %}}

---

## 3. Add Repository

### 3.1 Select Repository

1. **Repository**: Chọn `coffee-cloud-frontend`
2. **Branch**: Chọn `main`
3. Click **Next**

![Select Repo](/images/5-Workshop/5.1-amplify-frontend/select-repo.png)

### 3.2 Configure Build Settings

AWS Amplify sẽ tự động detect build settings cho Vite project:

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - npm ci
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

{{% notice tip %}}
💡 **Tip**: Amplify tự động detect framework. Nếu không đúng, bạn có thể edit build settings sau
{{% /notice %}}

#### Verify settings:
- ✅ **App name**: `coffee-cloud-frontend` (tự động từ repo name)
- ✅ **Environment name**: `main` (từ branch name)
- ✅ **Build command**: `npm run build`
- ✅ **Build output directory**: `dist`

Click **Next**

---

## 4. Configure Advanced Settings (Optional)

### 4.1 Environment Variables

Hiện tại không cần, nhưng trong tương lai bạn có thể thêm:
- `VITE_API_URL`: URL của backend API
- `VITE_COGNITO_USER_POOL_ID`: ID của Cognito User Pool (Workshop 2)
- `VITE_COGNITO_CLIENT_ID`: Client ID của Cognito (Workshop 2)

Click **Next** để skip

### 4.2 Review

Review tất cả settings:
- Repository: `your-username/coffee-cloud-frontend`
- Branch: `main`
- Build command: `npm run build`
- Output directory: `dist`

Click **Save and deploy**

![Review Settings](/images/5-Workshop/5.1-amplify-frontend/review-settings.png)

---

## 5. Theo dõi Deployment Process

AWS Amplify sẽ bắt đầu deploy với 4 phases:

### 5.1 Provision
⏳ **Duration**: ~30 seconds
- Allocate resources
- Setup build environment

### 5.2 Build
⏳ **Duration**: ~2-3 minutes
- Pull code từ GitHub
- Run `npm ci` (install dependencies)
- Run `npm run build`
- Generate static files trong `dist/`

### 5.3 Deploy
⏳ **Duration**: ~30 seconds
- Upload build artifacts to CloudFront CDN
- Configure SSL certificate
- Setup domain

### 5.4 Verify
⏳ **Duration**: ~10 seconds
- Health check
- Verify deployment success

![Deployment Process](/images/5-Workshop/5.1-amplify-frontend/deployment-process.png)

---

## 6. Access Your App

### 6.1 Get URL

Sau khi deployment thành công:
1. Amplify sẽ hiển thị URL dạng: `https://main.xxxxxx.amplifyapp.com`
2. Click vào URL để mở ứng dụng

![App URL](/images/5-Workshop/5.1-amplify-frontend/app-url.png)

### 6.2 Test Application

Verify tất cả pages:
- ✅ Homepage (`/`)
- ✅ Menu page (`/menu`)
- ✅ Order page (`/order`)
- ✅ Login page (`/login`)
- ✅ Navigation works
- ✅ Responsive design on mobile

![Live App](/images/5-Workshop/5.1-amplify-frontend/live-app.png)

---

## 7. Setup CI/CD Auto-Deploy

### 7.1 Verify Webhook

AWS Amplify đã tự động setup webhook trong GitHub:

1. Vào GitHub repository → **Settings** → **Webhooks**
2. Bạn sẽ thấy webhook từ AWS Amplify

![GitHub Webhook](/images/5-Workshop/5.1-amplify-frontend/github-webhook.png)

### 7.2 Test Auto-Deploy

Let's test CI/CD pipeline:

1. Edit file `src/pages/Home.jsx` local
2. Change heading text:
```jsx
<h1 className="display-4">☕ Welcome to Coffee Cloud v2.0!</h1>
```

3. Commit và push:
```powershell
git add src/pages/Home.jsx
git commit -m "Update homepage heading"
git push
```

4. Quay lại **Amplify Console** → Bạn sẽ thấy build tự động trigger!
5. Sau ~3 minutes, refresh app URL → Thấy thay đổi!

🎉 **CI/CD đã hoạt động!**

---

## 8. View Build Logs

### 8.1 Access Logs

1. Trong Amplify Console, click vào **latest build**
2. Expand các phases để xem logs:
   - **Provision logs**: Resource allocation
   - **Build logs**: npm install + build output
   - **Deploy logs**: Upload to CDN
   - **Verify logs**: Health checks

### 8.2 Download Logs

Click **Download build logs** để save logs về máy

---

## 9. Configure Custom Domain (Optional)

### 9.1 Add Custom Domain

1. Trong Amplify Console, click **Domain management** (sidebar)
2. Click **Add domain**
3. Nhập domain của bạn (ví dụ: `coffeecloud.com`)
4. Follow instructions để:
   - Add CNAME record to DNS
   - Verify domain ownership
   - Wait for SSL certificate (15-30 minutes)

{{% notice warning %}}
⚠️ **Note**: Custom domain yêu cầu bạn đã sở hữu domain. Nếu chưa có, skip bước này.
{{% /notice %}}

---

## 10. Monitoring & Metrics

### 10.1 View Analytics

1. Trong Amplify Console, click **Analytics** (sidebar)
2. Xem:
   - **Requests**: Số lượng requests
   - **Data transferred**: Bandwidth usage
   - **Build minutes**: CI/CD usage
   - **Errors**: 404, 500 errors

### 10.2 Setup Alarms (Optional)

1. Click **Alarms** → **Create alarm**
2. Configure threshold (ví dụ: Build failed > 2 times)
3. Add email notification

---

## 11. Troubleshooting

### Issue 1: Build Failed - "npm: command not found"

**Solution**: Update build settings:
```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - nvm use 18  # Specify Node version
        - npm ci
```

### Issue 2: "Module not found" error

**Solution**: Clear cache và rebuild:
1. Amplify Console → **App settings** → **Build settings**
2. Clear cache
3. Redeploy

### Issue 3: 404 on route refresh

**Solution**: Add redirects for SPA:
1. Click **Rewrites and redirects**
2. Add rule:
   - Source: `</^[^.]+$|\.(?!(css|gif|ico|jpg|js|png|txt|svg|woff|ttf)$)([^.]+$)/>`
   - Target: `/index.html`
   - Type: `200 (Rewrite)`

![SPA Redirect](/images/5-Workshop/5.1-amplify-frontend/spa-redirect.png)

---

## Next Steps

Tiếp tục với [Configure Build Settings](../5.1.6-configure-build/) để tối ưu hóa build process.
