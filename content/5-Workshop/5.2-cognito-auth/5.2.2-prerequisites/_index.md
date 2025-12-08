---
title: "Prerequisites"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Prerequisites

## 1. Completed Workshops

- ✅ **Workshop 1**: Amplify Frontend deployed và hoạt động
- ✅ Frontend app URL: `https://main.xxxxx.amplifyapp.com`

## 2. AWS Permissions

Đảm bảo IAM user/role có permissions:
- `cognito-idp:CreateUserPool`
- `cognito-idp:CreateUserPoolClient`
- `cognito-idp:CreateGroup`
- `cognito-idp:AdminCreateUser`

## 3. Email for Testing

Cần ít nhất 3 email addresses để test 3 roles:
- `customer@example.com` - Customer role
- `shipper@example.com` - Shipper role
- `admin@example.com` - Admin role

{{% notice tip %}}
💡 **Tip**: Có thể dùng Gmail với alias: `youremail+customer@gmail.com`, `youremail+shipper@gmail.com`
{{% /notice %}}

## 4. Install AWS Amplify Libraries

Trong frontend project:

```powershell
cd coffee-cloud-frontend
npm install aws-amplify @aws-amplify/ui-react
```

## 5. Verify Current Setup

```powershell
# Check frontend is running
npm run dev

# Check Git status
git status

# Check AWS CLI (optional)
aws cognito-idp list-user-pools --max-results 10
```

## Next Steps

Tiếp tục với [Create Cognito User Pool](../5.2.3-create-user-pool/)
