# 📚 Next.js Full-Stack Portfolio - Complete Course Slides

**Course:** Web Development
**Project:** Week 2 - Portfolio with Database Integration
**Duration:** 5 hours (5 x 60-minute modules)
**Prerequisites:** Basic React knowledge, HTML/CSS fundamentals

---

# 🎯 Course Overview: Next.js Full-Stack Portfolio

**Duration:** 5 hours (5 x 60-minute modules)
**Prerequisites:** Basic React, HTML/CSS fundamentals

---

## 🚀 What You'll Build

A **full-stack portfolio website** featuring:
- ✨ Dynamic project showcase with database integration
- 🔧 RESTful API for CRUD operations
- 📱 Responsive design with Tailwind CSS
- 🚀 Production deployment on Vercel

---

## 📚 Learning Outcomes

By the end of this course, you will:

- **Master Next.js App Router** architecture
- **Understand server vs client** components
- **Build RESTful APIs** with proper error handling
- **Integrate PostgreSQL** databases using Prisma ORM
- **Deploy full-stack** applications to production

---

## 🏗️ Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Frontend** | Next.js 15 + React 18 | Server-side rendering & UI |
| **Styling** | Tailwind CSS 4.0 | Utility-first CSS framework |
| **Database** | PostgreSQL (Neon) | Relational data storage |
| **ORM** | Prisma | Type-safe database access |
| **Deployment** | Vercel | Edge deployment platform |
| **Testing** | Vitest | Unit and integration tests |

---

## 📋 Module Breakdown

1. **Module 1:** Next.js Architecture Fundamentals (60 min)
2. **Module 2:** Database Integration with Prisma (60 min)
3. **Module 3:** RESTful API Development (75 min)
4. **Module 4:** Full-Stack Integration (60 min)
5. **Module 5:** Advanced Component Development (90 min)

---

## 🎯 Assessment Overview

- **Technical Implementation** (70%) - Working API, components, integration
- **Code Quality** (20%) - Best practices, organization
- **Documentation & Testing** (10%) - Tests passing, clear README

**Total Project Value:** 100 points

---

# 📋 Module 1: Next.js Architecture Fundamentals

**Duration:** 60 minutes
**Objective:** Master the difference between server and client components

---

## 🎯 Learning Objectives

By the end of this module, students will:
- ✅ Understand the difference between server and client components
- ✅ Navigate the App Router file structure
- ✅ Implement dynamic routing with parameters
- ✅ Choose appropriate rendering strategies

---

## 🔍 Server vs Client Components

### Server Components (Default)
```javascript
// app/about/page.js - Runs on server
export default function About() {
  // ✅ Can access databases directly
  // ✅ Better SEO, smaller bundle size
  // ❌ Cannot use useState, useEffect, event handlers
  return <h1>About Me</h1>;
}
```

### Client Components (Opt-in)
```javascript
// app/projects/page.js - Runs in browser
'use client';
import { useState } from 'react';

export default function Projects() {
  const [showForm, setShowForm] = useState(false);
  // ✅ Can use React hooks, event handlers
  // ✅ Interactive features, state management
  // ❌ Larger bundle size
  return <button onClick={() => setShowForm(true)}>Add Project</button>;
}
```

---

## 🗂️ File-Based Routing

```
app/
├── page.js              → /
├── about/page.js        → /about
├── projects/
│   ├── page.js          → /projects
│   └── [id]/page.js     → /projects/123
└── api/
    └── projects/route.js → /api/projects (API endpoint)
```

**Key Concept:** File structure = URL structure

---

## 🛠️ Hands-On Exercise: Component Analysis

**Task (15 minutes):** Examine the starter project and identify:

1. **Find server components:**
   - `app/page.js` (Homepage)
   - `app/about/page.js`
   - `app/contact/page.js`

2. **Find client components:**
   - None initially - we'll create these!

3. **Identify routing patterns:**
   - Static routes: `/`, `/about`, `/contact`
   - Dynamic route: `/projects/[id]`
   - API routes: `/api/projects`

**Discussion:** Why is the homepage a server component?

---

## 🎮 Live Demo: Dynamic Routes

