---
title: "Integrate with React Frontend"
weight: 5
chapter: false
pre: " <b> 5.2.5 </b> "
---

# Tích hợp Cognito với React Frontend

## 1. Install Dependencies

```powershell
cd coffee-cloud-frontend
npm install aws-amplify @aws-amplify/ui-react
```

---

## 2. Configure Amplify

### 2.1 Create aws-config.js

Tạo file `src/aws-config.js`:

```javascript
const awsConfig = {
  Auth: {
    region: 'us-east-1',
    userPoolId: 'us-east-1_xxxxxxxxx', // ← Paste your User Pool ID
    userPoolWebClientId: 'abcdefghijklmnopqrstuvwxyz', // ← Paste your Client ID
    authenticationFlowType: 'USER_SRP_AUTH',
  }
};

export default awsConfig;
```

### 2.2 Initialize Amplify

Update `src/main.jsx`:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Amplify } from 'aws-amplify'
import App from './App.jsx'
import awsConfig from './aws-config'
import './index.css'
import 'bootstrap/dist/css/bootstrap.min.css'

// Configure Amplify
Amplify.configure(awsConfig)

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

---

## 3. Create Auth Context

### 3.1 Create AuthContext.jsx

Tạo file `src/context/AuthContext.jsx`:

```jsx
import React, { createContext, useState, useEffect, useContext } from 'react';
import { Auth } from 'aws-amplify';

const AuthContext = createContext();

export const useAuth = () => useContext(AuthContext);

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [userGroup, setUserGroup] = useState(null);

  useEffect(() => {
    checkUser();
  }, []);

  const checkUser = async () => {
    try {
      const currentUser = await Auth.currentAuthenticatedUser();
      setUser(currentUser);
      
      // Get user groups from JWT token
      const groups = currentUser.signInUserSession.accessToken.payload['cognito:groups'];
      setUserGroup(groups ? groups[0] : null); // Get first group (highest precedence)
    } catch (error) {
      setUser(null);
      setUserGroup(null);
    } finally {
      setLoading(false);
    }
  };

  const signIn = async (email, password) => {
    try {
      const user = await Auth.signIn(email, password);
      setUser(user);
      
      // Get groups
      const groups = user.signInUserSession.accessToken.payload['cognito:groups'];
      setUserGroup(groups ? groups[0] : null);
      
      return { success: true, user };
    } catch (error) {
      console.error('Sign in error:', error);
      return { success: false, error: error.message };
    }
  };

  const signUp = async (email, password, name) => {
    try {
      const { user } = await Auth.signUp({
        username: email,
        password,
        attributes: {
          email,
          name,
        },
      });
      return { success: true, user };
    } catch (error) {
      console.error('Sign up error:', error);
      return { success: false, error: error.message };
    }
  };

  const confirmSignUp = async (email, code) => {
    try {
      await Auth.confirmSignUp(email, code);
      return { success: true };
    } catch (error) {
      console.error('Confirm sign up error:', error);
      return { success: false, error: error.message };
    }
  };

  const signOut = async () => {
    try {
      await Auth.signOut();
      setUser(null);
      setUserGroup(null);
      return { success: true };
    } catch (error) {
      console.error('Sign out error:', error);
      return { success: false, error: error.message };
    }
  };

  const changePassword = async (oldPassword, newPassword) => {
    try {
      const user = await Auth.currentAuthenticatedUser();
      await Auth.changePassword(user, oldPassword, newPassword);
      return { success: true };
    } catch (error) {
      console.error('Change password error:', error);
      return { success: false, error: error.message };
    }
  };

  const forgotPassword = async (email) => {
    try {
      await Auth.forgotPassword(email);
      return { success: true };
    } catch (error) {
      console.error('Forgot password error:', error);
      return { success: false, error: error.message };
    }
  };

  const forgotPasswordSubmit = async (email, code, newPassword) => {
    try {
      await Auth.forgotPasswordSubmit(email, code, newPassword);
      return { success: true };
    } catch (error) {
      console.error('Forgot password submit error:', error);
      return { success: false, error: error.message };
    }
  };

  const value = {
    user,
    userGroup,
    loading,
    signIn,
    signUp,
    confirmSignUp,
    signOut,
    changePassword,
    forgotPassword,
    forgotPasswordSubmit,
    checkUser,
  };

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
};
```

