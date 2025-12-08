---
title: "Testing & Verification"
weight: 6
chapter: false
pre: " <b> 5.2.6 </b> "
---

# Testing & Verification

## 1. Test Signup Flow

### 1.1 Create New Account

1. Navigate to `/signup`
2. Fill form:
   - Name: `Test Customer`
   - Email: `testcustomer@example.com`
   - Password: `TestPass123!`
3. Click **Sign Up**
4. Should redirect to verify email page

### 1.2 Verify Email

**Option A: Using real email**
- Check inbox for verification code
- Enter code on verification page

**Option B: Using Cognito Console**
1. Cognito → Users → Find user
2. Status: `UNCONFIRMED` → Click user
3. Actions → **Confirm account**

## 2. Test Login Flow

### 2.1 Login as Customer

```
Email: customer@coffeecloud.com
Password: <temp password from Cognito>
```

After first login, might need to change password.

### 2.2 Verify Customer Dashboard

- ✅ Dashboard shows "Customer Dashboard"
- ✅ Can see Order History and Loyalty Points
- ✅ Cannot access Admin features

### 2.3 Login as Shipper

```
Email: shipper@coffeecloud.com
Password: <temp password>
```

- ✅ Dashboard shows "Shipper Dashboard"
- ✅ Can see Available Orders
- ✅ Cannot access Admin features

### 2.4 Login as Admin

```
Email: admin@coffeecloud.com
Password: <temp password>
```

- ✅ Dashboard shows "Admin Dashboard"
- ✅ Can see Manage Products, Orders, Users
- ✅ Full access to all features

## 3. Test Protected Routes

### 3.1 Without Login

1. Logout
2. Try accessing `/order` or `/dashboard`
3. Should redirect to `/login` ✅

### 3.2 With Login

1. Login as any user
2. Can access protected routes ✅

## 4. Test Token Persistence

### 4.1 Refresh Page

1. Login
2. Refresh browser (F5)
3. Should still be logged in ✅

### 4.2 Check LocalStorage

Open DevTools → Application → Local Storage:
```
CognitoIdentityServiceProvider.<client-id>.LastAuthUser
CognitoIdentityServiceProvider.<client-id>.<username>.idToken
CognitoIdentityServiceProvider.<client-id>.<username>.accessToken
CognitoIdentityServiceProvider.<client-id>.<username>.refreshToken
```

## 5. Test Token Expiration

### 5.1 Wait for Token Expiry

Tokens expire after 60 minutes. Test:
1. Login
2. Wait 61 minutes
3. Try accessing protected route
4. Should auto-refresh token or redirect to login

## 6. Test Role-Based Access

### 6.1 Add Role Check to Route

Update `App.jsx`:

```jsx
<Route
  path="/admin"
  element={
    <ProtectedRoute allowedGroups={['Admin']}>
      <AdminPanel />
    </ProtectedRoute>
  }
/>
```

### 6.2 Test Access

- Admin user: Can access ✅
- Customer user: Shows "Access Denied" ✅
- Shipper user: Shows "Access Denied" ✅

## 7. Test Cognito Console

### 7.1 View Users

1. Cognito Console → Users
2. Should see all created users
3. Check Status: `CONFIRMED` or `FORCE_CHANGE_PASSWORD`

### 7.2 Check User Groups

1. Click on user → Group memberships
2. Verify correct group assignment

### 7.3 View Sign-in Activity

- Last sign-in date
- Number of sign-ins
- Device information

## 8. Test Error Handling

### 8.1 Wrong Password

```
Email: customer@coffeecloud.com
Password: WrongPassword123
```

Should show error: "Incorrect username or password" ✅

### 8.2 Unconfirmed Email

Try login with unconfirmed email → Should show error or redirect to verify

### 8.3 Weak Password on Signup

Try password: `test123`
Should show: "Password does not meet requirements" ✅

## 9. Performance Testing

### 9.1 Login Speed

- Login should complete in < 2 seconds ✅

### 9.2 Token Validation

- Protected route check should be instant (< 100ms) ✅

## 10. Security Checklist

- [ ] Passwords are not logged in console
- [ ] Tokens are stored securely (httpOnly ideal, but localStorage acceptable)
- [ ] API calls include Authorization header
- [ ] Users cannot access other users' data
- [ ] Admin panel accessible only by Admins
- [ ] Logout clears all tokens

## 11. Cleanup (Optional)

If you want to delete users:

```powershell
aws cognito-idp admin-delete-user `
  --user-pool-id us-east-1_xxxxxxxxx `
  --username testcustomer@example.com
```

Delete User Pool:
1. Cognito Console → User pools
2. Select pool → Actions → Delete
3. Type `delete` to confirm

{{% notice warning %}}
⚠️ **Warning**: Deleting User Pool will delete ALL users and cannot be undone!
{{% /notice %}}

## 🎉 Congratulations!

**Workshop 2 Complete! You've learned:**
- ✅ Create Amazon Cognito User Pool
- ✅ Configure multi-role user groups
- ✅ Integrate Cognito with React
- ✅ Implement JWT authentication
- ✅ Build role-based dashboards
- ✅ Handle auth errors and edge cases

## Next Workshop

Continue to **Workshop 3: Elastic Beanstalk Backend** để tạo backend API với .NET!
