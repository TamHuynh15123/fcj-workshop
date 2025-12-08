---
title: "Tạo .NET Web API"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Tạo .NET 8.0 Web API

Trong phần này, chúng ta sẽ tạo một Web API .NET 8.0 hoàn chỉnh cho backend Coffee Cloud với quản lý menu và đơn hàng.

#### Bước 1: Tạo API Project Mới

Mở terminal và tạo project:

```bash
# Tạo thư mục mới
mkdir CoffeeCloudAPI
cd CoffeeCloudAPI

# Tạo Web API project mới
dotnet new webapi -n CoffeeCloudAPI

# Di chuyển vào thư mục project
cd CoffeeCloudAPI

# Chạy để kiểm tra hoạt động
dotnet run
```

Bạn sẽ thấy:
```
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5000
```

Nhấn `Ctrl+C` để dừng.

#### Bước 2: Cài đặt Packages cần thiết

```bash
# AWS SDK cho DynamoDB
dotnet add package AWSSDK.DynamoDBv2

# Newtonsoft JSON cho xử lý JSON tốt hơn
dotnet add package Newtonsoft.Json

# Hỗ trợ CORS
dotnet add package Microsoft.AspNetCore.Cors
```

#### Bước 3: Tạo Models

Tạo thư mục `Models` và thêm các data models:

**Models/MenuItem.cs**
```csharp
namespace CoffeeCloudAPI.Models
{
    public class MenuItem
    {
        public string Id { get; set; } = Guid.NewGuid().ToString();
        public string Name { get; set; } = string.Empty;
        public string Description { get; set; } = string.Empty;
        public decimal Price { get; set; }
        public string Category { get; set; } = string.Empty; // Coffee, Tea, Food, etc.
        public string ImageUrl { get; set; } = string.Empty;
        public bool IsAvailable { get; set; } = true;
        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
    }
}
```

**Models/Order.cs**
```csharp
namespace CoffeeCloudAPI.Models
{
    public class Order
    {
        public string Id { get; set; } = Guid.NewGuid().ToString();
        public string UserId { get; set; } = string.Empty;
        public string UserName { get; set; } = string.Empty;
        public List<OrderItem> Items { get; set; } = new();
        public decimal TotalAmount { get; set; }
        public string Status { get; set; } = "Pending"; // Pending, Confirmed, Preparing, Shipping, Delivered
        public string DeliveryAddress { get; set; } = string.Empty;
        public string PhoneNumber { get; set; } = string.Empty;
        public DateTime CreatedAt { get; set; } = DateTime.UtcNow;
        public DateTime? UpdatedAt { get; set; }
    }

    public class OrderItem
    {
        public string MenuItemId { get; set; } = string.Empty;
        public string Name { get; set; } = string.Empty;
        public int Quantity { get; set; }
        public decimal Price { get; set; }
        public decimal Subtotal => Quantity * Price;
    }
}
```

**Models/ApiResponse.cs**
```csharp
namespace CoffeeCloudAPI.Models
{
    public class ApiResponse<T>
    {
        public bool Success { get; set; }
        public string Message { get; set; } = string.Empty;
        public T? Data { get; set; }
        
        public static ApiResponse<T> SuccessResponse(T data, string message = "Success")
        {
            return new ApiResponse<T>
            {
                Success = true,
                Message = message,
                Data = data
            };
        }
        
        public static ApiResponse<T> ErrorResponse(string message)
        {
            return new ApiResponse<T>
            {
                Success = false,
                Message = message,
                Data = default
            };
        }
    }
}
```

#### Bước 4: Tạo Service Interfaces

Tạo thư mục `Services`:

**Services/IMenuService.cs**
```csharp
using CoffeeCloudAPI.Models;

namespace CoffeeCloudAPI.Services
{
    public interface IMenuService
    {
        Task<List<MenuItem>> GetAllMenuItemsAsync();
        Task<MenuItem?> GetMenuItemByIdAsync(string id);
        Task<List<MenuItem>> GetMenuItemsByCategoryAsync(string category);
        Task<MenuItem> CreateMenuItemAsync(MenuItem item);
        Task<bool> UpdateMenuItemAsync(MenuItem item);
        Task<bool> DeleteMenuItemAsync(string id);
    }
}
```

