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

**Students build a complete form component (40 minutes):**

```javascript
// app/projects/components/ProjectForm.js
'use client';

import { useState } from 'react';
import TechnologyInput from './TechnologyInput';

export default function ProjectForm({ onSubmit, onCancel, isOpen }) {
  // Form state management
  const [formData, setFormData] = useState({
    title: '',
    description: '',
    imageUrl: '',
    projectUrl: '',
    githubUrl: '',
    technologies: []
  });
  
  // Error and loading states
  const [errors, setErrors] = useState({});
  const [isSubmitting, setIsSubmitting] = useState(false);
  
  // Validation function
  const validateForm = () => {
    const newErrors = {};
    
    if (!formData.title.trim()) {
      newErrors.title = 'Title is required';
    }
    
    if (!formData.description.trim()) {
      newErrors.description = 'Description is required';
    }
    
    if (formData.technologies.length === 0) {
      newErrors.technologies = 'Add at least one technology';
    }
    
    // URL validation
    const urlPattern = /^https?:\/\/.+\..+/;
    if (formData.projectUrl && !urlPattern.test(formData.projectUrl)) {
      newErrors.projectUrl = 'Enter a valid URL';
    }
    
    if (formData.githubUrl && !urlPattern.test(formData.githubUrl)) {
      newErrors.githubUrl = 'Enter a valid GitHub URL';
    }
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };
  
  // Handle form submission
  const handleSubmit = async (e) => {
    e.preventDefault();
    
    if (!validateForm()) return;
    
    setIsSubmitting(true);
    try {
      await onSubmit(formData);
      
      // Reset form on success
      setFormData({
        title: '',
        description: '',
        imageUrl: '',
        projectUrl: '',
        githubUrl: '',
        technologies: []
      });
      setErrors({});
    } catch (error) {
      setErrors({ submit: 'Failed to create project. Please try again.' });
    } finally {
      setIsSubmitting(false);
    }
  };
  
  // Handle input changes
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
    
    // Clear error when user starts typing
    if (errors[name]) {
      setErrors(prev => ({
        ...prev,
        [name]: undefined
      }));
    }
  };
  
  // Handle technologies array updates
  const handleTechnologiesChange = (newTechnologies) => {
    setFormData(prev => ({
      ...prev,
      technologies: newTechnologies
    }));
    
    // Clear technology errors
    if (errors.technologies && newTechnologies.length > 0) {
      setErrors(prev => ({
        ...prev,
        technologies: undefined
      }));
    }
  };
  
  // Only render when open
  if (!isOpen) return null;
  
  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div className="bg-white rounded-lg p-6 w-full max-w-2xl max-h-[90vh] overflow-y-auto">
        <h2 className="text-2xl font-bold mb-6">Add New Project</h2>
        
        <form onSubmit={handleSubmit} className="space-y-6">
          {/* Title Field */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              Project Title *
            </label>
            <input
              type="text"
              name="title"
              value={formData.title}
              onChange={handleChange}
              className={`w-full px-3 py-2 border rounded-md ${
                errors.title ? 'border-red-500' : 'border-gray-300'
              }`}
              placeholder="Enter project title"
            />
            {errors.title && (
              <p className="text-red-500 text-sm mt-1">{errors.title}</p>
            )}
          </div>
          
          {/* Description Field */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              Description *
            </label>
            <textarea
              name="description"
              value={formData.description}
              onChange={handleChange}
              rows={4}
              className={`w-full px-3 py-2 border rounded-md ${
                errors.description ? 'border-red-500' : 'border-gray-300'
              }`}
              placeholder="Describe your project"
            />
            {errors.description && (
              <p className="text-red-500 text-sm mt-1">{errors.description}</p>
            )}
          </div>
          
          {/* Technology Input Component */}
          <TechnologyInput
            technologies={formData.technologies}
            onChange={handleTechnologiesChange}
            error={errors.technologies}
          />
          
          {/* Optional URL Fields */}
          <div className="grid md:grid-cols-2 gap-4">
            <div>
              <label className="block text-sm font-medium text-gray-700 mb-1">
                Project URL
              </label>
              <input
                type="url"
                name="projectUrl"
                value={formData.projectUrl}
                onChange={handleChange}
                className={`w-full px-3 py-2 border rounded-md ${
                  errors.projectUrl ? 'border-red-500' : 'border-gray-300'
                }`}
                placeholder="https://your-project.com"
              />
              {errors.projectUrl && (
                <p className="text-red-500 text-sm mt-1">{errors.projectUrl}</p>
              )}
            </div>
            
            <div>
              <label className="block text-sm font-medium text-gray-700 mb-1">
                GitHub URL
              </label>
              <input
                type="url"
                name="githubUrl"
                value={formData.githubUrl}
                onChange={handleChange}
                className={`w-full px-3 py-2 border rounded-md ${
                  errors.githubUrl ? 'border-red-500' : 'border-gray-300'
                }`}
                placeholder="https://github.com/user/repo"
              />
              {errors.githubUrl && (
                <p className="text-red-500 text-sm mt-1">{errors.githubUrl}</p>
              )}
            </div>
          </div>
          
          {/* Image URL Field */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              Image URL
            </label>
            <input
              type="url"
              name="imageUrl"
              value={formData.imageUrl}
              onChange={handleChange}
              className="w-full px-3 py-2 border border-gray-300 rounded-md"
              placeholder="https://example.com/project-image.jpg"
            />
            <p className="text-sm text-gray-500 mt-1">
              Optional: URL to project screenshot or logo
            </p>
          </div>
          
          {/* Submit Error */}
          {errors.submit && (
            <div className="p-4 bg-red-50 border border-red-200 rounded-md">
              <p className="text-red-700">{errors.submit}</p>
            </div>
          )}
          
          {/* Form Actions */}
          <div className="flex justify-end gap-4 pt-4">
            <button
              type="button"
              onClick={onCancel}
              className="px-6 py-2 border border-gray-300 rounded-md hover:bg-gray-50 transition-colors"
              disabled={isSubmitting}
            >
              Cancel
            </button>
            <button
              type="submit"
              disabled={isSubmitting}
              className="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 disabled:bg-blue-300 transition-colors"
            >
              {isSubmitting ? 'Creating...' : 'Create Project'}
            </button>
          </div>
        </form>
      </div>
    </div>
  );
}
```

