---
title: "Testing & Verification"
weight: 6
chapter: false
pre: " <b> 5.1.6 </b> "
---

# Testing & Verification

## 1. Functional Testing

### 1.1 Test all pages

- [ ] Homepage loads correctly
- [ ] Menu displays products
- [ ] Order page accessible
- [ ] Login form displays
- [ ] Navigation works
- [ ] Footer displays

### 1.2 Test Routing

Test các URLs:
```
https://your-app.amplifyapp.com/
https://your-app.amplifyapp.com/menu
https://your-app.amplifyapp.com/order
https://your-app.amplifyapp.com/login
```

Refresh mỗi page → Không bị 404 ✅

## 2. Responsive Testing

Test trên nhiều devices:
- 📱 Mobile (375px)
- 📱 Tablet (768px)
- 💻 Desktop (1920px)

Chrome DevTools → Toggle device toolbar

## 3. Performance Testing

### 3.1 Google PageSpeed Insights

1. Truy cập [https://pagespeed.web.dev/](https://pagespeed.web.dev/)
2. Nhập Amplify URL
3. Target scores:
   - Performance: > 90
   - Accessibility: > 90
   - Best Practices: > 90
   - SEO: > 90

### 3.2 Network Tab

Chrome DevTools → Network:
- Total page size: < 2MB ✅
- Load time: < 3s ✅
- Number of requests: < 50 ✅

## 4. CI/CD Testing

### 4.1 Test Auto-Deploy

1. Make code change
2. Commit and push
3. Verify auto-deploy triggers
4. Check deploy success

## 5. Cleanup (Optional)

Nếu muốn xóa app để tránh costs:

1. Amplify Console → **Actions** → **Delete app**
2. Confirm deletion

{{% notice warning %}}
⚠️ **Cảnh báo**: Xóa app sẽ xóa tất cả deployments và không thể khôi phục!
{{% /notice %}}

## 🎉 Congratulations!

Bạn đã hoàn thành Workshop 1! 

**Đã học được:**
- ✅ Tạo ReactJS app với Vite
- ✅ Setup Git + GitHub
- ✅ Deploy lên AWS Amplify
- ✅ Configure CI/CD pipeline
- ✅ Optimize build settings

## Next Workshop

Tiếp tục với [Workshop 2: Cognito Authentication](../../5.2-cognito-auth/) để implement user authentication!
