# 🤖 AI Coding Instructions - Next.js Portfolio with Database

## 🎯 Project Overview

This is a **Next.js 15 full-stack portfolio application** built for educational purposes. The project demonstrates modern web development patterns including server-side rendering, API development, database integration, and component-based architecture.

**Tech Stack:**
- **Frontend:** Next.js 15 + React 18 + Tailwind CSS 4.0
- **Backend:** Next.js API routes + Prisma ORM
- **Database:** PostgreSQL (Neon)
- **Testing:** Vitest + Testing Library
- **Deployment:** Vercel

---

## 🏗️ Architecture Patterns

### Server vs Client Component Strategy
This project follows Next.js App Router patterns with intentional component placement:

- **Server Components (Default):** Used for pages that primarily display data (`app/about/page.js`, `app/contact/page.js`)
- **Client Components:** Used only when interactivity is needed (`app/projects/page.js` for form handling)

```javascript
// Server component example (default)
export default function About() {
  // Can access database directly, better SEO
  return <AboutContent />;
}

// Client component (when needed)
'use client';
export default function Projects() {
  const [showForm, setShowForm] = useState(false);
  // Interactive state management
}
```

### Database Schema Design
The project uses a simple but extensible Project model:

```prisma
model Project {
  id           Int      @id @default(autoincrement())
  title        String   // Required
  description  String   // Required  
  imageUrl     String?  // Optional
  projectUrl   String?  // Optional
  githubUrl    String?  // Optional
  technologies String[] // Array field for tags
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
}
```

**Key Patterns:**
- Use `String?` for optional fields
- Use `String[]` for tag/array data
- Include `createdAt`/`updatedAt` for audit trails

---

## 🔧 Development Workflows

### Database Management Commands
```bash
# Essential workflow commands (use these frequently)
npm run db:generate    # After schema changes
npm run db:push       # Sync schema to database
npm run db:seed       # Add sample data
npm run db:studio     # Visual database browser

# Development server
npm run dev           # Start with Turbopack for speed
```

### Testing Strategy
```bash
npm test              # Run all tests
npm run test:watch    # Watch mode during development
```

**Critical:** Always run tests after implementing features. The test suite validates:
- API endpoints return correct status codes
- Components render without errors
- Form validation works properly
- Database operations complete successfully

---

## 🗂️ File Structure Patterns

### API Route Organization
```
app/api/
├── projects/
│   ├── route.js           # GET /api/projects, POST /api/projects
│   └── [id]/
│       └── route.js       # GET, PUT, DELETE /api/projects/[id]
```

**Pattern:** One file per endpoint, export functions for each HTTP method.

### Component Organization
```
app/projects/
├── page.js                # Main projects page
├── [id]/
│   └── page.js           # Individual project detail
└── components/
    ├── ProjectForm.js     # Form component
    └── TechnologyInput.js # Specialized input component
```

**Pattern:** Keep components close to where they're used, create `/components` folders for reusable parts.

---

## 💡 Implementation Guidelines

### Error Handling Pattern
**API Routes:** Always use this error handling structure:
```javascript
export async function GET() {
  try {
    const data = await prisma.model.findMany();
    return NextResponse.json(data);
  } catch (error) {
    console.error('Error description:', error);
    return NextResponse.json(
      { error: 'User-friendly message' },
      { status: 500 }
    );
  }
}
```

**Client Components:** Use loading/error state pattern:
```javascript
const [data, setData] = useState(null);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);

// Always handle all three states in your UI
```

### Form Validation Strategy
Implement validation at multiple levels:

1. **Client-side:** Immediate feedback for users
2. **API-side:** Security and data integrity
3. **Database-side:** Schema constraints

```javascript
// Client validation example
const validateForm = (data) => {
  const errors = {};
  if (!data.title?.trim()) errors.title = 'Title is required';
  if (!data.technologies?.length) errors.technologies = 'Add at least one technology';
  return errors;
};
```

