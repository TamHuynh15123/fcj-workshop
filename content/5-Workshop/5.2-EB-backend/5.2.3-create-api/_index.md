---
title: "Create .NET Web API"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Create .NET 8.0 Web API

In this section, we'll create a complete .NET 8.0 Web API for the Coffee Cloud backend with menu and order management.

#### Step 1: Create New API Project

Open terminal and create the project:

```bash
# Create new directory
mkdir CoffeeCloudAPI
cd CoffeeCloudAPI

# Create new Web API project
dotnet new webapi -n CoffeeCloudAPI

# Navigate to project folder
cd CoffeeCloudAPI

# Run to verify it works
dotnet run
```

You should see:
```
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5000
```

Press `Ctrl+C` to stop.

#### Step 2: Install Required Packages

```bash
# AWS SDK for DynamoDB
dotnet add package AWSSDK.DynamoDBv2

# Newtonsoft JSON for better JSON handling
dotnet add package Newtonsoft.Json

# CORS support
dotnet add package Microsoft.AspNetCore.Cors
```

#### Step 3: Create Models

Create `Models` folder and add data models:

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

#### Step 4: Create Service Interfaces

Create `Services` folder:

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

#### Step 5: Implement Services (In-Memory for now)

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
            // Initialize with sample data
            _menuItems = new List<MenuItem>
            {
                new MenuItem { Id = "1", Name = "Espresso", Description = "Strong black coffee", Price = 3.50m, Category = "Coffee", ImageUrl = "/images/espresso.jpg" },
                new MenuItem { Id = "2", Name = "Cappuccino", Description = "Espresso with steamed milk", Price = 4.50m, Category = "Coffee", ImageUrl = "/images/cappuccino.jpg" },
                new MenuItem { Id = "3", Name = "Latte", Description = "Smooth coffee with milk", Price = 4.75m, Category = "Coffee", ImageUrl = "/images/latte.jpg" },
                new MenuItem { Id = "4", Name = "Green Tea", Description = "Fresh green tea", Price = 3.00m, Category = "Tea", ImageUrl = "/images/green-tea.jpg" },
                new MenuItem { Id = "5", Name = "Croissant", Description = "Buttery pastry", Price = 2.50m, Category = "Food", ImageUrl = "/images/croissant.jpg" }
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
            
            // Calculate total
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

#### Step 6: Create Controllers

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
                return Ok(ApiResponse<List<MenuItem>>.SuccessResponse(items, "Menu items retrieved successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting menu items");
                return StatusCode(500, ApiResponse<List<MenuItem>>.ErrorResponse("Internal server error"));
            }
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<ApiResponse<MenuItem>>> GetById(string id)
        {
            try
            {
                var item = await _menuService.GetMenuItemByIdAsync(id);
                if (item == null)
                    return NotFound(ApiResponse<MenuItem>.ErrorResponse("Menu item not found"));

                return Ok(ApiResponse<MenuItem>.SuccessResponse(item));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting menu item {Id}", id);
                return StatusCode(500, ApiResponse<MenuItem>.ErrorResponse("Internal server error"));
            }
        }

        [HttpGet("category/{category}")]
        public async Task<ActionResult<ApiResponse<List<MenuItem>>>> GetByCategory(string category)
        {
            try
            {
                var items = await _menuService.GetMenuItemsByCategoryAsync(category);
                return Ok(ApiResponse<List<MenuItem>>.SuccessResponse(items, $"Items in category '{category}' retrieved"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting items for category {Category}", category);
                return StatusCode(500, ApiResponse<List<MenuItem>>.ErrorResponse("Internal server error"));
            }
        }

        [HttpPost]
        public async Task<ActionResult<ApiResponse<MenuItem>>> Create([FromBody] MenuItem item)
        {
            try
            {
                var created = await _menuService.CreateMenuItemAsync(item);
                return CreatedAtAction(nameof(GetById), new { id = created.Id }, 
                    ApiResponse<MenuItem>.SuccessResponse(created, "Menu item created successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error creating menu item");
                return StatusCode(500, ApiResponse<MenuItem>.ErrorResponse("Internal server error"));
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
                    ApiResponse<Order>.SuccessResponse(created, "Order created successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error creating order");
                return StatusCode(500, ApiResponse<Order>.ErrorResponse("Internal server error"));
            }
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<ApiResponse<Order>>> GetOrderById(string id)
        {
            try
            {
                var order = await _orderService.GetOrderByIdAsync(id);
                if (order == null)
                    return NotFound(ApiResponse<Order>.ErrorResponse("Order not found"));

                return Ok(ApiResponse<Order>.SuccessResponse(order));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting order {Id}", id);
                return StatusCode(500, ApiResponse<Order>.ErrorResponse("Internal server error"));
            }
        }

        [HttpGet("user/{userId}")]
        public async Task<ActionResult<ApiResponse<List<Order>>>> GetUserOrders(string userId)
        {
            try
            {
                var orders = await _orderService.GetOrdersByUserIdAsync(userId);
                return Ok(ApiResponse<List<Order>>.SuccessResponse(orders, "User orders retrieved successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting orders for user {UserId}", userId);
                return StatusCode(500, ApiResponse<List<Order>>.ErrorResponse("Internal server error"));
            }
        }

        [HttpPut("{id}/status")]
        public async Task<ActionResult<ApiResponse<bool>>> UpdateOrderStatus(string id, [FromBody] string status)
        {
            try
            {
                var updated = await _orderService.UpdateOrderStatusAsync(id, status);
                if (!updated)
                    return NotFound(ApiResponse<bool>.ErrorResponse("Order not found"));

                return Ok(ApiResponse<bool>.SuccessResponse(true, "Order status updated successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error updating order status {Id}", id);
                return StatusCode(500, ApiResponse<bool>.ErrorResponse("Internal server error"));
            }
        }

        [HttpGet]
        public async Task<ActionResult<ApiResponse<List<Order>>>> GetAllOrders()
        {
            try
            {
                var orders = await _orderService.GetAllOrdersAsync();
                return Ok(ApiResponse<List<Order>>.SuccessResponse(orders, "All orders retrieved successfully"));
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error getting all orders");
                return StatusCode(500, ApiResponse<List<Order>>.ErrorResponse("Internal server error"));
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

#### Step 7: Update Program.cs

Replace the contents of `Program.cs`:

```csharp
using CoffeeCloudAPI.Services;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// Register our services
builder.Services.AddSingleton<IMenuService, MenuService>();
builder.Services.AddSingleton<IOrderService, OrderService>();

// Add CORS
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

// Configure the HTTP request pipeline
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

#### Step 8: Test the API

Run the API:

```bash
dotnet run
```

Open browser and test:
- `http://localhost:5000/api/health` - Should show healthy status
- `http://localhost:5000/swagger` - Interactive API documentation

Test with curl:

```bash
# Get all menu items
curl http://localhost:5000/api/menu

# Get menu items by category
curl http://localhost:5000/api/menu/category/Coffee

# Create an order
curl -X POST http://localhost:5000/api/order \
  -H "Content-Type: application/json" \
  -d '{
    "userId": "user123",
    "userName": "John Doe",
    "phoneNumber": "+1234567890",
    "deliveryAddress": "123 Coffee St",
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

#### Project Structure

Your project should now look like:

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

✅ **Your API is ready!** Next, we'll containerize it with Docker. →

