---
title: "Workshop Overview"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Workshop Overview

#### Mục tiêu Workshop

Sau khi hoàn thành workshop này, bạn sẽ có thể:
- ✅ Tạo Amazon Cognito User Pool
- ✅ Configure 3 user groups: Customer, Shipper, Admin
- ✅ Implement signup/login flow trong React
- ✅ Handle JWT tokens và session management
- ✅ Implement role-based access control (RBAC)
- ✅ Add email verification và password reset

#### Authentication Flow

```
User Registration Flow:
1. User fills signup form → Frontend validates
2. Frontend calls Cognito SignUp API
3. Cognito sends verification code via email
4. User enters code → Account confirmed
5. Admin assigns user to group (Customer/Shipper/Admin)

User Login Flow:
1. User enters email + password
2. Frontend calls Cognito SignIn API
3. Cognito validates credentials
4. Cognito returns JWT tokens (ID token, Access token, Refresh token)
5. Frontend stores tokens in localStorage
6. Frontend reads user group from token claims
7. Frontend shows UI based on user role
```

#### JWT Token Structure

```json
{
  "sub": "user-uuid",
  "email": "customer@example.com",
  "cognito:groups": ["Customer"],
  "iat": 1234567890,
  "exp": 1234571490
}
```

#### Security Features

- 🔒 **Password Policy**: Minimum 8 characters, uppercase, lowercase, numbers
- 📧 **Email Verification**: Required before login
- 🔑 **MFA** (Multi-Factor Authentication): Optional, can enable later
- 🔄 **Token Refresh**: Access tokens expire after 1 hour
- 🚫 **Account Lockout**: After 5 failed login attempts

#### Cost Estimation

With **AWS Free Tier**:
- ✅ First 50,000 MAU: **FREE**
- ✅ Email/SMS for verification: First 1000 free

After Free Tier:
- $0.0055 per MAU (Monthly Active User)
- Example: 1000 users = $5.50/month

**Estimated cost for this workshop**: $0 (within Free Tier)

#### Next Steps

Bắt đầu với [Prerequisites](../5.2.2-prerequisites/)
