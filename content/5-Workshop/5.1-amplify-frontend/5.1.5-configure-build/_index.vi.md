---
title: "Cấu hình Build Settings"
weight: 5
chapter: false
pre: " <b> 5.1.5 </b> "
---

# Cấu hình Build Settings

Trong bước này, chúng ta sẽ tối ưu hóa build settings cho performance và cost.

## 1. Truy cập Build Settings

1. Amplify Console → **App settings** → **Build settings**
2. Click **Edit**

## 2. Tối ưu hóa Build Configuration

### 2.1 Cập nhật amplify.yml

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        # Sử dụng Node 18 LTS
        - nvm use 18
        # Cài đặt dependencies (nhanh hơn npm install)
        - npm ci
    build:
      commands:
        # Production build
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

## 3. Environment Variables

### 3.1 Thêm Variables

Click **Environment variables** → **Manage variables** → **Add variable**:

| Key | Value | Ghi chú |
|-----|-------|---------|
| `NODE_ENV` | `production` | Build mode |
| `VITE_APP_NAME` | `Coffee Cloud` | Tên app |
| `VITE_VERSION` | `1.0.0` | Phiên bản |

{{% notice tip %}}
💡 **Mẹo**: Variables có prefix `VITE_` sẽ được expose trong React app
{{% /notice %}}

## 4. Bật Build Optimizations

### 4.1 Bật Cache
- ✅ **Cache dependencies**: Tiết kiệm ~1 phút mỗi build
- ✅ **Reuse build artifacts**: Deploy nhanh hơn

### 4.2 Concurrent Builds
- **Giới hạn**: 1 (Free Tier mặc định)
- Nâng cấp plan để tăng giới hạn nếu cần

## 5. Cấu hình Redirects cho SPA

1. Click **Rewrites and redirects**
2. Thêm rule cho React Router:

| Source | Target | Type |
|--------|--------|------|
| `</^[^.]+$\|\.(?!(css\|gif\|ico\|jpg\|js\|png\|txt\|svg\|woff\|ttf)$)([^.]+$)/>` | `/index.html` | `200 (Rewrite)` |

Click **Save**

## 6. Custom Headers (Tùy chọn)

Thêm security headers:

```yaml
customHeaders:
  - pattern: '**/*'
    headers:
      - key: 'Strict-Transport-Security'
        value: 'max-age=31536000; includeSubDomains'
      - key: 'X-Frame-Options'
        value: 'SAMEORIGIN'
      - key: 'X-Content-Type-Options'
        value: 'nosniff'
```

## 7. Kiểm tra Build

1. Click **Redeploy this version**
2. Theo dõi build logs
3. Xác minh chức năng app

## Bước tiếp theo

Tiếp tục với [Kiểm tra và xác minh](../5.1.6-testing/)
