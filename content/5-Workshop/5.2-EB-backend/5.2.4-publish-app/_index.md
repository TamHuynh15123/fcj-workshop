---
title: "Publish Application"
weight: 4
chapter: false
pre: " <b> 5.2.4 </b> "
---

# Publish .NET Application for Deployment

Before deploying to Elastic Beanstalk, we need to publish our .NET application into a deployment package.

#### Step 1: Test Locally with Swagger

First, make sure your API works locally:

```bash
cd CoffeeCloudAPI
dotnet run
```

Open your browser and go to:
- `http://localhost:5000/swagger`

You should see **Swagger UI** with all your API endpoints. Try testing a few:
- Click on `GET /api/menu` → **Try it out** → **Execute**
- You should see the menu items JSON response

Press `Ctrl+C` to stop the server.

#### Step 2: Publish for Windows (Elastic Beanstalk Default)

Elastic Beanstalk for .NET runs on Windows Server by default. Publish your app:

```bash
dotnet publish -c Release -o ./publish
```

This creates a `publish` folder with all necessary files.

#### Step 3: Create Deployment Package

Create a ZIP file from the published output:

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

**Important:** The ZIP should contain the files directly, not a parent folder:
```
CoffeeCloudAPI.zip
├── CoffeeCloudAPI.dll
├── CoffeeCloudAPI.deps.json
├── CoffeeCloudAPI.runtimeconfig.json
├── appsettings.json
├── web.config
└── ... other files
```

#### Step 4: Verify ZIP Contents

**Windows:**
```powershell
# List contents
Expand-Archive -Path CoffeeCloudAPI.zip -DestinationPath temp
Get-ChildItem temp
Remove-Item temp -Recurse
```

**Mac/Linux:**
```bash
unzip -l CoffeeCloudAPI.zip | head -20
```

You should see these key files:
- ✅ `CoffeeCloudAPI.dll` (your main application)
- ✅ `web.config` (IIS configuration)
- ✅ `appsettings.json` (app settings)
- ✅ All dependency DLLs

#### Step 5: Check File Size

```bash
# Windows PowerShell
(Get-Item CoffeeCloudAPI.zip).Length / 1MB

# Mac/Linux
du -h CoffeeCloudAPI.zip
```

Typical size: **15-30 MB** (compressed)

**Elastic Beanstalk Limits:**
- Maximum deployment package: **512 MB**
- You're well within limits! ✅

#### Step 6: Optional - Add Procfile (Advanced)

If you want to customize the startup command, create a `Procfile` in your project root:

**Procfile** (no extension):
```
web: dotnet CoffeeCloudAPI.dll --urls=http://0.0.0.0:5000
```

Then republish and rezip:
```bash
dotnet publish -c Release -o ./publish
# Copy Procfile to publish folder
Copy-Item Procfile .\publish\
Compress-Archive -Path .\publish\* -DestinationPath CoffeeCloudAPI.zip -Force
```

#### Step 7: Verify Swagger Configuration

Make sure Swagger is enabled for production. Check your `Program.cs`:

```csharp
var app = builder.Build();

// Enable Swagger in all environments
app.UseSwagger();
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "Coffee Cloud API V1");
    c.RoutePrefix = "swagger"; // Access via /swagger
});

app.UseCors("AllowAmplify");
app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

**Important:** Remove `if (app.Environment.IsDevelopment())` condition to enable Swagger in production!

#### Deployment Package Ready! 📦

You now have:
- ✅ `CoffeeCloudAPI.zip` - Ready to upload to Elastic Beanstalk
- ✅ Swagger UI enabled for testing
- ✅ All dependencies included
- ✅ Proper configuration files

**File Location:**
```
CoffeeCloudAPI/
├── CoffeeCloudAPI/
│   ├── ... source code ...
├── publish/
│   └── ... published files ...
└── CoffeeCloudAPI.zip  ← This is what we'll upload!
```

#### Common Issues

**Issue:** ZIP file is too large (>512 MB)
**Solution:** 
- Remove unnecessary files from publish folder
- Check for duplicated dependencies
- Use `dotnet publish --self-contained false`

**Issue:** Swagger doesn't work after deployment
**Solution:**
- Make sure `UseSwagger()` is called without environment check
- Verify `appsettings.json` is included in ZIP
- Check HTTPS redirection settings

**Issue:** Application won't start
**Solution:**
- Verify `web.config` is present
- Check .NET version matches (8.0)
- Review CloudWatch logs after deployment

#### Next Steps

Now that we have our deployment package, let's upload it to AWS Elastic Beanstalk! →

