---
title: "Publish Ứng dụng"
weight: 4
chapter: false
pre: " <b> 5.2.4 </b> "
---

# Publish Ứng dụng .NET để Triển khai

Trước khi triển khai lên Elastic Beanstalk, chúng ta cần publish ứng dụng .NET thành package triển khai.

#### Bước 1: Kiểm tra Locally với Swagger

Đầu tiên, đảm bảo API hoạt động ở local:

```bash
cd CoffeeCloudAPI
dotnet run
```

Mở trình duyệt và truy cập:
- `http://localhost:5000/swagger`

Bạn sẽ thấy **Swagger UI** với tất cả API endpoints. Thử test một vài:
- Click vào `GET /api/menu` → **Try it out** → **Execute**
- Bạn sẽ thấy kết quả JSON của menu items

Nhấn `Ctrl+C` để dừng server.

#### Bước 2: Publish cho Windows (Mặc định Elastic Beanstalk)

Elastic Beanstalk cho .NET chạy trên Windows Server theo mặc định. Publish ứng dụng:

```bash
dotnet publish -c Release -o ./publish
```

Lệnh này tạo thư mục `publish` với tất cả files cần thiết.

#### Bước 3: Tạo Deployment Package

Tạo file ZIP từ output đã publish:

**Windows (PowerShell):**
```powershell
Compress-Archive -Path .\publish\* -DestinationPath CoffeeCloudAPI.zip -Force
```

**Mac/Linux:**
```bash
cd publish
zip -r ../CoffeeCloudAPI.zip *
cd ..
```

**Quan trọng:** ZIP phải chứa các files trực tiếp, không có thư mục cha:
```
CoffeeCloudAPI.zip
├── CoffeeCloudAPI.dll
├── CoffeeCloudAPI.deps.json
├── CoffeeCloudAPI.runtimeconfig.json
├── appsettings.json
├── web.config
└── ... các file khác
```

#### Bước 4: Xác minh Nội dung ZIP

**Windows:**
```powershell
# Liệt kê nội dung
Expand-Archive -Path CoffeeCloudAPI.zip -DestinationPath temp
Get-ChildItem temp
Remove-Item temp -Recurse
```

**Mac/Linux:**
```bash
unzip -l CoffeeCloudAPI.zip | head -20
```

Bạn phải thấy các file chính:
- ✅ `CoffeeCloudAPI.dll` (ứng dụng chính)
- ✅ `web.config` (cấu hình IIS)
- ✅ `appsettings.json` (cài đặt app)
- ✅ Tất cả các dependency DLLs

#### Bước 5: Kiểm tra Kích thước File

```bash
# Windows PowerShell
(Get-Item CoffeeCloudAPI.zip).Length / 1MB

# Mac/Linux
du -h CoffeeCloudAPI.zip
```

Kích thước thông thường: **15-30 MB** (đã nén)

**Giới hạn Elastic Beanstalk:**
- Deployment package tối đa: **512 MB**
- Bạn vẫn trong giới hạn! ✅

#### Bước 6: Tùy chọn - Thêm Procfile (Nâng cao)

Nếu muốn tùy chỉnh lệnh khởi động, tạo `Procfile` trong thư mục gốc project:

**Procfile** (không có đuôi file):
```
web: dotnet CoffeeCloudAPI.dll --urls=http://0.0.0.0:5000
```

Sau đó publish và zip lại:
```bash
dotnet publish -c Release -o ./publish
# Copy Procfile vào thư mục publish
Copy-Item Procfile .\publish\
Compress-Archive -Path .\publish\* -DestinationPath CoffeeCloudAPI.zip -Force
```

#### Bước 7: Xác minh Cấu hình Swagger

Đảm bảo Swagger được bật cho production. Kiểm tra `Program.cs`:

```csharp
var app = builder.Build();

// Bật Swagger trong tất cả môi trường
app.UseSwagger();
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "Coffee Cloud API V1");
    c.RoutePrefix = "swagger"; // Truy cập qua /swagger
});

app.UseCors("AllowAmplify");
app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

**Quan trọng:** Xóa điều kiện `if (app.Environment.IsDevelopment())` để bật Swagger trong production!

#### Deployment Package Sẵn sàng! 📦

Bây giờ bạn có:
- ✅ `CoffeeCloudAPI.zip` - Sẵn sàng upload lên Elastic Beanstalk
- ✅ Swagger UI đã bật để testing
- ✅ Tất cả dependencies đã bao gồm
- ✅ Các file cấu hình phù hợp

**Vị trí File:**
```
CoffeeCloudAPI/
├── CoffeeCloudAPI/
│   ├── ... source code ...
├── publish/
│   └── ... published files ...
└── CoffeeCloudAPI.zip  ← File này sẽ upload!
```

#### Các Vấn đề Thường gặp

**Vấn đề:** File ZIP quá lớn (>512 MB)
**Giải pháp:** 
- Xóa các file không cần thiết khỏi thư mục publish
- Kiểm tra các dependency bị trùng lặp
- Dùng `dotnet publish --self-contained false`

**Vấn đề:** Swagger không hoạt động sau khi deploy
**Giải pháp:**
- Đảm bảo `UseSwagger()` được gọi không có điều kiện môi trường
- Xác minh `appsettings.json` có trong ZIP
- Kiểm tra cài đặt HTTPS redirection

**Vấn đề:** Ứng dụng không khởi động
**Giải pháp:**
- Xác minh `web.config` có mặt
- Kiểm tra phiên bản .NET khớp (8.0)
- Xem CloudWatch logs sau khi deploy

#### Bước tiếp theo

Bây giờ chúng ta đã có deployment package, hãy upload lên AWS Elastic Beanstalk! →

