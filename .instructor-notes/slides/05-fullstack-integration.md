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