---

## 4. Wrap App with AuthProvider

Update `src/App.jsx`:

```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { AuthProvider } from './context/AuthContext';
import Navbar from './components/Navbar';
import Footer from './components/Footer';
import Home from './pages/Home';
import Menu from './pages/Menu';
import Order from './pages/Order';
import Login from './pages/Login';
import Signup from './pages/Signup';
import VerifyEmail from './pages/VerifyEmail';
import Dashboard from './pages/Dashboard';
import ProtectedRoute from './components/ProtectedRoute';
import './App.css';

function App() {
  return (
    <AuthProvider>
      <Router>
        <div className="d-flex flex-column min-vh-100">
          <Navbar />
          <main className="flex-grow-1">
            <Routes>
              <Route path="/" element={<Home />} />
              <Route path="/menu" element={<Menu />} />
              <Route path="/login" element={<Login />} />
              <Route path="/signup" element={<Signup />} />
              <Route path="/verify-email" element={<VerifyEmail />} />
              
              {/* Protected routes */}
              <Route
                path="/order"
                element={
                  <ProtectedRoute>
                    <Order />
                  </ProtectedRoute>
                }
              />
              <Route
                path="/dashboard"
                element={
                  <ProtectedRoute>
                    <Dashboard />
                  </ProtectedRoute>
                }
              />
            </Routes>
          </main>
          <Footer />
        </div>
      </Router>
    </AuthProvider>
  );
}

export default App;
```

---

## 5. Create ProtectedRoute Component

Tạo `src/components/ProtectedRoute.jsx`:

```jsx
import React from 'react';
import { Navigate } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

const ProtectedRoute = ({ children, allowedGroups }) => {
  const { user, userGroup, loading } = useAuth();

  if (loading) {
    return (
      <div className="container mt-5 text-center">
        <div className="spinner-border" role="status">
          <span className="visually-hidden">Loading...</span>
        </div>
      </div>
    );
  }

  if (!user) {
    return <Navigate to="/login" />;
  }

  // Check if user's group is allowed
  if (allowedGroups && !allowedGroups.includes(userGroup)) {
    return (
      <div className="container mt-5">
        <div className="alert alert-danger">
          <h4>Access Denied</h4>
          <p>You don't have permission to access this page.</p>
          <p>Your role: <strong>{userGroup || 'No group'}</strong></p>
        </div>
      </div>
    );
  }

  return children;
};

export default ProtectedRoute;
```

---

## 6. Update Login Page

Thay thế `src/pages/Login.jsx`:

```jsx
import React, { useState } from 'react';
import { useNavigate, Link } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

function Login() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();
  const { signIn } = useAuth();

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError('');
    setLoading(true);

    const result = await signIn(email, password);

    if (result.success) {
      navigate('/dashboard');
    } else {
      if (result.error.includes('User is not confirmed')) {
        navigate('/verify-email', { state: { email } });
      } else if (result.error.includes('NEW_PASSWORD_REQUIRED')) {
        // Handle force change password
        setError('You must change your password. Contact admin.');
      } else {
        setError(result.error);
      }
    }

    setLoading(false);
  };

  return (
    <div className="container mt-5">
      <div className="row justify-content-center">
        <div className="col-md-6">
          <div className="card">
            <div className="card-body">
              <h3 className="card-title text-center mb-4">Login to Coffee Cloud</h3>
              
              {error && (
                <div className="alert alert-danger" role="alert">
                  {error}
                </div>
              )}

              <form onSubmit={handleSubmit}>
                <div className="mb-3">
                  <label className="form-label">Email</label>
                  <input
                    type="email"
                    className="form-control"
                    value={email}
                    onChange={(e) => setEmail(e.target.value)}
                    required
                    disabled={loading}
                  />
                </div>
                <div className="mb-3">
                  <label className="form-label">Password</label>
                  <input
                    type="password"
                    className="form-control"
                    value={password}
                    onChange={(e) => setPassword(e.target.value)}
                    required
                    disabled={loading}
                  />
                </div>
                <button
                  type="submit"
                  className="btn btn-primary w-100"
                  disabled={loading}
                >
                  {loading ? 'Signing in...' : 'Login'}
                </button>
              </form>

              <hr />

              <p className="text-center mt-3">
                <Link to="/forgot-password">Forgot password?</Link>
              </p>
              <p className="text-center">
                Don't have an account? <Link to="/signup">Sign up</Link>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

export default Login;
```

