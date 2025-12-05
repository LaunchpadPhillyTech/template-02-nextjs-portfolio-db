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