---

## 🏷️ Advanced Component: TechnologyInput

**Students build a complex input component (30 minutes):**

```javascript
// app/projects/components/TechnologyInput.js
'use client';

import { useState } from 'react';

export default function TechnologyInput({ technologies = [], onChange, error }) {
  const [inputValue, setInputValue] = useState('');
  
  const predefinedTechnologies = [
    'JavaScript', 'TypeScript', 'React', 'Next.js', 'Node.js', 'Express',
    'HTML', 'CSS', 'Tailwind CSS', 'Bootstrap', 'Python', 'Java',
    'PostgreSQL', 'MongoDB', 'MySQL', 'Prisma', 'GraphQL', 'REST API',
    'Git', 'Docker', 'AWS', 'Vercel', 'Figma', 'Photoshop'
  ];
  
  const addTechnology = (tech) => {
    const trimmedTech = tech.trim();
    if (trimmedTech && !technologies.includes(trimmedTech)) {
      onChange([...technologies, trimmedTech]);
    }
    setInputValue('');
  };
  
  const removeTechnology = (index) => {
    const newTechnologies = technologies.filter((_, i) => i !== index);
    onChange(newTechnologies);
  };
  
  const handleKeyPress = (e) => {
    if (e.key === 'Enter') {
      e.preventDefault();
      addTechnology(inputValue);
    }
  };
  
  const handleQuickAdd = (tech) => {
    if (!technologies.includes(tech)) {
      onChange([...technologies, tech]);
    }
  };
  
  return (
    <div>
      <label className="block text-sm font-medium text-gray-700 mb-2">
        Technologies *
      </label>
      
      {/* Input Field */}
      <div className="flex gap-2 mb-3">
        <input
          type="text"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          onKeyPress={handleKeyPress}
          className={`flex-1 px-3 py-2 border rounded-md ${
            error ? 'border-red-500' : 'border-gray-300'
          }`}
          placeholder="Type a technology and press Enter"
        />
        <button
          type="button"
          onClick={() => addTechnology(inputValue)}
          className="px-4 py-2 bg-gray-600 text-white rounded-md hover:bg-gray-700 transition-colors"
          disabled={!inputValue.trim()}
        >
          Add
        </button>
      </div>
      
      {/* Quick Add Buttons */}
      <div className="mb-3">
        <p className="text-sm text-gray-600 mb-2">Quick add:</p>
        <div className="flex flex-wrap gap-2">
          {predefinedTechnologies
            .filter(tech => !technologies.includes(tech))
            .slice(0, 8)
            .map((tech) => (
              <button
                key={tech}
                type="button"
                onClick={() => handleQuickAdd(tech)}
                className="px-2 py-1 text-sm bg-gray-100 text-gray-700 rounded hover:bg-gray-200 transition-colors"
              >
                + {tech}
              </button>
            ))}
        </div>
      </div>
      
      {/* Selected Technologies */}
      <div className="min-h-[40px] p-3 border border-gray-200 rounded-md bg-gray-50">
        {technologies.length === 0 ? (
          <p className="text-gray-500 text-sm">No technologies added yet</p>
        ) : (
          <div className="flex flex-wrap gap-2">
            {technologies.map((tech, index) => (
              <span
                key={index}
                className="inline-flex items-center gap-1 px-2 py-1 bg-blue-100 text-blue-800 text-sm rounded"
              >
                {tech}
                <button
                  type="button"
                  onClick={() => removeTechnology(index)}
                  className="hover:text-blue-600 font-bold"
                  title="Remove technology"
                >
                  ×
                </button>
              </span>
            ))}
          </div>
        )}
      </div>
      
      {/* Error Message */}
      {error && (
        <p className="text-red-500 text-sm mt-1">{error}</p>
      )}
      
      {/* Help Text */}
      <p className="text-sm text-gray-500 mt-1">
        Add technologies used in this project. Press Enter or click Add.
      </p>
    </div>
  );
}
```