### Step 1: Create Dynamic Project Page
```javascript
// app/projects/[id]/page.js
export default function ProjectDetail({ params }) {
  const { id } = params;

  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold">Project {id}</h1>
      <p className="text-gray-600 mt-4">
        This will show details for project ID: {id}
      </p>
    </div>
  );
}
```

### Step 2: Test the Route
- Navigate to `/projects/1`, `/projects/hello`, `/projects/123`
- Notice how `params.id` captures the URL parameter

### Step 3: Add Navigation
```javascript
// app/projects/page.js
import Link from 'next/link';

export default function Projects() {
  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold mb-8">My Projects</h1>
      <div className="space-y-4">
        <Link href="/projects/1" className="block text-blue-600 hover:underline">
          View Project 1
        </Link>
        <Link href="/projects/2" className="block text-blue-600 hover:underline">
          View Project 2
        </Link>
      </div>
    </div>
  );
}
```

---

## ✅ Assessment Checkpoint

**Quick Check:**
1. What directive converts a component to client-side?
2. What file creates the route `/api/projects`?
3. How do you access URL parameters in `[id]` routes?

**Expected Answers:**
1. `'use client';`
2. `app/api/projects/route.js`
3. Through the `params` prop: `params.id`

---

## 🔑 Key Takeaways

- **Server Components** are the default and best for SEO
- **Client Components** are needed for interactivity
- **File structure** determines your app's routing
- **Dynamic routes** use `[param]` syntax
- **Choose wisely** between server and client rendering

---

# 📋 Module 2: Database Integration with Prisma

**Duration:** 60 minutes
**Objective:** Connect PostgreSQL database using Prisma ORM

---

## 🎯 Learning Objectives

By the end of this module, students will:
- ✅ Set up PostgreSQL database connections
- ✅ Design database schemas with Prisma
- ✅ Understand ORM concepts and benefits
- ✅ Manage database migrations and seeding

---

## 🤔 What is an ORM?

**Object-Relational Mapping** - Translates between database tables and JavaScript objects

### Without ORM (Raw SQL) ❌
```sql
SELECT * FROM projects WHERE id = 1;
INSERT INTO projects (title, description)
VALUES ('My App', 'A cool app');
```

### With Prisma ORM ✅
```javascript
const project = await prisma.project.findUnique({ where: { id: 1 } });
const newProject = await prisma.project.create({
  data: { title: 'My App', description: 'A cool app' }
});
```

**Benefits:** Type safety, auto-completion, migrations, query builder

---

## 🗃️ Database Schema Design

```prisma
// prisma/schema.prisma
model Project {
  id           Int      @id @default(autoincrement())
  title        String   // Required field
  description  String   // Required field
  imageUrl     String?  // Optional field (? = nullable)
  projectUrl   String?  // Optional field
  githubUrl    String?  // Optional field
  technologies String[] // Array of strings
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
}
```

**Key Concepts:**
- `@id` = Primary key
- `@default(autoincrement())` = Auto-incrementing ID
- `String?` = Optional/nullable field
- `String[]` = Array field
- `@updatedAt` = Automatically updates on change

---

## 🔐 Environment Variables

**Keep secrets safe with environment variables:**

```bash
# .env.local (never commit this!)
DATABASE_URL="postgresql://user:pass@host:5432/database?sslmode=require"
```

```javascript
// Access in your code
const databaseUrl = process.env.DATABASE_URL;
```

**Security Rules:**
- ✅ Use `.env.local` for local development
- ✅ Use platform environment variables for production
- ❌ Never commit `.env` files to Git
- ❌ Never hardcode credentials in source code

---

## 🛠️ Hands-On Exercise: Database Setup

