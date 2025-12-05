# 📋 Module 3: RESTful API Development

**Duration:** 75 minutes  
**Objective:** Build complete CRUD API with proper error handling

---

## 🎯 Learning Objectives

By the end of this module, students will:
- ✅ Understand RESTful API principles
- ✅ Build CRUD endpoints with proper error handling
- ✅ Implement request validation and status codes
- ✅ Test APIs using browser and development tools

---

## 🌐 REST Principles

**REpresentational State Transfer** - A design pattern for web APIs

### HTTP Methods Map to Operations

| Method | Endpoint | Purpose | Status Code |
|--------|----------|---------|-------------|
| `GET` | `/api/projects` | Read all projects | `200` OK |
| `GET` | `/api/projects/1` | Read specific project | `200` OK |
| `POST` | `/api/projects` | Create new project | `201` Created |
| `PUT` | `/api/projects/1` | Update existing project | `200` OK |
| `DELETE` | `/api/projects/1` | Remove project | `200` OK |

### Status Codes Have Meaning
- `200` OK - Successful GET, PUT, DELETE
- `201` Created - Successful POST
- `400` Bad Request - Invalid data sent
- `404` Not Found - Resource doesn't exist
- `500` Server Error - Something went wrong

---

## 🏗️ API Route Structure in Next.js

```javascript
// app/api/projects/route.js
export async function GET() {
  // Handle GET /api/projects
}

export async function POST(request) {
  // Handle POST /api/projects
  // request.json() to get body data
}

// app/api/projects/[id]/route.js
export async function GET(request, { params }) {
  // Handle GET /api/projects/123
  const { id } = params; // Extract URL parameter
}
```

**Key Concepts:**
- One file = one endpoint
- Export functions for each HTTP method
- `params` object contains URL parameters
- `request` object contains body, headers, etc.

---

## 🛠️ Hands-On Exercise: API Implementation

Students implement all 5 endpoints step by step:

### 1. GET /api/projects (Read All)

```javascript
// app/api/projects/route.js
import { PrismaClient } from '@prisma/client';
import { NextResponse } from 'next/server';

const prisma = new PrismaClient();

export async function GET() {
  try {
    const projects = await prisma.project.findMany({
      orderBy: { createdAt: 'desc' }
    });
    return NextResponse.json(projects);
  } catch (error) {
    console.error('Error fetching projects:', error);
    return NextResponse.json(
      { error: 'Failed to fetch projects' },
      { status: 500 }
    );
  }
}
```

---

## 📝 POST /api/projects (Create)

```javascript
export async function POST(request) {
  try {
    const body = await request.json();
    const { title, description, imageUrl, projectUrl, githubUrl, technologies } = body;
    
    // Validation
    if (!title || !description || !technologies?.length) {
      return NextResponse.json(
        { error: 'Missing required fields: title, description, technologies' },
        { status: 400 }
      );
    }
    
    const project = await prisma.project.create({
      data: {
        title,
        description,
        imageUrl,
        projectUrl,
        githubUrl,
        technologies
      }
    });
    
    return NextResponse.json(project, { status: 201 });
  } catch (error) {
    console.error('Error creating project:', error);
    return NextResponse.json(
      { error: 'Failed to create project' },
      { status: 500 }
    );
  }
}
```

---

## 🔍 GET /api/projects/[id] (Read One)

```javascript
// app/api/projects/[id]/route.js
export async function GET(request, { params }) {
  try {
    const id = parseInt(params.id);
    
    // Validate ID format
    if (isNaN(id)) {
      return NextResponse.json(
        { error: 'Invalid project ID' },
        { status: 400 }
      );
    }
    
    const project = await prisma.project.findUnique({
      where: { id: id }
    });
    
    if (!project) {
      return NextResponse.json(
        { error: 'Project not found' },
        { status: 404 }
      );
    }
    
    return NextResponse.json(project);
  } catch (error) {
    console.error('Error fetching project:', error);
    return NextResponse.json(
      { error: 'Failed to fetch project' },
      { status: 500 }
    );
  }
}
```

