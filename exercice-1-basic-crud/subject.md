# 🎯 Exercise 1 - Basic CRUD API Specification

## 📋 Objective
Create a complete OpenAPI specification for a simple Product Management API with full CRUD operations.

## 🚀 Requirements

### **Endpoints to Implement:**

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/products` | Get all products |
| `POST` | `/products` | Create a new product |
| `GET` | `/products/{id}` | Get a specific product |
| `PUT` | `/products/{id}` | Update a product |
| `DELETE` | `/products/{id}` | Delete a product |

### **Data Model:**
```yaml
Product:
  type: object
  required:
    - name
    - price
    - category
  properties:
    id:
      type: integer
      format: int64
      readOnly: true
      description: Auto-generated product ID
    name:
      type: string
      minLength: 2
      maxLength: 100
      example: "Wireless Headphones"
    price:
      type: number
      format: float
      minimum: 0
      exclusiveMinimum: true
      example: 99.99
    description:
      type: string
      nullable: true
      example: "High-quality wireless headphones with noise cancellation"
    category:
      type: string
      enum: [electronics, clothing, books, home]
      example: "electronics"
    in_stock:
      type: boolean
      default: true
    created_at:
      type: string
      format: date-time
      readOnly: true
```

### **Validation Rules:**
- ✅ **Price**: Must be greater than 0
- ✅ **Name**: Must be 2-100 characters long
- ✅ **Category**: Must be one of: electronics, clothing, books, home
- ✅ **ID**: Must be positive integer in path parameters

### **Example Requests:**

**POST /products**
```json
{
  "name": "Laptop",
  "price": 1299.99,
  "category": "electronics",
  "description": "Gaming laptop with RGB keyboard"
}
```

**PUT /products/123**
```json
{
  "name": "Updated Laptop",
  "price": 1199.99,
  "category": "electronics",
  "description": "Updated description",
  "in_stock": false
}
```

### **Expected Responses:**
- `201 Created` - Product successfully created
- `200 OK` - Product retrieved or updated successfully
- `400 Bad Request` - Validation error
- `404 Not Found` - Product not found
- `500 Internal Server Error` - Server error

## 🎯 Learning Goals

- Define path parameters and endpoints
- Create request and response schemas
- Implement basic data validation
- Handle error responses properly
- Use enums and readOnly properties
- Structure components section

## 📝 Your Task

Create a file `my-solution.yml` with complete OpenAPI specification including:
- ✅ Info section with API metadata
- ✅ All required endpoints with proper parameters
- ✅ Product schema in components
- ✅ Proper response definitions
- ✅ Error handling examples
- ✅ Validation rules enforcement

## 💡 Tips

1. Start with the basic OpenAPI structure
2. Define the Product schema first in components
3. Add endpoints one by one
4. Test your YAML syntax regularly
5. Use the template provided in `/templates/` if needed

## 🔍 Validation Checklist

- [ ] All endpoints are implemented
- [ ] Schema validation rules are enforced
- [ ] Proper HTTP status codes are used
- [ ] Examples are provided for requests/responses
- [ ] No syntax errors in YAML file
- [ ] Components are properly organized

---

**Time Estimate:** 45-60 minutes  
**Difficulty Level:** Beginner