# 🎯 Exercise 3 - Pagination, Filtering & Search API Specification

## 📋 Objective
Create a complete OpenAPI specification for an Articles API with advanced querying capabilities including pagination, filtering, sorting, and search.

## 🚀 Requirements

### **Endpoints to Implement:**

| Method | Endpoint | Description | Query Parameters |
|--------|----------|-------------|------------------|
| `GET` | `/articles` | Get articles with filtering | `page`, `limit`, `author`, `category`, `status`, `sort_by`, `sort_order`, `date_from`, `date_to` |
| `POST` | `/articles` | Create new article | None |
| `GET` | `/articles/{id}` | Get specific article | None |
| `PUT` | `/articles/{id}` | Update article | None |
| `DELETE` | `/articles/{id}` | Delete article | None |
| `GET` | `/articles/search` | Full-text search | `q`, `page`, `limit` |

### **Data Models:**
```yaml
Article:
  type: object
  required:
    - title
    - content
    - author_id
    - category
  properties:
    id:
      type: integer
      format: int64
      readOnly: true
    title:
      type: string
      minLength: 5
      maxLength: 200
      example: "Introduction to OpenAPI"
    content:
      type: string
      minLength: 10
      example: "OpenAPI is a powerful specification for REST APIs..."
    author_id:
      type: integer
      format: int64
      example: 123
    category:
      type: string
      enum: [technology, science, arts, business, health]
      example: "technology"
    status:
      type: string
      enum: [draft, published, archived]
      default: "draft"
    tags:
      type: array
      items:
        type: string
      example: ["api", "documentation", "rest"]
    published_at:
      type: string
      format: date-time
      nullable: true
    created_at:
      type: string
      format: date-time
      readOnly: true
    updated_at:
      type: string
      format: date-time
      readOnly: true

ArticlesResponse:
  type: object
  properties:
    articles:
      type: array
      items:
        $ref: '#/components/schemas/Article'
    pagination:
      $ref: '#/components/schemas/PaginationMeta'

PaginationMeta:
  type: object
  properties:
    total:
      type: integer
      example: 150
    page:
      type: integer
      example: 1
    limit:
      type: integer
      example: 10
    total_pages:
      type: integer
      example: 15
    has_next:
      type: boolean
      example: true
    has_prev:
      type: boolean
      example: false
```

### **Query Parameters Specification:**

**For GET /articles:**
- `page`: integer, minimum: 1, default: 1
- `limit`: integer, minimum: 1, maximum: 100, default: 10
- `author`: integer (filter by author_id)
- `category`: string, enum: [technology, science, arts, business, health]
- `status`: string, enum: [draft, published, archived]
- `date_from`: string, format: date (filter articles created after)
- `date_to`: string, format: date (filter articles created before)
- `sort_by`: string, enum: [created_at, updated_at, title, published_at], default: created_at
- `sort_order`: string, enum: [asc, desc], default: desc

**For GET /articles/search:**
- `q`: string, minLength: 2 (search query)
- `page`: integer, minimum: 1, default: 1
- `limit`: integer, minimum: 1, maximum: 50, default: 10

### **Validation Rules:**
- ✅ **Title**: 5-200 characters
- ✅ **Content**: Minimum 10 characters
- ✅ **Category**: Must be valid enum value
- ✅ **Status**: Must be valid enum value
- ✅ **Page/Limit**: Positive integers with reasonable limits

### **Example Requests:**

**GET /articles?page=2&limit=20&category=technology&status=published&sort_by=published_at&sort_order=desc**

**GET /articles/search?q=openapi+tutorial&page=1&limit=15**

**POST /articles**
```json
{
  "title": "Advanced OpenAPI Techniques",
  "content": "In this article, we explore advanced OpenAPI features...",
  "author_id": 456,
  "category": "technology",
  "tags": ["openapi", "swagger", "documentation"],
  "status": "draft"
}
```

### **Expected Responses:**
- `200 OK` - Articles retrieved successfully (with pagination metadata)
- `201 Created` - Article created successfully
- `400 Bad Request` - Invalid query parameters or validation error
- `404 Not Found` - Article not found
- `500 Internal Server Error` - Server error

## 🎯 Learning Goals

- Implement complex query parameters with validation
- Create pagination systems with metadata
- Design filtering and sorting mechanisms
- Build search functionality
- Use array types and enum validations
- Structure nested response objects
- Handle date filtering and sorting

## 📝 Your Task

Create a file `my-solution.yml` with complete OpenAPI specification including:
- ✅ All endpoints with comprehensive query parameters
- ✅ Article schema with proper validation
- ✅ Pagination metadata structure
- ✅ Filtering parameters with enum validation
- ✅ Search endpoint with full-text search capability
- ✅ Proper error handling for invalid queries

## 💡 Tips

1. Define query parameters as reusable components if possible
2. Use `default` values for common parameters
3. Implement reasonable `minimum`/`maximum` for pagination
4. Use `enum` for all categorical filters
5. Include examples for complex query combinations

## 🔍 Validation Checklist

- [ ] All query parameters properly defined and validated
- [ ] Pagination metadata included in response
- [ ] Filtering by category, status, author works
- [ ] Date range filtering implemented
- [ ] Sorting with multiple fields and directions
- [ ] Full-text search endpoint functional
- [ ] Proper error handling for invalid parameters
- [ ] Reasonable limits on pagination (max 100 items per page)

---

**Time Estimate:** 75-90 minutes  
**Difficulty Level:** Intermediate