**Services/IOrderService.cs**
```csharp
using CoffeeCloudAPI.Models;

namespace CoffeeCloudAPI.Services
{
    public interface IOrderService
    {
        Task<Order> CreateOrderAsync(Order order);
        Task<Order?> GetOrderByIdAsync(string id);
        Task<List<Order>> GetOrdersByUserIdAsync(string userId);
        Task<bool> UpdateOrderStatusAsync(string id, string status);
        Task<List<Order>> GetAllOrdersAsync();
    }
}
```

#### Bước 5: Triển khai Services (In-Memory tạm thời)

**Services/MenuService.cs**
```csharp
using CoffeeCloudAPI.Models;

namespace CoffeeCloudAPI.Services
{
    public class MenuService : IMenuService
    {
        private readonly List<MenuItem> _menuItems;

        public MenuService()
        {
            // Khởi tạo với dữ liệu mẫu
            _menuItems = new List<MenuItem>
            {
                new MenuItem { Id = "1", Name = "Espresso", Description = "Cà phê đen đậm đà", Price = 3.50m, Category = "Coffee", ImageUrl = "/images/espresso.jpg" },
                new MenuItem { Id = "2", Name = "Cappuccino", Description = "Espresso với sữa hấp", Price = 4.50m, Category = "Coffee", ImageUrl = "/images/cappuccino.jpg" },
                new MenuItem { Id = "3", Name = "Latte", Description = "Cà phê sữa mượt mà", Price = 4.75m, Category = "Coffee", ImageUrl = "/images/latte.jpg" },
                new MenuItem { Id = "4", Name = "Trà Xanh", Description = "Trà xanh tươi", Price = 3.00m, Category = "Tea", ImageUrl = "/images/green-tea.jpg" },
                new MenuItem { Id = "5", Name = "Bánh Sừng Bò", Description = "Bánh ngọt bơ", Price = 2.50m, Category = "Food", ImageUrl = "/images/croissant.jpg" }
            };
        }

        public Task<List<MenuItem>> GetAllMenuItemsAsync()
        {
            return Task.FromResult(_menuItems.Where(m => m.IsAvailable).ToList());
        }

        public Task<MenuItem?> GetMenuItemByIdAsync(string id)
        {
            var item = _menuItems.FirstOrDefault(m => m.Id == id);
            return Task.FromResult(item);
        }

        public Task<List<MenuItem>> GetMenuItemsByCategoryAsync(string category)
        {
            var items = _menuItems.Where(m => 
                m.Category.Equals(category, StringComparison.OrdinalIgnoreCase) && m.IsAvailable
            ).ToList();
            return Task.FromResult(items);
        }

        public Task<MenuItem> CreateMenuItemAsync(MenuItem item)
        {
            item.Id = Guid.NewGuid().ToString();
            item.CreatedAt = DateTime.UtcNow;
            _menuItems.Add(item);
            return Task.FromResult(item);
        }

        public Task<bool> UpdateMenuItemAsync(MenuItem item)
        {
            var existing = _menuItems.FirstOrDefault(m => m.Id == item.Id);
            if (existing == null) return Task.FromResult(false);

            existing.Name = item.Name;
            existing.Description = item.Description;
            existing.Price = item.Price;
            existing.Category = item.Category;
            existing.ImageUrl = item.ImageUrl;
            existing.IsAvailable = item.IsAvailable;
            
            return Task.FromResult(true);
        }

        public Task<bool> DeleteMenuItemAsync(string id)
        {
            var item = _menuItems.FirstOrDefault(m => m.Id == id);
            if (item == null) return Task.FromResult(false);

            _menuItems.Remove(item);
            return Task.FromResult(true);
        }
    }
}
```

**Services/OrderService.cs**
```csharp
using CoffeeCloudAPI.Models;

namespace CoffeeCloudAPI.Services
{
    public class OrderService : IOrderService
    {
        private readonly List<Order> _orders = new();

        public Task<Order> CreateOrderAsync(Order order)
        {
            order.Id = Guid.NewGuid().ToString();
            order.CreatedAt = DateTime.UtcNow;
            order.Status = "Pending";
            
            // Tính tổng tiền
            order.TotalAmount = order.Items.Sum(item => item.Subtotal);
            
            _orders.Add(order);
            return Task.FromResult(order);
        }

        public Task<Order?> GetOrderByIdAsync(string id)
        {
            var order = _orders.FirstOrDefault(o => o.Id == id);
            return Task.FromResult(order);
        }

        public Task<List<Order>> GetOrdersByUserIdAsync(string userId)
        {
            var orders = _orders.Where(o => o.UserId == userId).OrderByDescending(o => o.CreatedAt).ToList();
            return Task.FromResult(orders);
        }

        public Task<bool> UpdateOrderStatusAsync(string id, string status)
        {
            var order = _orders.FirstOrDefault(o => o.Id == id);
            if (order == null) return Task.FromResult(false);

            order.Status = status;
            order.UpdatedAt = DateTime.UtcNow;
            return Task.FromResult(true);
        }

        public Task<List<Order>> GetAllOrdersAsync()
        {
            return Task.FromResult(_orders.OrderByDescending(o => o.CreatedAt).ToList());
        }
    }
}
```

