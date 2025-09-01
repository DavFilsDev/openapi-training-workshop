# 🎯 Exercise 4 - File Upload & Download API Specification

## 📋 Objective
Create a complete OpenAPI specification for a File Management API that handles file uploads, downloads, and metadata management with proper validation and security.

## 🚀 Requirements

### **Endpoints to Implement:**

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| `POST` | `/files/upload` | Upload single file | Required |
| `POST` | `/files/upload-multiple` | Upload multiple files | Required |
| `GET` | `/files` | List user's files | Required |
| `GET` | `/files/{file_id}` | Get file metadata | Required |
| `GET` | `/files/{file_id}/download` | Download file | Required |
| `PUT` | `/files/{file_id}` | Update file metadata | Required |
| `DELETE` | `/files/{file_id}` | Delete file | Required |

### **Data Models:**
```yaml
File:
  type: object
  properties:
    id:
      type: string
      format: uuid
      readOnly: true
      example: "550e8400-e29b-41d4-a716-446655440000"
    filename:
      type: string
      example: "document.pdf"
    original_name:
      type: string
      example: "my_document.pdf"
    size:
      type: integer
      format: int64
      readOnly: true
      example: 1048576
    mime_type:
      type: string
      readOnly: true
      example: "application/pdf"
    extension:
      type: string
      readOnly: true
      example: "pdf"
    owner_id:
      type: integer
      format: int64
      readOnly: true
    is_public:
      type: boolean
      default: false
    tags:
      type: array
      items:
        type: string
      example: ["documents", "important"]
    created_at:
      type: string
      format: date-time
      readOnly: true
    updated_at:
      type: string
      format: date-time
      readOnly: true

FileUploadResponse:
  type: object
  properties:
    file:
      $ref: '#/components/schemas/File'
    download_url:
      type: string
      format: uri
      example: "/files/550e8400-e29b-41d4-a716-446655440000/download"

FilesListResponse:
  type: object
  properties:
    files:
      type: array
      items:
        $ref: '#/components/schemas/File'
    total_count:
      type: integer
      example: 25
```

### **File Type Restrictions:**
```yaml
Allowed file types:
  - images: ["image/jpeg", "image/png", "image/gif", "image/webp"]
  - documents: ["application/pdf", "application/msword", "application/vnd.openxmlformats-officedocument.wordprocessingml.document"]
  - archives: ["application/zip", "application/x-rar-compressed"]
  - text: ["text/plain", "text/csv", "application/json"]

Max file size: 10MB (10,485,760 bytes)
Max multiple files: 5 files per request
```

### **Request Bodies:**

**POST /files/upload**
```yaml
multipart/form-data:
  schema:
    type: object
    properties:
      file:
        type: string
        format: binary
        description: File to upload
      is_public:
        type: boolean
        default: false
      tags:
        type: array
        items:
          type: string
```

**POST /files/upload-multiple**
```yaml
multipart/form-data:
  schema:
    type: object
    properties:
      files:
        type: array
        items:
          type: string
          format: binary
      is_public:
        type: boolean
        default: false
      tags:
        type: array
        items:
          type: string
```

### **Query Parameters for GET /files:**
- `page`: integer, min: 1, default: 1
- `limit`: integer, min: 1, max: 50, default: 20
- `tag`: string (filter by tag)
- `sort_by`: string, enum: [filename, size, created_at, updated_at], default: created_at
- `sort_order`: string, enum: [asc, desc], default: desc

### **Validation Rules:**
- ✅ **File size**: Max 10MB per file
- ✅ **File types**: Only allowed MIME types
- ✅ **Multiple files**: Max 5 files per request
- ✅ **Filename**: Must be valid filename characters
- ✅ **Tags**: Array of strings, max 10 tags per file

### **Expected Responses:**
- `201 Created` - File uploaded successfully
- `200 OK` - File metadata retrieved or updated
- `400 Bad Request` - Invalid file type/size or validation error
- `401 Unauthorized` - Authentication required
- `403 Forbidden` - Access to file denied
- `404 Not Found` - File not found
- `413 Payload Too Large` - File too large

## 🎯 Learning Goals

- Implement multipart/form-data for file uploads
- Handle file type and size validation
- Manage multiple file uploads
- Create download endpoints with proper responses
- Implement file metadata management
- Use format: binary for file content
- Handle security for file access

## 📝 Your Task

Create a file `my-solution.yml` with complete OpenAPI specification including:
- ✅ Multipart form data for upload endpoints
- ✅ File validation (size, type, quantity)
- ✅ File metadata schema with proper types
- ✅ Download endpoint with binary response
- ✅ Authentication requirements for all endpoints
- ✅ Proper error handling for file operations

## 💡 Tips

1. Use `format: binary` for file upload parameters
2. Define allowed MIME types in descriptions
3. Use `format: uuid` for file IDs
4. Implement proper security for file downloads
5. Include examples for different file types

## 🔍 Validation Checklist

- [ ] Multipart form data properly defined
- [ ] File size validation implemented
- [ ] MIME type restrictions specified
- [ ] Multiple file upload support
- [ ] Download endpoint with binary response
- [ ] File metadata management endpoints
- [ ] Proper error codes for file validation failures
- [ ] Authentication required for all operations

---

**Time Estimate:** 80-95 minutes  
**Difficulty Level:** Intermediate/Advanced