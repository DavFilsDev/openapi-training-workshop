# 🎯 Exercise 2 - Authentication & Security API Specification

## 📋 Objective
Create a complete OpenAPI specification for a User Authentication API with JWT security and protected endpoints.

## 🚀 Requirements

### **Endpoints to Implement:**

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| `POST` | `/auth/register` | Create new user account | None |
| `POST` | `/auth/login` | Login and get JWT token | None |
| `GET` | `/auth/profile` | Get current user profile | Required |
| `PUT` | `/auth/profile` | Update user profile | Required |
| `GET` | `/auth/users` | List all users (Admin only) | Required + Admin |

### **Data Models:**
```yaml
User:
  type: object
  required:
    - username
    - email
    - password
  properties:
    id:
      type: integer
      format: int64
      readOnly: true
    username:
      type: string
      minLength: 3
      maxLength: 50
      pattern: '^[a-zA-Z0-9_]+$'
      example: "john_doe"
    email:
      type: string
      format: email
      example: "john@example.com"
    password:
      type: string
      format: password
      minLength: 6
      writeOnly: true
      example: "secure123"
    role:
      type: string
      enum: [user, admin]
      default: "user"
    created_at:
      type: string
      format: date-time
      readOnly: true

LoginRequest:
  type: object
  required:
    - username
    - password
  properties:
    username:
      type: string
      example: "john_doe"
    password:
      type: string
      format: password
      example: "secure123"

LoginResponse:
  type: object
  properties:
    access_token:
      type: string
      example: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    token_type:
      type: string
      default: "bearer"
    expires_in:
      type: integer
      example: 3600
```

### **Authentication Scheme:**
```yaml
BearerAuth:
  type: http
  scheme: bearer
  bearerFormat: JWT
```

### **Validation Rules:**
- ✅ **Username**: 3-50 chars, alphanumeric + underscore only
- ✅ **Email**: Must be valid email format
- ✅ **Password**: Minimum 6 characters
- ✅ **Role**: Must be either "user" or "admin"

### **Example Requests:**

**POST /auth/register**
```json
{
  "username": "jane_smith",
  "email": "jane@example.com",
  "password": "password123",
  "role": "user"
}
```

**POST /auth/login**
```json
{
  "username": "jane_smith",
  "password": "password123"
}
```

**PUT /auth/profile** (requires Authorization header)
```json
{
  "email": "new_email@example.com"
}
```

### **Expected Responses:**
- `201 Created` - User successfully registered
- `200 OK` - Login successful or profile retrieved
- `400 Bad Request` - Validation error
- `401 Unauthorized` - Missing or invalid token
- `403 Forbidden` - Insufficient permissions (admin only)
- `404 Not Found` - User not found
- `409 Conflict` - Username or email already exists

## 🎯 Learning Goals

- Implement JWT Bearer authentication scheme
- Use securitySchemes in components
- Apply security requirements to endpoints
- Handle password security (writeOnly, format: password)
- Manage different user roles and permissions
- Implement proper error handling for auth failures

## 📝 Your Task

Create a file `my-solution.yml` with complete OpenAPI specification including:
- ✅ JWT Bearer authentication scheme definition
- ✅ All authentication endpoints with proper security
- ✅ User and Login schemas in components
- ✅ Role-based access control (admin vs user)
- ✅ Proper error responses for auth failures
- ✅ Validation rules for user input

## 💡 Tips

1. Define the security scheme first in components
2. Use `security` array to protect endpoints
3. Remember `writeOnly: true` for password fields
4. Use `enum` for role validation
5. Include examples for both success and error cases

## 🔍 Validation Checklist

- [ ] JWT Bearer auth scheme properly defined
- [ ] Endpoints have correct security requirements
- [ ] Password fields are writeOnly and format: password
- [ ] Role validation with enum
- [ ] Proper error codes for auth failures (401, 403)
- [ ] Email format validation
- [ ] Admin-only endpoint properly secured

---

**Time Estimate:** 60-75 minutes  
**Difficulty Level:** Intermediate