#### Bước 6: Tạo Controllers

**Controllers/MenuController.cs**
```csharp
using Microsoft.AspNetCore.Mvc;
using CoffeeCloudAPI.Models;
using CoffeeCloudAPI.Services;

namespace CoffeeCloudAPI.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MenuController : ControllerBase
    {
        private readonly IMenuService _menuService;
        private readonly ILogger<MenuController> _logger;

        public MenuController(IMenuService menuService, ILogger<MenuController> logger)
        {
            _menuService = menuService;
            _logger = logger;
        }

        [HttpGet]
        public async Task<ActionResult<ApiResponse<List<MenuItem>>>> GetAll()
        {
            try
            {
                var items = await _menuService.GetAllMenuItemsAsync();
                return Ok(ApiResponse<List<MenuItem>>.SuccessResponse(items, "Lấy menu items thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy menu items");
                return StatusCode(500, ApiResponse<List<MenuItem>>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<ApiResponse<MenuItem>>> GetById(string id)
        {
            try
            {
                var item = await _menuService.GetMenuItemByIdAsync(id);
                if (item == null)
                    return NotFound(ApiResponse<MenuItem>.ErrorResponse("Không tìm thấy menu item"));

                return Ok(ApiResponse<MenuItem>.SuccessResponse(item));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy menu item {Id}", id);
                return StatusCode(500, ApiResponse<MenuItem>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpGet("category/{category}")]
        public async Task<ActionResult<ApiResponse<List<MenuItem>>>> GetByCategory(string category)
        {
            try
            {
                var items = await _menuService.GetMenuItemsByCategoryAsync(category);
                return Ok(ApiResponse<List<MenuItem>>.SuccessResponse(items, $"Lấy items danh mục '{category}' thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy items cho danh mục {Category}", category);
                return StatusCode(500, ApiResponse<List<MenuItem>>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpPost]
        public async Task<ActionResult<ApiResponse<MenuItem>>> Create([FromBody] MenuItem item)
        {
            try
            {
                var created = await _menuService.CreateMenuItemAsync(item);
                return CreatedAtAction(nameof(GetById), new { id = created.Id }, 
                    ApiResponse<MenuItem>.SuccessResponse(created, "Tạo menu item thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi tạo menu item");
                return StatusCode(500, ApiResponse<MenuItem>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }
    }
}
```

