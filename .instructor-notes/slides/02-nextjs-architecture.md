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