---

## 7. Create Signup Page

Tạo `src/pages/Signup.jsx`:

```jsx
import React, { useState } from 'react';
import { useNavigate, Link } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

function Signup() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    password: '',
    confirmPassword: '',
  });
  const [error, setError] = useState('');
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();
  const { signUp } = useAuth();

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value,
    });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError('');

    if (formData.password !== formData.confirmPassword) {
      setError('Passwords do not match');
      return;
    }

    if (formData.password.length < 8) {
      setError('Password must be at least 8 characters');
      return;
    }

    setLoading(true);

    const result = await signUp(formData.email, formData.password, formData.name);

    if (result.success) {
      navigate('/verify-email', { state: { email: formData.email } });
    } else {
      setError(result.error);
    }

    setLoading(false);
  };

  return (
    <div className="container mt-5">
      <div className="row justify-content-center">
        <div className="col-md-6">
          <div className="card">
            <div className="card-body">
              <h3 className="card-title text-center mb-4">Sign Up for Coffee Cloud</h3>

              {error && (
                <div className="alert alert-danger" role="alert">
                  {error}
                </div>
              )}

              <form onSubmit={handleSubmit}>
                <div className="mb-3">
                  <label className="form-label">Full Name</label>
                  <input
                    type="text"
                    name="name"
                    className="form-control"
                    value={formData.name}
                    onChange={handleChange}
                    required
                    disabled={loading}
                  />
                </div>
                <div className="mb-3">
                  <label className="form-label">Email</label>
                  <input
                    type="email"
                    name="email"
                    className="form-control"
                    value={formData.email}
                    onChange={handleChange}
                    required
                    disabled={loading}
                  />
                </div>
                <div className="mb-3">
                  <label className="form-label">Password</label>
                  <input
                    type="password"
                    name="password"
                    className="form-control"
                    value={formData.password}
                    onChange={handleChange}
                    required
                    disabled={loading}
                  />
                  <small className="form-text text-muted">
                    At least 8 characters with uppercase, lowercase, and numbers
                  </small>
                </div>
                <div className="mb-3">
                  <label className="form-label">Confirm Password</label>
                  <input
                    type="password"
                    name="confirmPassword"
                    className="form-control"
                    value={formData.confirmPassword}
                    onChange={handleChange}
                    required
                    disabled={loading}
                  />
                </div>
                <button
                  type="submit"
                  className="btn btn-primary w-100"
                  disabled={loading}
                >
                  {loading ? 'Creating account...' : 'Sign Up'}
                </button>
              </form>

              <hr />

              <p className="text-center mt-3">
                Already have an account? <Link to="/login">Login</Link>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

export default Signup;
```

---

## 8. Create Dashboard (Role-based UI)

Tạo `src/pages/Dashboard.jsx`:

