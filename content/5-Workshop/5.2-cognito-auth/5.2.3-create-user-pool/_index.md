---
title: "Create Cognito User Pool"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Tạo Amazon Cognito User Pool

## 1. Truy cập Cognito Console

### 1.1 Open AWS Console

1. Đăng nhập [https://console.aws.amazon.com](https://console.aws.amazon.com)
2. Region: Chọn **US East (N. Virginia) us-east-1** (hoặc region của bạn)
3. Search bar → Gõ "**Cognito**" → Click **Amazon Cognito**

![Cognito Console](/images/5-Workshop/5.2-cognito-auth/cognito-console.png)

---

## 2. Create User Pool

### 2.1 Click Create User Pool

1. Click **Create user pool**
2. Bắt đầu configuration wizard

### 2.2 Step 1: Configure Sign-in Experience

**Authentication providers:**
- ☑️ **Cognito user pool** (checked)
- ☐ Federated identity providers (unchecked - optional)

**Cognito user pool sign-in options:**
- ☑️ **Email** (checked)
- ☐ Username (unchecked)
- ☐ Phone number (unchecked)

**User name requirements:**
- ☐ Make user name case sensitive (unchecked - cho phép đăng nhập không phân biệt hoa thường)

Click **Next**

---

### 2.3 Step 2: Configure Security Requirements

#### Password Policy

**Password policy mode:**
- ⦿ **Cognito defaults** (recommended)

Default policy:
- Minimum length: 8 characters
- Contains uppercase letters
- Contains lowercase letters
- Contains numbers
- Contains special characters

**Or chọn Custom để tùy chỉnh:**
```
- ⦿ Custom
  - Minimum length: 8
  - ☑️ Require numbers
  - ☑️ Require special characters
  - ☑️ Require uppercase letters
  - ☑️ Require lowercase letters
```

#### Multi-factor authentication (MFA)

**MFA enforcement:**
- ⦿ **No MFA** (cho workshop, có thể enable sau)
- ○ Optional MFA
- ○ Require MFA

#### User account recovery

**Self-service account recovery:**
- ☑️ **Enable self-service account recovery** (checked)

**Delivery method for user account recovery messages:**
- ⦿ **Email only** (selected)
- ○ SMS only
- ○ Email or SMS

Click **Next**

---

### 2.4 Step 3: Configure Sign-up Experience

#### Self-service sign-up

- ☑️ **Enable self-registration** (checked - cho phép users tự đăng ký)

#### Attribute verification and user account confirmation

**Attributes to verify:**
- ☑️ **Email** (checked)
- ☐ Phone number (unchecked)

**Verifying attribute changes:**
- ☑️ **Keep original attribute value active when an update is pending** (checked)

**Active attribute values when an update is pending:**
- ☑️ Email (checked)

#### Required attributes

Select attributes cần thiết khi signup:

Standard attributes:
- ☑️ **name** (Full name)
- ☑️ **email** (Email address - auto-selected)
- ☐ phone_number (optional)
- ☐ address (optional)

Custom attributes (optional - có thể thêm sau):
- Có thể thêm: `custom:userType`, `custom:loyaltyPoints`

Click **Next**

---

### 2.5 Step 4: Configure Message Delivery

#### Email

**Email provider:**
- ⦿ **Send email with Cognito** (Free Tier: 50 emails/day)
- ○ Send email with Amazon SES (unlimited, phải verify domain)

**FROM email address:**
- Leave default: `no-reply@verificationemail.com`
- Hoặc custom (cần SES): `noreply@yourdomain.com`

**REPLY-TO email address:**
- Optional: `support@yourdomain.com`

#### SMS (Optional - skip nếu không dùng)

- Skip SMS configuration (không dùng trong workshop này)

Click **Next**

---

### 2.6 Step 5: Integrate Your App

#### User pool name

**User pool name:**
```
coffee-cloud-user-pool
```

#### Hosted authentication pages

**Use the Cognito Hosted UI:**
- ☐ Unchecked (chúng ta sẽ dùng custom UI trong React)

#### Initial app client

**App type:**
- ⦿ **Public client** (selected - cho web và mobile apps)
- ○ Confidential client

**App client name:**
```
coffee-cloud-web-client
```

**Client secret:**
- ⦿ **Don't generate a client secret** (selected - cho public web apps)

#### Advanced app client settings (Expand)

**Authentication flows:**
- ☑️ **ALLOW_USER_SRP_AUTH** (checked - Secure Remote Password)
- ☑️ **ALLOW_REFRESH_TOKEN_AUTH** (checked - cho token refresh)
- ☐ ALLOW_USER_PASSWORD_AUTH (unchecked - less secure)
- ☐ ALLOW_CUSTOM_AUTH

**Refresh token expiration:**
```
30 days
```

**Access token expiration:**
```
60 minutes
```

**ID token expiration:**
```
60 minutes
```

Click **Next**

---

### 2.7 Step 6: Review and Create

Review tất cả configurations:

| Setting | Value |
|---------|-------|
| User pool name | `coffee-cloud-user-pool` |
| Sign-in options | Email |
| Password policy | Cognito defaults |
| MFA | No MFA |
| Account recovery | Email only |
| Self-registration | Enabled |
| Required attributes | name, email |
| Email provider | Cognito |
| App client name | `coffee-cloud-web-client` |

Click **Create user pool** ✅

---

## 3. Save Configuration Details

### 3.1 User Pool ID

Sau khi tạo xong, copy thông tin sau:

1. Click vào user pool vừa tạo: `coffee-cloud-user-pool`
2. Tab **User pool overview**
3. Copy **User Pool ID**: `us-east-1_xxxxxxxxx`

![User Pool ID](/images/5-Workshop/5.2-cognito-auth/user-pool-id.png)

### 3.2 App Client ID

1. Tab **App integration** (sidebar)
2. Scroll xuống **App client list**
3. Click vào `coffee-cloud-web-client`
4. Copy **Client ID**: `abcdefghijklmnopqrstuvwxyz`

![Client ID](/images/5-Workshop/5.2-cognito-auth/client-id.png)

### 3.3 Save to File

Tạo file `src/aws-config.js` trong React project:

```javascript
const awsConfig = {
  region: 'us-east-1',
  userPoolId: 'us-east-1_xxxxxxxxx', // ← Paste User Pool ID
  userPoolWebClientId: 'abcdefghijklmnopqrstuvwxyz', // ← Paste Client ID
};

export default awsConfig;
```

{{% notice warning %}}
⚠️ **Lưu ý**: KHÔNG commit file này với real values lên Git! Add vào `.gitignore` hoặc dùng environment variables
{{% /notice %}}

---

## 4. Verify User Pool

### 4.1 Check User Pool Status

1. Cognito Console → User pools
2. Verify `coffee-cloud-user-pool` status: **Active** ✅

### 4.2 Explore Tabs

- **Users**: Danh sách users (hiện tại: 0)
- **Groups**: User groups (sẽ tạo ở bước tiếp theo)
- **App integration**: App clients và domains
- **Sign-in experience**: Authentication settings
- **Sign-up experience**: Registration settings
- **Messaging**: Email/SMS templates
- **User pool properties**: General settings

---

## Next Steps

Tiếp tục với [Configure User Groups](../5.2.4-configure-groups/) để tạo 3 groups: Customer, Shipper, Admin