### Database Query Patterns
**Always order by `createdAt` for consistent results:**
```javascript
const projects = await prisma.project.findMany({
  orderBy: { createdAt: 'desc' }  // Newest first
});
```

**Handle not found cases explicitly:**
```javascript
const project = await prisma.project.findUnique({
  where: { id: parseInt(params.id) }
});

if (!project) {
  return NextResponse.json(
    { error: 'Project not found' },
    { status: 404 }
  );
}
```

---

## 🎨 Styling Conventions

### Tailwind CSS Patterns
This project uses **Tailwind CSS 4.0** with these established patterns:

**Layout Components:**
```javascript
<div className="container mx-auto px-4 py-8">        // Standard page wrapper
<div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">  // Responsive grid
```

**Interactive Elements:**
```javascript
<button className="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
```

**Form Elements:**
```javascript
<input className="w-full px-3 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500">
```

**Error States:**
```javascript
<div className="bg-red-50 border border-red-200 rounded-lg p-6">
  <p className="text-red-700">{error}</p>
</div>
```

### Image Handling
**Always use Next.js Image component:**
```javascript
import Image from 'next/image';

<Image
  src={project.imageUrl}
  alt={project.title}
  width={400}
  height={200}
  className="w-full h-48 object-cover"
/>
```

---

## 🚨 Common Pitfalls & Solutions

### Environment Variables
**Problem:** Database connection fails
**Solution:** Ensure `.env.local` exists and `DATABASE_URL` is set
```bash
DATABASE_URL="postgresql://user:pass@host:5432/db?sslmode=require"
```

### Prisma Client Issues
**Problem:** "Prisma client not found"
**Solution:** Run `npm run db:generate` after schema changes

### Type Coercion
**Problem:** URL params are always strings
**Solution:** Always convert to numbers for database IDs
```javascript
const id = parseInt(params.id);
if (isNaN(id)) {
  return NextResponse.json({ error: 'Invalid ID' }, { status: 400 });
}
```

### Array Field Handling
**Problem:** PostgreSQL array fields need special handling
**Solution:** Use Prisma array operators
```javascript
// Check if array contains value
where: {
  technologies: {
    has: 'React'
  }
}

// Update array (replace entirely)
data: {
  technologies: ['React', 'Next.js']
}
```

---

## 🎓 Educational Context

### Student Skill Progression
This project is designed for students learning:

1. **Week 1:** Basic Next.js and React patterns
2. **Week 2:** Database integration with Prisma
3. **Week 3:** API development and testing
4. **Week 4:** Advanced component patterns
5. **Week 5:** Full-stack integration and deployment

### TODOs in Codebase
The starter code contains intentional TODOs for student implementation:
- `app/api/projects/route.js` - Students implement CRUD endpoints
- `app/projects/components/ProjectForm.js` - Students build form component
- `app/projects/components/TechnologyInput.js` - Students create advanced input

**When helping students:** Guide them through the implementation rather than providing complete solutions.

---

## 🚀 Deployment Checklist

### Vercel Deployment
1. **Environment Variables:** Set `DATABASE_URL` in Vercel dashboard
2. **Build Command:** Ensure `npm run build` passes locally first
3. **Database:** Verify Neon database is accessible from Vercel

### Production Considerations
- Enable Prisma query logging for debugging
- Set up error monitoring (Sentry integration ready)
- Configure image domains in `next.config.js` for external images
- Test API endpoints with production database

---

## 🔍 Code Quality Standards

### TypeScript Migration Path
While currently JavaScript, the project is structured for easy TypeScript migration:
- Use consistent prop patterns
- Implement proper error handling
- Follow React best practices

### Testing Approach
- **API Tests:** Verify endpoint functionality and error handling
- **Component Tests:** Ensure UI renders correctly
- **Integration Tests:** Test full user workflows
- **Database Tests:** Verify data operations work correctly

---

This codebase demonstrates modern full-stack development patterns while maintaining educational clarity. Focus on helping students understand the "why" behind architectural decisions, not just the "how" of implementation.