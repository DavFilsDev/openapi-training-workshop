# OpenAPI Training Workshop 🚀

A comprehensive training repository to master OpenAPI specification through practical exercises.

## 📁 Repository Structure

```
openapi-training-workshop/
│
├── exercise-1-basic-crud/
│   ├── subject.md          # Exercise instructions
│   ├── solution.yml        # Complete solution
│   └── my-solution.yml     # Your attempt
│
├── exercise-2-authentication/
│   ├── subject.md
│   ├── solution.yml
│   └── my-solution.yml
│
├── exercise-3-pagination-filters/
│   ├── subject.md
│   ├── solution.yml
│   └── my-solution.yml
│
├── exercise-4-file-upload/
│   ├── subject.md
│   ├── solution.yml
│   └── my-solution.yml
│
├── exercise-5-webhooks-events/
│   ├── subject.md
│   ├── solution.yml
│   └── my-solution.yml
│
├── exercise-6-advanced-validation/
│   ├── subject.md
│   ├── solution.yml
│   └── my-solution.yml
│
├── templates/
│   ├── basic-template.yml  # Starter template
│   └── advanced-template.yml
│
├── resources/
│   ├── openapi-cheatsheet.md
│   └── best-practices.md
│
└── README.md
```

## 🎯 Exercises Overview

### 1. **Basic CRUD API** 
   - Fundamental OpenAPI syntax
   - Path parameters, request/response schemas
   - Simple data validation

### 2. **Authentication System**
   - JWT Bearer tokens
   - Security schemes
   - Protected endpoints

### 3. **Pagination & Filters**
   - Query parameters
   - Advanced filtering
   - Sorting and pagination

### 4. **File Upload API**
   - Multipart form data
   - File type validation
   - Size limitations

### 5. **Webhooks & Events**
   - Callback URLs
   - Event-driven architecture
   - Webhook management

### 6. **Advanced Validation**
   - Complex data constraints
   - Custom validation rules
   - Business logic in specs

## 🚀 How to Use This Repository

1. **Start with Exercise 1**
   ```bash
   cd exercise-1-basic-crud/
   read subject.md
   # Create your solution in my-solution.yml
   ```

2. **Compare with Solution**
   ```bash
   # After completing your attempt
   diff my-solution.yml solution.yml
   ```

3. **Move to Next Exercise**
   ```bash
   cd ../exercise-2-authentication/
   ```

## 🛠️ Prerequisites

- Basic understanding of REST APIs
- Text editor (VS Code recommended)
- OpenAPI extension (optional but helpful)
- Yaml linting tool

## 📚 Learning Path

1. **Beginner**: Exercises 1-2
2. **Intermediate**: Exercises 3-4
3. **Advanced**: Exercises 5-6

## 💡 Tips for Success

- **Read the subject carefully** before starting
- **Use the templates** if you get stuck
- **Validate your YAML** regularly
- **Compare with solutions** to learn best practices
- **Take notes** of new concepts learned

## 🔧 Validation Tools

Validate your OpenAPI files with:

```bash
# Using npm package
npx @redocly/cli lint my-solution.yml

# Using online validator
# https://editor.swagger.io/
```

## 🎓 Learning Objectives

By completing all exercises, you'll master:

- ✅ OpenAPI 3.0.x syntax
- ✅ Schema design and validation
- ✅ Authentication patterns
- ✅ Advanced filtering and pagination
- ✅ File handling specifications
- ✅ Webhook implementations
- ✅ Industry best practices

## 🤝 Contributing

This is a personal training repository. Feel free to:
- Add your own exercises
- Improve existing solutions
- Share your learning experience

## 📝 License

This repository is for educational purposes. Use it to enhance your OpenAPI skills!