```jsx
import React from 'react';
import { useAuth } from '../context/AuthContext';
import { useNavigate } from 'react-router-dom';

function Dashboard() {
  const { user, userGroup, signOut } = useAuth();
  const navigate = useNavigate();

  const handleSignOut = async () => {
    await signOut();
    navigate('/login');
  };

  const renderDashboardByRole = () => {
    switch (userGroup) {
      case 'Admin':
        return (
          <div>
            <h2>Admin Dashboard</h2>
            <p>Manage products, orders, and users</p>
            <div className="row mt-4">
              <div className="col-md-4">
                <div className="card">
                  <div className="card-body">
                    <h5>Manage Products</h5>
                    <button className="btn btn-primary">View Products</button>
                  </div>
                </div>
              </div>
              <div className="col-md-4">
                <div className="card">
                  <div className="card-body">
                    <h5>View Orders</h5>
                    <button className="btn btn-primary">All Orders</button>
                  </div>
                </div>
              </div>
              <div className="col-md-4">
                <div className="card">
                  <div className="card-body">
                    <h5>Manage Users</h5>
                    <button className="btn btn-primary">User List</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        );

      case 'Shipper':
        return (
          <div>
            <h2>Shipper Dashboard</h2>
            <p>View and manage deliveries</p>
            <div className="alert alert-info">
              <h5>Available Orders</h5>
              <p>You have 3 pending deliveries</p>
              <button className="btn btn-primary">View Orders</button>
            </div>
          </div>
        );

      case 'Customer':
      default:
        return (
          <div>
            <h2>Customer Dashboard</h2>
            <p>Browse menu and place orders</p>
            <div className="row mt-4">
              <div className="col-md-6">
                <div className="card">
                  <div className="card-body">
                    <h5>Order History</h5>
                    <p>View your past orders</p>
                    <button className="btn btn-primary">View Orders</button>
                  </div>
                </div>
              </div>
              <div className="col-md-6">
                <div className="card">
                  <div className="card-body">
                    <h5>Loyalty Points</h5>
                    <p>You have <strong>250 points</strong></p>
                    <button className="btn btn-success">Redeem</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        );
    }
  };

  return (
    <div className="container mt-5">
      <div className="row">
        <div className="col-md-12">
          <div className="d-flex justify-content-between align-items-center mb-4">
            <div>
              <h1>Welcome, {user?.attributes?.name || user?.username}!</h1>
              <p className="text-muted">
                Role: <span className="badge bg-primary">{userGroup || 'No Group'}</span>
              </p>
            </div>
            <button className="btn btn-danger" onClick={handleSignOut}>
              Sign Out
            </button>
          </div>

          {renderDashboardByRole()}
        </div>
      </div>
    </div>
  );
}

export default Dashboard;
```

---

## 9. Update Navbar với Auth State

Update `src/components/Navbar.jsx`:

```jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

function Navbar() {
  const { user, userGroup, signOut } = useAuth();

  return (
    <nav className="navbar navbar-expand-lg navbar-dark bg-dark">
      <div className="container">
        <Link className="navbar-brand" to="/">
          ☕ Coffee Cloud
        </Link>
        <button
          className="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
        >
          <span className="navbar-toggler-icon"></span>
        </button>
        <div className="collapse navbar-collapse" id="navbarNav">
          <ul className="navbar-nav ms-auto">
            <li className="nav-item">
              <Link className="nav-link" to="/">Home</Link>
            </li>
            <li className="nav-item">
              <Link className="nav-link" to="/menu">Menu</Link>
            </li>
            
            {user ? (
              <>
                <li className="nav-item">
                  <Link className="nav-link" to="/order">Order</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="/dashboard">
                    Dashboard {userGroup && `(${userGroup})`}
                  </Link>
                </li>
                <li className="nav-item">
                  <button
                    className="nav-link btn btn-link"
                    onClick={() => signOut()}
                  >
                    Logout
                  </button>
                </li>
              <>
            ) : (
              <>
                <li className="nav-item">
                  <Link className="nav-link" to="/login">Login</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="/signup">Sign Up</Link>
                </li>
              </>
            )}
          </ul>
        </div>
      </div>
    </nav>
  );
}

export default Navbar;
```

---

## 10. Test Locally

```powershell
npm run dev
```

Test:
1. Sign up new user
2. Verify email (check console for code if using Cognito test emails)
3. Login với user đã tạo
4. Check dashboard hiển thị đúng role
5. Test logout

---

## 11. Deploy to Amplify

```powershell
git add .
git commit -m "Add Cognito authentication with multi-role support"
git push
```

Amplify sẽ tự động build và deploy (2-3 phút)

---

## Next Steps

Tiếp tục với [Testing & Verification](../5.2.6-testing/)
