# 🎯 Exercise 6 - Advanced Validation & Complex Business Logic API Specification

## 📋 Objective
Create a complete OpenAPI specification for an E-commerce API with complex validation rules, business logic constraints, and advanced data relationships.

## 🚀 Requirements

### **Endpoints to Implement:**

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| `POST` | `/orders` | Create a new order | Required |
| `GET` | `/orders` | List user's orders | Required |
| `GET` | `/orders/{order_id}` | Get order details | Required |
| `PUT` | `/orders/{order_id}/cancel` | Cancel order | Required |
| `POST` | `/payments` | Process payment | Required |
| `GET` | `/products` | List products with inventory | Optional |
| `POST` | `/coupons/validate` | Validate coupon code | Optional |
| `GET` | `/users/{user_id}/stats` | Get user statistics | Required + Admin |

### **Data Models:**
```yaml
Order:
  type: object
  required:
    - user_id
    - items
    - shipping_address
  properties:
    id:
      type: string
      format: uuid
      readOnly: true
    user_id:
      type: integer
      format: int64
      readOnly: true
    status:
      type: string
      enum: [pending, confirmed, processing, shipped, delivered, cancelled, refunded]
      default: "pending"
      readOnly: true
    items:
      type: array
      items:
        $ref: '#/components/schemas/OrderItem'
      minItems: 1
      maxItems: 20
    total_amount:
      type: number
      format: decimal
      minimum: 0
      readOnly: true
    discount_amount:
      type: number
      format: decimal
      minimum: 0
      default: 0
    tax_amount:
      type: number
      format: decimal
      minimum: 0
      readOnly: true
    final_amount:
      type: number
      format: decimal
      minimum: 0
      readOnly: true
    shipping_address:
      $ref: '#/components/schemas/Address'
    billing_address:
      $ref: '#/components/schemas/Address'
    coupon_code:
      type: string
      nullable: true
    created_at:
      type: string
      format: date-time
      readOnly: true
    updated_at:
      type: string
      format: date-time
      readOnly: true

OrderItem:
  type: object
  required:
    - product_id
    - quantity
    - price
  properties:
    product_id:
      type: integer
      format: int64
    product_name:
      type: string
      readOnly: true
    quantity:
      type: integer
      minimum: 1
      maximum: 10
    price:
      type: number
      format: decimal
      minimum: 0
    subtotal:
      type: number
      format: decimal
      minimum: 0
      readOnly: true

Address:
  type: object
  required:
    - street
    - city
    - postal_code
    - country
  properties:
    street:
      type: string
      maxLength: 200
    city:
      type: string
      maxLength: 100
    postal_code:
      type: string
      pattern: '^[A-Z0-9\- ]+$'
    country:
      type: string
      enum: [US, CA, UK, FR, DE, AU]
    state:
      type: string
      nullable: true
      maxLength: 100

Payment:
  type: object
  required:
    - order_id
    - payment_method
    - amount
  properties:
    id:
      type: string
      format: uuid
      readOnly: true
    order_id:
      type: string
      format: uuid
    payment_method:
      type: string
      enum: [credit_card, paypal, stripe, bank_transfer]
    amount:
      type: number
      format: decimal
      minimum: 0.01
    currency:
      type: string
      pattern: '^[A-Z]{3}$'
      default: "USD"
    status:
      type: string
      enum: [pending, processing, completed, failed, refunded]
      default: "pending"
      readOnly: true
    card_last4:
      type: string
      pattern: '^\d{4}$'
      nullable: true
    created_at:
      type: string
      format: date-time
      readOnly: true

CouponValidation:
  type: object
  properties:
    valid:
      type: boolean
    discount_type:
      type: string
      enum: [percentage, fixed_amount]
    discount_value:
      type: number
      format: decimal
      minimum: 0
    min_order_amount:
      type: number
      format: decimal
      nullable: true
    message:
      type: string
```

### **Complex Validation Rules:**

**Order Validation:**
- ✅ Minimum order amount: $10.00
- ✅ Maximum order amount: $5000.00
- ✅ Stock validation: Product must be in stock
- ✅ Quantity validation: Cannot exceed available stock
- ✅ Address validation: Billing address required for certain payment methods

**Payment Validation:**
- ✅ Payment amount must match order final amount (±1% tolerance)
- ✅ Credit card payments require card details
- ✅ Currency must match user's region

**Business Logic Constraints:**
- ✅ Orders can only be cancelled within 1 hour of creation
- ✅ Refunds only possible for orders in specific statuses
- ✅ Coupon codes have minimum order amount requirements
- ✅ Certain products have quantity limits per user

### **Example Requests:**

**POST /orders**
```json
{
  "user_id": 123,
  "items": [
    {
      "product_id": 456,
      "quantity": 2
    }
  ],
  "shipping_address": {
    "street": "123 Main St",
    "city": "New York",
    "postal_code": "10001",
    "country": "US",
    "state": "NY"
  },
  "billing_address": {
    "street": "123 Main St",
    "city": "New York",
    "postal_code": "10001",
    "country": "US",
    "state": "NY"
  },
  "coupon_code": "SUMMER2024"
}
```

**POST /payments**
```json
{
  "order_id": "550e8400-e29b-41d4-a716-446655440000",
  "payment_method": "credit_card",
  "amount": 99.99,
  "currency": "USD",
  "card_last4": "4242"
}
```

**POST /coupons/validate**
```json
{
  "coupon_code": "SUMMER2024",
  "order_amount": 150.00
}
```

### **Expected Responses:**
- `201 Created` - Order/payment created successfully
- `200 OK` - Operation completed successfully
- `400 Bad Request` - Validation error or business rule violation
- `402 Payment Required` - Payment processing failed
- `409 Conflict` - Order cannot be modified in current state
- `422 Unprocessable Entity` - Business logic validation failed
- `429 Too Many Requests` - Too many payment attempts

## 🎯 Learning Goals

- Implement complex cross-field validation
- Design business logic constraints in OpenAPI
- Handle monetary values with decimal formatting
- Create conditional validation rules
- Implement read-only computed fields
- Manage state transitions with enums
- Design comprehensive error responses

## 📝 Your Task

Create a file `my-solution.yml` with complete OpenAPI specification including:
- ✅ Complex validation rules with custom error messages
- ✅ Business logic constraints implementation
- ✅ Monetary value handling with decimal format
- ✅ State management with enum transitions
- ✅ Cross-field validation dependencies
- ✅ Conditional requirements based on payment methods
- ✅ Comprehensive error response schemas

## 💡 Tips

1. Use `format: decimal` for monetary values
2. Implement `readOnly: true` for computed fields
3. Use `pattern` for postal code and card number validation
4. Create custom error codes for business rule violations
5. Use `oneOf`/`anyOf` for conditional validation
6. Implement rate limiting for payment endpoints

## 🔍 Validation Checklist

- [ ] Complex order validation rules implemented
- [ ] Payment amount matching with tolerance
- [ ] Address validation based on country
- [ ] Stock and quantity validation
- [ ] Coupon validation with minimum order amounts
- [ ] State transition rules for orders
- [ ] Custom error messages for business rules
- [ ] Decimal formatting for monetary values
- [ ] Conditional field requirements

---

**Time Estimate:** 100-120 minutes  
**Difficulty Level:** Expert