---

## 🔗 Component Integration

**Final integration in Projects page:**

```javascript
// app/projects/page.js
'use client';

import { useState, useEffect } from 'react';
import ProjectForm from './components/ProjectForm';

export default function Projects() {
  const [projects, setProjects] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);
  const [showForm, setShowForm] = useState(false);
  
  const fetchProjects = async () => {
    // ... (from previous module)
  };
  
  const handleCreateProject = async (formData) => {
    const response = await fetch('/api/projects', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(formData)
    });
    
    if (!response.ok) {
      const errorData = await response.json();
      throw new Error(errorData.error || 'Failed to create project');
    }
    
    const newProject = await response.json();
    
    // Optimistic update
    setProjects(prev => [newProject, ...prev]);
    
    // Close form
    setShowForm(false);
  };
  
  useEffect(() => {
    fetchProjects();
  }, []);
  
  return (
    <div className="container mx-auto px-4 py-8">
      <div className="flex justify-between items-center mb-8">
        <h1 className="text-4xl font-bold">My Projects</h1>
        <button
          onClick={() => setShowForm(true)}
          className="px-6 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors"
        >
          Add New Project
        </button>
      </div>
      
      {/* Form Component */}
      <ProjectForm
        isOpen={showForm}
        onSubmit={handleCreateProject}
        onCancel={() => setShowForm(false)}
      />
      
      {/* Project Grid */}
      {/* ... (loading, error, projects display) */}
    </div>
  );
}
```

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