---

## ✏️ PUT /api/projects/[id] (Update)

```javascript
export async function PUT(request, { params }) {
  try {
    const id = parseInt(params.id);
    const body = await request.json();
    
    if (isNaN(id)) {
      return NextResponse.json(
        { error: 'Invalid project ID' },
        { status: 400 }
      );
    }
    
    const { title, description, imageUrl, projectUrl, githubUrl, technologies } = body;
    
    const project = await prisma.project.update({
      where: { id: id },
      data: {
        title,
        description,
        imageUrl,
        projectUrl,
        githubUrl,
        technologies
      }
    });
    
    return NextResponse.json(project);
  } catch (error) {
    if (error.code === 'P2025') { // Prisma "record not found"
      return NextResponse.json(
        { error: 'Project not found' },
        { status: 404 }
      );
    }
    return NextResponse.json(
      { error: 'Failed to update project' },
      { status: 500 }
    );
  }
}
```

---

## 🗑️ DELETE /api/projects/[id] (Delete)

```javascript
export async function DELETE(request, { params }) {
  try {
    const id = parseInt(params.id);
    
    if (isNaN(id)) {
      return NextResponse.json(
        { error: 'Invalid project ID' },
        { status: 400 }
      );
    }
    
    await prisma.project.delete({
      where: { id: id }
    });
    
    return NextResponse.json({ 
      message: 'Project deleted successfully' 
    });
  } catch (error) {
    if (error.code === 'P2025') {
      return NextResponse.json(
        { error: 'Project not found' },
        { status: 404 }
      );
    }
    return NextResponse.json(
      { error: 'Failed to delete project' },
      { status: 500 }
    );
  }
}
```

---

## 🧪 API Testing Methods

### 1. Browser Testing (GET only)
```
http://localhost:3000/api/projects
http://localhost:3000/api/projects/1
```

### 2. DevTools Network Tab
- Open browser DevTools (F12)
- Go to Network tab
- Make requests and inspect responses

### 3. curl Commands (All methods)
```bash
# Test GET
curl http://localhost:3000/api/projects

# Test POST
curl -X POST http://localhost:3000/api/projects \
  -H "Content-Type: application/json" \
  -d '{"title":"Test Project","description":"A test","technologies":["React"]}'

# Test PUT
curl -X PUT http://localhost:3000/api/projects/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Updated Project","description":"Updated desc","technologies":["React","Next.js"]}'

# Test DELETE
curl -X DELETE http://localhost:3000/api/projects/1
```

---

## 🔧 Error Handling Patterns

### Standard Error Response Format
```javascript
{
  "error": "Human-readable error message",
  "code": "MACHINE_READABLE_CODE", // Optional
  "details": { /* Additional context */ } // Optional
}
```

### Common Error Scenarios
```javascript
// Validation errors
if (!title) {
  return NextResponse.json(
    { error: 'Title is required', code: 'MISSING_TITLE' },
    { status: 400 }
  );
}

// Not found errors
if (error.code === 'P2025') {
  return NextResponse.json(
    { error: 'Project not found' },
    { status: 404 }
  );
}

// Server errors (catch-all)
return NextResponse.json(
  { error: 'Internal server error' },
  { status: 500 }
);
```

---

## ✅ Assessment Checkpoint

**Quick Check:**
1. What HTTP method creates a new resource?
2. What status code indicates successful creation?
3. How do you handle "record not found" in Prisma?

**Expected Answers:**
1. POST
2. 201 Created
3. Catch Prisma error code 'P2025' and return 404

---

## 🔑 Key Takeaways

- **REST APIs** follow predictable patterns
- **HTTP methods** map to CRUD operations
- **Status codes** communicate results clearly
- **Error handling** is crucial for good UX
- **Validation** prevents bad data in your database