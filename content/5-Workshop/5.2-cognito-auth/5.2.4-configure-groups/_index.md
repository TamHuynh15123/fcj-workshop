---
title: "Configure User Groups"
weight: 4
chapter: false
pre: " <b> 5.2.4 </b> "
---

# Cấu hình User Groups

## 1. Create User Groups

### 1.1 Access Groups

1. Cognito Console → User pools → `coffee-cloud-user-pool`
2. Sidebar → Click **Groups**
3. Click **Create group**

---

### 1.2 Create Customer Group

**Group name:**
```
Customer
```

**Description:**
```
Regular customers who can order coffee and earn loyalty points
```

**IAM role:** (Optional - skip for now)
- Leave empty

**Precedence:**
```
3
```
(Lower number = higher priority. Customer có priority thấp nhất)

Click **Create group** ✅

---

### 1.3 Create Shipper Group

Click **Create group** again

**Group name:**
```
Shipper
```

**Description:**
```
Delivery personnel who can accept and deliver orders
```

**Precedence:**
```
2
```

Click **Create group** ✅

---

### 1.4 Create Admin Group

Click **Create group** again

**Group name:**
```
Admin
```

**Description:**
```
Administrators with full access to manage products, orders, and users
```

**Precedence:**
```
1
```
(Highest priority)

Click **Create group** ✅

---

## 2. Verify Groups

Sau khi tạo xong, bạn sẽ thấy 3 groups:

| Group Name | Precedence | Description |
|------------|------------|-------------|
| **Admin** | 1 | Full system access |
| **Shipper** | 2 | Delivery management |
| **Customer** | 3 | Order and browse |

![User Groups](/images/5-Workshop/5.2-cognito-auth/user-groups.png)

---

## 3. Create Test Users

### 3.1 Create Admin User

1. Click **Users** tab (sidebar)
2. Click **Create user**

**User information:**
- **Username:** `admin@coffeecloud.com`
- **Email address:** `admin@coffeecloud.com` (hoặc your real email)
- ☑️ Mark email address as verified
- ☐ Send an email invitation (unchecked)

**Temporary password:**
- ⦿ Generate a password
- ○ Set a password: (optional)

Click **Create user**

### 3.2 Add Admin to Admin Group

1. Click vào user `admin@coffeecloud.com`
2. Tab **Group memberships**
3. Click **Add user to group**
4. Select **Admin** group
5. Click **Add**

---

### 3.3 Create Customer User

Repeat process:

**Username:** `customer@coffeecloud.com`
**Email:** `customer@coffeecloud.com`
☑️ Mark email verified

Add to **Customer** group

---

### 3.4 Create Shipper User

**Username:** `shipper@coffeecloud.com`
**Email:** `shipper@coffeecloud.com`
☑️ Mark email verified

Add to **Shipper** group

---

## 4. Get Temporary Passwords

### 4.1 Retrieve Passwords

Sau khi tạo users, AWS Cognito sẽ generate temporary passwords.

**Option 1: Copy từ email** (nếu enabled email invitation)

**Option 2: Reset password manually:**
1. Click vào user
2. Tab **User attributes**
3. Click **Actions** → **Reset password**
4. Copy temporary password

{{% notice tip %}}
💡 **Tip**: Lưu temporary passwords vào notepad để test login sau
{{% /notice %}}

Example:
```
admin@coffeecloud.com: TempPass123!
customer@coffeecloud.com: TempPass456!
shipper@coffeecloud.com: TempPass789!
```

---

## 5. Verify Users and Groups

### 5.1 Check Users List

Users tab sẽ hiển thị:

| Username | Email | Status | Group |
|----------|-------|--------|-------|
| admin@coffeecloud.com | admin@coffeecloud.com | FORCE_CHANGE_PASSWORD | Admin |
| customer@coffeecloud.com | customer@coffeecloud.com | FORCE_CHANGE_PASSWORD | Customer |
| shipper@coffeecloud.com | shipper@coffeecloud.com | FORCE_CHANGE_PASSWORD | Shipper |

### 5.2 Verify Group Membership

Click vào mỗi user → Tab **Group memberships** → Verify correct group

---

## 6. (Optional) Create Additional Users via CLI

Nếu muốn tạo nhiều users nhanh:

```powershell
# Create user
aws cognito-idp admin-create-user `
  --user-pool-id us-east-1_xxxxxxxxx `
  --username customer2@coffeecloud.com `
  --user-attributes Name=email,Value=customer2@coffeecloud.com Name=email_verified,Value=true `
  --message-action SUPPRESS

# Add to group
aws cognito-idp admin-add-user-to-group `
  --user-pool-id us-east-1_xxxxxxxxx `
  --username customer2@coffeecloud.com `
  --group-name Customer
```

---

## 7. Understand Group Precedence

**Precedence** xác định priority khi user thuộc nhiều groups:

- User trong **Admin** (precedence 1) + **Customer** (precedence 3) → Admin takes priority
- User chỉ trong **Shipper** (precedence 2) → Shipper permissions
- User không thuộc group nào → No special permissions

---

## Next Steps

Tiếp tục với [Integrate with React Frontend](../5.2.5-integrate-frontend/) để implement authentication UI
