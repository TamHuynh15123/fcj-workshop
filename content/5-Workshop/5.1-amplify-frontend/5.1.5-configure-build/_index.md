---
title: "Configure Build Settings"
weight: 5
chapter: false
pre: " <b> 5.1.5 </b> "
---

# Cấu hình Build Settings

Trong bước này, chúng ta sẽ tối ưu hóa build settings cho performance và cost.

## 1. Access Build Settings

1. Amplify Console → **App settings** → **Build settings**
2. Click **Edit**

## 2. Optimize Build Configuration

### 2.1 Update amplify.yml

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        # Use Node 18 LTS
        - nvm use 18
        # Install dependencies (faster than npm install)
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

### 3.1 Add Variables

Click **Environment variables** → **Manage variables** → **Add variable**:

| Key | Value | Notes |
|-----|-------|-------|
| `NODE_ENV` | `production` | Build mode |
| `VITE_APP_NAME` | `Coffee Cloud` | App name |
| `VITE_VERSION` | `1.0.0` | Version |

{{% notice tip %}}
💡 **Tip**: Variables có prefix `VITE_` sẽ được expose trong React app
{{% /notice %}}

## 4. Enable Build Optimizations

### 4.1 Enable Cache
- ✅ **Cache dependencies**: Saves ~1 minute per build
- ✅ **Reuse build artifacts**: Faster deployments

### 4.2 Concurrent Builds
- **Limit**: 1 (Free Tier default)
- Upgrade plan để increase limit nếu cần

## 5. Configure Redirects for SPA

1. Click **Rewrites and redirects**
2. Add rule cho React Router:

| Source | Target | Type |
|--------|--------|------|
| `</^[^.]+$\|\.(?!(css\|gif\|ico\|jpg\|js\|png\|txt\|svg\|woff\|ttf)$)([^.]+$)/>` | `/index.html` | `200 (Rewrite)` |

Click **Save**

## 6. Custom Headers (Optional)

Add security headers:

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

## 7. Test Build

1. Click **Redeploy this version**
2. Monitor build logs
3. Verify app functionality

## Next Steps

Continue with [Testing & Verification](../5.1.6-testing/)
