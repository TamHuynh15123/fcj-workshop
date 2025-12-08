---
title: "Kiểm tra và xác minh"
weight: 6
chapter: false
pre: " <b> 5.1.6 </b> "
---

# Kiểm tra và xác minh

## 1. Kiểm tra chức năng

### 1.1 Kiểm tra tất cả các trang

- [ ] Trang chủ tải đúng
- [ ] Menu hiển thị sản phẩm
- [ ] Trang đặt hàng truy cập được
- [ ] Form đăng nhập hiển thị
- [ ] Navigation hoạt động
- [ ] Footer hiển thị

### 1.2 Kiểm tra Routing

Kiểm tra các URLs:
```
https://your-app.amplifyapp.com/
https://your-app.amplifyapp.com/menu
https://your-app.amplifyapp.com/order
https://your-app.amplifyapp.com/login
```

Refresh mỗi trang → Không bị lỗi 404 ✅

## 2. Kiểm tra Responsive

Kiểm tra trên nhiều thiết bị:
- 📱 Mobile (375px)
- 📱 Tablet (768px)
- 💻 Desktop (1920px)

Chrome DevTools → Toggle device toolbar

## 3. Kiểm tra Performance

### 3.1 Google PageSpeed Insights

1. Truy cập [https://pagespeed.web.dev/](https://pagespeed.web.dev/)
2. Nhập Amplify URL
3. Điểm mục tiêu:
   - Performance: > 90
   - Accessibility: > 90
   - Best Practices: > 90
   - SEO: > 90

### 3.2 Network Tab

Chrome DevTools → Network:
- Tổng kích thước trang: < 2MB ✅
- Thời gian tải: < 3s ✅
- Số lượng requests: < 50 ✅

## 4. Kiểm tra CI/CD

### 4.1 Kiểm tra Auto-Deploy

1. Thay đổi code
2. Commit và push
3. Xác minh auto-deploy kích hoạt
4. Kiểm tra deploy thành công

## 5. Dọn dẹp (Tùy chọn)

Nếu muốn xóa app để tránh chi phí:

1. Amplify Console → **Actions** → **Delete app**
2. Xác nhận xóa

{{% notice warning %}}
⚠️ **Cảnh báo**: Xóa app sẽ xóa tất cả deployments và không thể khôi phục!
{{% /notice %}}

## 🎉 Chúc mừng!

Bạn đã hoàn thành Workshop 1! 

**Đã học được:**
- ✅ Tạo ReactJS app với Vite
- ✅ Thiết lập Git + GitHub
- ✅ Deploy lên AWS Amplify
- ✅ Cấu hình CI/CD pipeline
- ✅ Tối ưu hóa build settings

## Workshop tiếp theo

Tiếp tục với [Workshop 2: Cognito Authentication](../../5.2-cognito-auth/) để triển khai xác thực người dùng!