**Controllers/OrderController.cs**
```csharp
using Microsoft.AspNetCore.Mvc;
using CoffeeCloudAPI.Models;
using CoffeeCloudAPI.Services;

namespace CoffeeCloudAPI.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class OrderController : ControllerBase
    {
        private readonly IOrderService _orderService;
        private readonly ILogger<OrderController> _logger;

        public OrderController(IOrderService orderService, ILogger<OrderController> logger)
        {
            _orderService = orderService;
            _logger = logger;
        }

        [HttpPost]
        public async Task<ActionResult<ApiResponse<Order>>> CreateOrder([FromBody] Order order)
        {
            try
            {
                var created = await _orderService.CreateOrderAsync(order);
                return CreatedAtAction(nameof(GetOrderById), new { id = created.Id },
                    ApiResponse<Order>.SuccessResponse(created, "Tạo đơn hàng thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi tạo đơn hàng");
                return StatusCode(500, ApiResponse<Order>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<ApiResponse<Order>>> GetOrderById(string id)
        {
            try
            {
                var order = await _orderService.GetOrderByIdAsync(id);
                if (order == null)
                    return NotFound(ApiResponse<Order>.ErrorResponse("Không tìm thấy đơn hàng"));

                return Ok(ApiResponse<Order>.SuccessResponse(order));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy đơn hàng {Id}", id);
                return StatusCode(500, ApiResponse<Order>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpGet("user/{userId}")]
        public async Task<ActionResult<ApiResponse<List<Order>>>> GetUserOrders(string userId)
        {
            try
            {
                var orders = await _orderService.GetOrdersByUserIdAsync(userId);
                return Ok(ApiResponse<List<Order>>.SuccessResponse(orders, "Lấy đơn hàng user thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy đơn hàng cho user {UserId}", userId);
                return StatusCode(500, ApiResponse<List<Order>>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpPut("{id}/status")]
        public async Task<ActionResult<ApiResponse<bool>>> UpdateOrderStatus(string id, [FromBody] string status)
        {
            try
            {
                var updated = await _orderService.UpdateOrderStatusAsync(id, status);
                if (!updated)
                    return NotFound(ApiResponse<bool>.ErrorResponse("Không tìm thấy đơn hàng"));

                return Ok(ApiResponse<bool>.SuccessResponse(true, "Cập nhật trạng thái đơn hàng thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi cập nhật trạng thái đơn hàng {Id}", id);
                return StatusCode(500, ApiResponse<bool>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }

        [HttpGet]
        public async Task<ActionResult<ApiResponse<List<Order>>>> GetAllOrders()
        {
            try
            {
                var orders = await _orderService.GetAllOrdersAsync();
                return Ok(ApiResponse<List<Order>>.SuccessResponse(orders, "Lấy tất cả đơn hàng thành công"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Lỗi khi lấy tất cả đơn hàng");
                return StatusCode(500, ApiResponse<List<Order>>.ErrorResponse("Lỗi máy chủ nội bộ"));
            }
        }
    }
}
```

**Controllers/HealthController.cs**
```csharp
using Microsoft.AspNetCore.Mvc;

namespace CoffeeCloudAPI.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class HealthController : ControllerBase
    {
        [HttpGet]
        public IActionResult Get()
        {
            return Ok(new
            {
                status = "Healthy",
                timestamp = DateTime.UtcNow,
                version = "1.0.0",
                service = "Coffee Cloud API"
            });
        }
    }
}
```

#### Bước 7: Cập nhật Program.cs

Thay thế nội dung của `Program.cs`:

```csharp
using CoffeeCloudAPI.Services;

var builder = WebApplication.CreateBuilder(args);

// Thêm services vào container
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// Đăng ký các services của chúng ta
builder.Services.AddSingleton<IMenuService, MenuService>();
builder.Services.AddSingleton<IOrderService, OrderService>();

// Thêm CORS
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowAmplify", policy =>
    {
        policy.WithOrigins(
            "http://localhost:5173",  // Vite dev server
            "https://*.amplifyapp.com" // Amplify production
        )
        .AllowAnyMethod()
        .AllowAnyHeader()
        .AllowCredentials();
    });
});

var app = builder.Build();

// Cấu hình HTTP request pipeline
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseCors("AllowAmplify");

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

#### Bước 8: Kiểm tra API

Chạy API:

```bash
dotnet run
```

Mở trình duyệt và test:
- `http://localhost:5000/api/health` - Nên hiện trạng thái healthy
- `http://localhost:5000/swagger` - Tài liệu API tương tác

Test với curl:

```bash
# Lấy tất cả menu items
curl http://localhost:5000/api/menu

# Lấy menu items theo danh mục
curl http://localhost:5000/api/menu/category/Coffee

# Tạo đơn hàng
curl -X POST http://localhost:5000/api/order \
  -H "Content-Type: application/json" \
  -d '{
    "userId": "user123",
    "userName": "Nguyễn Văn A",
    "phoneNumber": "+84987654321",
    "deliveryAddress": "123 Đường Cà Phê",
    "items": [
      {
        "menuItemId": "1",
        "name": "Espresso",
        "quantity": 2,
        "price": 3.50
      }
    ]
  }'
```

#### Cấu trúc Project

Project của bạn bây giờ sẽ trông như:

```
CoffeeCloudAPI/
├── Controllers/
│   ├── HealthController.cs
│   ├── MenuController.cs
│   └── OrderController.cs
├── Models/
│   ├── ApiResponse.cs
│   ├── MenuItem.cs
│   └── Order.cs
├── Services/
│   ├── IMenuService.cs
│   ├── IOrderService.cs
│   ├── MenuService.cs
│   └── OrderService.cs
├── Program.cs
├── appsettings.json
└── CoffeeCloudAPI.csproj
```

✅ **API của bạn đã sẵn sàng!** Tiếp theo, chúng ta sẽ container hóa nó với Docker. →