### Step 1: Create Neon Database (10 minutes)
1. Go to [neon.tech](https://neon.tech)
2. Sign up with GitHub
3. Create new project: "portfolio-db"
4. Copy connection string

### Step 2: Configure Environment (5 minutes)
```bash
# Copy environment template
cp .env.example .env.local

# Add your database URL to .env.local
DATABASE_URL="your-neon-connection-string"
```

### Step 3: Initialize Database (5 minutes)
```bash
# Generate Prisma client
npm run db:generate

# Create tables in database
npm run db:push

# Add sample data
npm run db:seed
```

### Step 4: Explore with Prisma Studio (5 minutes)
```bash
npm run db:studio
```

Opens browser interface to view/edit database records

---

## 🚨 Troubleshooting Common Issues

| Error | Solution |
|-------|----------|
| ❌ "Connection refused" | Check DATABASE_URL format |
| ❌ "Prisma client not found" | Run `npm run db:generate` |
| ❌ "No schema found" | Run `npm run db:push` first |
| ❌ "Environment variable not found" | Check `.env.local` exists |

---

## 🎮 Live Demo: Database Operations

### Reading Data
```javascript
// Get all projects
const projects = await prisma.project.findMany();

// Get one project
const project = await prisma.project.findUnique({
  where: { id: 1 }
});

// Get projects with filtering
const reactProjects = await prisma.project.findMany({
  where: {
    technologies: {
      has: 'React' // Array contains 'React'
    }
  },
  orderBy: { createdAt: 'desc' }
});
```

### Writing Data
```javascript
// Create new project
const newProject = await prisma.project.create({
  data: {
    title: 'Todo App',
    description: 'A simple todo application',
    technologies: ['React', 'JavaScript'],
    githubUrl: 'https://github.com/user/todo-app'
  }
});

// Update existing project
const updated = await prisma.project.update({
  where: { id: 1 },
  data: { title: 'Updated Title' }
});
```

---

## 🔄 Database Commands Reference

```bash
# Development workflow commands
npm run db:generate    # Generate Prisma client after schema changes
npm run db:push       # Push schema changes to database
npm run db:seed       # Add sample data
npm run db:studio     # Open database browser

# Migration commands (production)
npx prisma migrate dev --name "add-projects"  # Create migration
npx prisma migrate deploy                     # Deploy migrations
```

---

## ✅ Assessment Checkpoint

**Quick Check:**
1. What file defines your database schema?
2. Which command creates tables from your schema?
3. How do you query all projects ordered by creation date?

**Expected Answers:**
1. `prisma/schema.prisma`
2. `npm run db:push`
3. `prisma.project.findMany({ orderBy: { createdAt: 'desc' } })`

---

## 🔑 Key Takeaways

- **Prisma ORM** provides type-safe database access
- **Environment variables** keep credentials secure
- **Schema-first** approach defines your data structure
- **Generated client** provides auto-completion and validation
- **Migrations** track database changes over time

---

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

---

# 📋 Module 4: Full-Stack Integration

**Duration:** 60 minutes
**Objective:** Connect React frontend to API backend

---

## 🎯 Learning Objectives

By the end of this module, students will:
- ✅ Connect React frontend to API backend
- ✅ Implement data fetching with proper loading states
- ✅ Handle form submissions and API errors
- ✅ Understand client-side state management patterns

---

## 🔄 Client vs Server Data Fetching

### Server Component Data Fetching (SSR)
```javascript
// Runs on server, during build/request
export default async function Projects() {
  const response = await fetch('http://localhost:3000/api/projects');
  const projects = await response.json();

  // Pre-rendered, good for SEO, immediate display
  return <ProjectList projects={projects} />;
}
```

### Client Component Data Fetching (CSR)
```javascript
// Runs in browser, after page loads
'use client';
export default function Projects() {
  const [projects, setProjects] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/projects')
      .then(res => res.json())
      .then(setProjects)
      .finally(() => setLoading(false));
  }, []);

  // Interactive, can show loading states
  return loading ? <Spinner /> : <ProjectList projects={projects} />;
}
```

**When to use each:**
- **Server fetching:** SEO important, data rarely changes
- **Client fetching:** Interactive features, real-time updates

---

## 🎛️ State Management Patterns

### The Three States of Data
```javascript
const [data, setData] = useState(null);       // Actual data
const [loading, setLoading] = useState(true);  // Loading state
const [error, setError] = useState(null);      // Error state
```

### Loading States UI/UX
```javascript
if (loading) {
  return (
    <div className="text-center py-12">
      <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600 mx-auto"></div>
      <p className="text-gray-600 mt-4">Loading projects...</p>
    </div>
  );
}
```

### Error States UI/UX
```javascript
if (error) {
  return (
    <div className="bg-red-50 border border-red-200 rounded-lg p-6">
      <h3 className="text-red-800 font-semibold">Something went wrong</h3>
      <p className="text-red-700 mt-2">{error}</p>
      <button
        onClick={fetchProjects}
        className="mt-4 px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700"
      >
        Try again
      </button>
    </div>
  );
}
```

---

## 🛠️ Hands-On Exercise: Frontend Integration

### Step 1: Convert Projects Page to Client Component

```javascript
// app/projects/page.js
'use client';

import { useState, useEffect } from 'react';
import Image from 'next/image';
import Link from 'next/link';

export default function Projects() {
  const [projects, setProjects] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  // TODO: Implement fetchProjects function
  // TODO: Add useEffect to fetch data on mount
  // TODO: Handle loading and error states
  // TODO: Display projects in grid layout
}
```

---

### Step 2: Implement Data Fetching

```javascript
const fetchProjects = async () => {
  try {
    setIsLoading(true);
    setError(null); // Clear previous errors

    const response = await fetch('/api/projects');

    if (!response.ok) {
      throw new Error(`Failed to load projects: ${response.status}`);
    }

    const data = await response.json();
    setProjects(data);
  } catch (error) {
    console.error('Error fetching projects:', error);
    setError(error.message);
  } finally {
    setIsLoading(false);
  }
};

useEffect(() => {
  fetchProjects();
}, []); // Empty dependency array = run once on mount
```

**Key Concepts:**
- `async/await` for readable async code
- `try/catch/finally` for error handling
- `response.ok` to check HTTP success
- `setError(null)` to clear previous errors

---

### Step 3: Render Different States

```javascript
// Loading state
if (isLoading) {
  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-4xl font-bold mb-8">My Projects</h1>
      <div className="text-center py-12">
        <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600 mx-auto"></div>
        <p className="text-gray-600 mt-4">Loading projects...</p>
      </div>
    </div>
  );
}

// Error state
if (error) {
  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-4xl font-bold mb-8">My Projects</h1>
      <div className="bg-red-50 border border-red-200 rounded-lg p-6">
        <h3 className="text-red-800 font-semibold">Failed to load projects</h3>
        <p className="text-red-700 mt-2">{error}</p>
        <button
          onClick={fetchProjects}
          className="mt-4 px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700 transition-colors"
        >
          Try again
        </button>
      </div>
    </div>
  );
}

// Success state - render projects
return (
  <div className="container mx-auto px-4 py-8">
    <h1 className="text-4xl font-bold mb-8">My Projects</h1>

    {projects.length === 0 ? (
      <p className="text-gray-600 text-center py-12">
        No projects found. Create your first project!
      </p>
    ) : (
      <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        {projects.map((project) => (
          <ProjectCard key={project.id} project={project} />
        ))}
      </div>
    )}
  </div>
);
```

---

## 📝 Form Handling Patterns

### Basic Form State Management
```javascript
const [formData, setFormData] = useState({
  title: '',
  description: '',
  technologies: []
});

const [isSubmitting, setIsSubmitting] = useState(false);
const [submitError, setSubmitError] = useState(null);

const handleChange = (e) => {
  setFormData(prev => ({
    ...prev,
    [e.target.name]: e.target.value
  }));
};
```

### Form Submission with API Integration
```javascript
const handleSubmit = async (e) => {
  e.preventDefault();

  try {
    setIsSubmitting(true);
    setSubmitError(null);

    const response = await fetch('/api/projects', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(formData)
    });

    if (!response.ok) {
      const errorData = await response.json();
      throw new Error(errorData.error || 'Failed to create project');
    }

    const newProject = await response.json();

    // Optimistic update - add to list immediately
    setProjects(prev => [newProject, ...prev]);

    // Reset form
    setFormData({ title: '', description: '', technologies: [] });

    // Close form modal/drawer
    setShowForm(false);

  } catch (error) {
    console.error('Error creating project:', error);
    setSubmitError(error.message);
  } finally {
    setIsSubmitting(false);
  }
};
```

---

## 🎮 Live Demo: Complete Integration

**Instructor demonstrates:**

1. **Convert static page to dynamic**
2. **Add loading spinner**
3. **Test error states** (disconnect database)
4. **Show optimistic updates** (add new project)
5. **Demonstrate real-time updates**

### Project Card Component Example
```javascript
function ProjectCard({ project }) {
  return (
    <div className="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow">
      {project.imageUrl && (
        <Image
          src={project.imageUrl}
          alt={project.title}
          width={400}
          height={200}
          className="w-full h-48 object-cover"
        />
      )}
      <div className="p-6">
        <h3 className="text-xl font-semibold mb-2">{project.title}</h3>
        <p className="text-gray-600 mb-4">{project.description}</p>

        <div className="flex flex-wrap gap-2 mb-4">
          {project.technologies.map((tech) => (
            <span
              key={tech}
              className="px-2 py-1 bg-blue-100 text-blue-800 text-sm rounded"
            >
              {tech}
            </span>
          ))}
        </div>

        <div className="flex gap-2">
          {project.projectUrl && (
            <a
              href={project.projectUrl}
              className="text-blue-600 hover:underline"
              target="_blank"
              rel="noopener noreferrer"
            >
              View Project
            </a>
          )}
          {project.githubUrl && (
            <a
              href={project.githubUrl}
              className="text-gray-600 hover:underline"
              target="_blank"
              rel="noopener noreferrer"
            >
              GitHub
            </a>
          )}
        </div>
      </div>
    </div>
  );
}
```

---

## 🔧 Error Handling Best Practices

### Client-Side Error Types
```javascript
// Network errors
if (!navigator.onLine) {
  setError('You appear to be offline. Check your connection.');
  return;
}

// HTTP errors
if (response.status === 404) {
  setError('The requested resource was not found.');
} else if (response.status === 500) {
  setError('Server error. Please try again later.');
} else if (!response.ok) {
  setError(`Request failed: ${response.status}`);
}

// Validation errors
const errorData = await response.json();
if (errorData.code === 'MISSING_TITLE') {
  setFieldError('title', 'Title is required');
}
```

### User-Friendly Error Messages
```javascript
const getErrorMessage = (error) => {
  if (error.message.includes('fetch')) {
    return 'Unable to connect to server. Check your internet connection.';
  }
  if (error.message.includes('404')) {
    return 'The project you\'re looking for doesn\'t exist.';
  }
  if (error.message.includes('500')) {
    return 'Something went wrong on our end. We\'re working to fix it.';
  }
  return error.message;
};
```

---

## ✅ Assessment Checkpoint

**Quick Check:**
1. What React hook fetches data after component mounts?
2. How do you handle loading states in React?
3. What's an "optimistic update"?

**Expected Answers:**
1. useEffect with empty dependency array `[]`
2. useState for loading boolean + conditional rendering
3. Updating UI immediately, before server confirms success

---

## 🔑 Key Takeaways

- **Client components** enable interactive features
- **Loading states** improve perceived performance
- **Error handling** creates better user experience
- **Optimistic updates** make apps feel faster
- **State management** is crucial for complex UIs

---

# 📋 Module 5: Advanced Component Development

**Duration:** 90 minutes
**Objective:** Build complex, reusable components with advanced patterns

---

## 🎯 Learning Objectives

By the end of this module, students will:
- ✅ Build complex form components with validation
- ✅ Implement reusable UI components
- ✅ Handle advanced user interactions
- ✅ Apply component composition patterns

---

## 🧩 Component Composition Principles

### ❌ Monolithic Component (Hard to maintain)
```javascript
function ProjectPage() {
  return (
    <div>
      {/* 300+ lines of form, validation, state management, UI */}
      {/* Impossible to reuse, test, or debug */}
    </div>
  );
}
```

### ✅ Composed Components (Much better)
```javascript
function ProjectPage() {
  return (
    <div>
      <ProjectForm onSubmit={handleCreate} />
      <ProjectList projects={projects} />
    </div>
  );
}

function ProjectForm({ onSubmit }) {
  return (
    <form onSubmit={onSubmit}>
      <TitleInput />
      <DescriptionInput />
      <TechnologyInput />
    </form>
  );
}
```

**Benefits:**
- Easier to test individual pieces
- Reusable across different pages
- Simpler debugging and maintenance
- Clear separation of concerns

---

## 🔍 Form Validation Patterns

### Validation Strategy
```javascript
const validateForm = (data) => {
  const errors = {};

  // Required field validation
  if (!data.title || data.title.trim() === '') {
    errors.title = 'Title is required';
  }

  if (!data.description || data.description.trim() === '') {
    errors.description = 'Description is required';
  }

  // Array validation
  if (!data.technologies || data.technologies.length === 0) {
    errors.technologies = 'Add at least one technology';
  }

  // URL validation
  const urlPattern = /^https?:\/\/.+\..+/;
  if (data.projectUrl && !urlPattern.test(data.projectUrl)) {
    errors.projectUrl = 'Enter a valid URL (include http:// or https://)';
  }

  if (data.githubUrl && !urlPattern.test(data.githubUrl)) {
    errors.githubUrl = 'Enter a valid GitHub URL';
  }

  return errors;
};

// Usage
const errors = validateForm(formData);
const isValid = Object.keys(errors).length === 0;
```

---

## 🛠️ Hands-On Exercise: ProjectForm Component

**Students build a complete form component with validation, error handling, and proper state management**

*[Full implementation code from Module 5 slide 06-advanced-components.md]*

---

## 🏷️ Advanced Component: TechnologyInput

**Students build a complex input component with dynamic array management**

*[Full implementation code from Module 5 slide 06-advanced-components.md]*

---

## 🔗 Component Integration

**Final integration in Projects page showing how all components work together**

---

## 🧪 Testing Your Components

**Run the test suite to verify everything works:**

```bash
npm test
```

**Tests verify:**
- ✅ Form component exists and renders
- ✅ Form validation works correctly
- ✅ Technology input handles arrays properly
- ✅ Form submission integrates with API
- ✅ Error states display correctly
- ✅ Loading states work as expected

---

## 🎨 Advanced Patterns Learned

### 1. Controlled Components
```javascript
// Component controls its own state via props
<input
  value={formData.title}
  onChange={(e) => setFormData({...formData, title: e.target.value})}
/>
```

### 2. Compound Components
```javascript
// Components work together but are separate
<ProjectForm>
  <TitleInput />
  <TechnologyInput />
  <SubmitButton />
</ProjectForm>
```

### 3. Error Boundaries
```javascript
// Clear errors when user interacts
if (errors[name]) {
  setErrors(prev => ({...prev, [name]: undefined}));
}
```

### 4. Optimistic Updates
```javascript
// Update UI immediately, handle errors later
setProjects(prev => [newProject, ...prev]);
```

---

## ✅ Final Assessment

**Students test complete application:**

1. **Form functionality:**
   - ✅ Can open/close form modal
   - ✅ Form validation displays errors
   - ✅ Can add/remove technologies
   - ✅ Successful submission updates project list

2. **API integration:**
   - ✅ Data loads from database on page load
   - ✅ New projects appear immediately after creation
   - ✅ Error states display with retry options

3. **User experience:**
   - ✅ Loading states provide feedback
   - ✅ Error messages are helpful and clear
   - ✅ Form resets after successful submission

---

## 🔑 Key Takeaways

- **Component composition** makes complex UIs manageable
- **Form validation** provides better user experience
- **State management** patterns scale as apps grow
- **Error handling** at component level improves UX
- **Testing** ensures components work as expected

---

# 🎯 Course Wrap-Up & Next Steps

## 🏆 What Students Have Built
- **Full-stack web application** with database
- **RESTful API** with proper error handling
- **Interactive React components** with validation
- **Production-ready code** following best practices

---

## 📈 Skills Acquired
- **Next.js App Router** architecture
- **Server vs Client** component patterns
- **Database integration** with Prisma ORM
- **API development** following REST principles
- **React state management** and form handling
- **Modern deployment** practices

---

## 🚀 Deployment & Production

**Students should deploy their projects:**

1. **Push to GitHub:**
```bash
git add .
git commit -m "Complete portfolio project"
git push
```

2. **Deploy to Vercel:**
   - Connect GitHub repository
   - Set environment variables
   - Deploy with automatic builds

3. **Test production:**
   - Verify database connection
   - Test all functionality
   - Check responsive design

---

## 📚 Further Learning

**Recommended next topics:**
- **Authentication** (NextAuth.js)
- **File uploads** (AWS S3, Cloudinary)
- **Real-time features** (WebSockets)
- **Advanced styling** (Framer Motion)
- **Testing strategies** (Jest, Playwright)
- **Performance optimization** (caching, CDN)

---

## 🔧 Common Issues & Solutions

**During Development:**
- Environment variables not loading → Restart dev server
- Prisma client errors → Run `npm run db:generate`
- API not connecting → Check dev server is running
- Form not submitting → Check network tab for errors

**During Deployment:**
- Build failures → Check for TypeScript errors
- Database connection issues → Verify environment variables
- Missing dependencies → Check package.json

---

## 📋 Assessment Rubric

### Technical Implementation (70 points)
- **Database Schema** (15 pts) - Proper Prisma model with validation
- **API Routes** (25 pts) - All 5 endpoints with error handling
- **Component Development** (20 pts) - Working form with validation
- **Integration** (10 pts) - Frontend connects to backend properly

### Code Quality (20 points)
- **Best Practices** (10 pts) - Proper error handling, validation
- **Code Organization** (10 pts) - Clean components, proper file structure

### Documentation & Testing (10 points)
- **All tests passing** (5 pts) - Automated test suite passes
- **README completion** (5 pts) - Clear setup instructions

### Total: 100 points

---

# 📋 Project Extensions & AI Enhancement Recommendations

Based on the current Next.js portfolio project, here are strategic recommendations for extending the project with AI and modern features.

---

## 🤖 AI Integration Opportunities

### 1. Project Description AI Assistant
- Generate professional project descriptions using OpenAI API
- Multiple suggestion options
- Seamless integration into project form

### 2. Smart Technology Tag Suggestions
- AI-powered technology recommendations based on project description
- Pattern matching and intelligent suggestions

### 3. Portfolio Content AI Generator
- Generate "About Me" sections
- Create professional bios
- Streaming content for better UX

---

## 🚀 Feature Extensions

### 4. Real-time Collaboration
- WebSocket integration
- Live project updates
- Multi-user editing

### 5. Advanced Analytics Dashboard
- Chart.js visualization
- Technology usage statistics
- Portfolio performance metrics

### 6. Dark Mode with System Preference
- Tailwind dark mode integration
- localStorage persistence
- System preference detection

### 7. Project Performance Monitoring
- Load time tracking
- Lighthouse score integration
- Performance metrics dashboard

---

## 🛠️ Implementation Strategy

### Phase 1: AI Content Assistant (Week 1)
1. Set up OpenAI API integration
2. Build description generator component
3. Add technology suggestions feature
4. Test with real content

### Phase 2: Analytics & Monitoring (Week 2)
1. Add analytics database schema
2. Implement tracking components
3. Build dashboard with charts
4. Add performance monitoring

### Phase 3: Advanced Features (Week 3)
1. Implement dark mode with preferences
2. Add real-time features (optional)
3. Build admin dashboard (optional)
4. Deploy with monitoring

---

## 📚 Learning Outcomes Extension

### Additional Skills Students Will Gain:

**AI Integration:**
- Working with external APIs
- Streaming responses
- Prompt engineering
- Error handling for AI services

**Advanced React:**
- Context API for theme management
- Performance optimization
- Real-time data handling
- Chart library integration

**Full-Stack Development:**
- Analytics and monitoring
- Performance tracking
- Advanced database schemas
- Production deployment considerations

---

## 🚀 Production Considerations

### Environment Variables Needed:
```bash
# .env.local
DATABASE_URL="your-database-url"
OPENAI_API_KEY="your-openai-key"
NEXTAUTH_SECRET="your-auth-secret"
ANALYTICS_API_KEY="your-analytics-key"
```

### Deployment Checklist:
- [ ] Set up environment variables in Vercel
- [ ] Configure database connection pooling
- [ ] Set up error monitoring (Sentry)
- [ ] Configure analytics tracking
- [ ] Test AI API rate limits
- [ ] Set up caching for AI responses

---

# 🎓 Course Complete!

Thank you for participating in this Next.js Full-Stack Portfolio course. You now have the skills to build modern, production-ready web applications!

**Happy coding! 🚀**
