# 📘 Instructor SOP: Week 1 Portfolio - GitHub Classroom Setup

**Course:** Next.js Full-Stack Development  
**Week:** 1 - Foundation & Routing  
**Competencies:** TS.2.3.1, TS.2.3.2, TS.1.2.1  
**Estimated Setup Time:** 45-60 minutes (first time), 15 minutes (subsequent weeks)

---

## 🎯 Overview

This SOP guides you through setting up Week 1's portfolio project in GitHub Classroom with automated grading. Students will build a 4-page portfolio website using Next.js, deploy it to Vercel, and submit via GitHub.

**Grading Breakdown:**
- **60% Automated** - Tests, build checks, lint (via GitHub Actions)
- **40% Manual** - Design quality, content, responsiveness (instructor review)

---

## 📋 Prerequisites

Before starting, ensure you have:

- [ ] GitHub account with GitHub Classroom access
- [ ] GitHub organization for your class (e.g., "LCCC-NextJS-Fall-2025")
- [ ] Week 1 template repository downloaded (from Step 1)
- [ ] GitHub Classroom roster imported (student names/emails)

**First Time Setup?** See Appendix A for GitHub Classroom organization setup.

---

## 🚀 Part 1: Create Template Repository (One-Time Setup)

### Step 1.1: Upload Template to GitHub

1. **Create new repository on GitHub**
   - Go to your class organization (e.g., github.com/LCCC-NextJS-Fall-2025)
   - Click "New repository"
   - Name: `week1-portfolio-template`
   - Description: "Week 1: Next.js Portfolio Project - Starter Code"
   - **Important:** Make it **Public** (so students can fork it)
   - **Do NOT** initialize with README (we have one)
   - Click "Create repository"

2. **Upload the template files**
   
   **Option A: Using GitHub Web Interface (Easiest)**
   - Extract `week1-portfolio-github-classroom-template.zip`
   - On your new repo page, click "uploading an existing file"
   - Drag and drop ALL files from the extracted folder
   - Commit message: "Initial commit - Week 1 portfolio template"
   - Click "Commit changes"

   **Option B: Using Command Line (Recommended)**
   ```bash
   # Extract the ZIP file
   unzip week1-portfolio-github-classroom-template.zip
   cd week1-portfolio-template
   
   # Initialize git and push
   git init
   git add .
   git commit -m "Initial commit - Week 1 portfolio template"
   git branch -M main
   git remote add origin https://github.com/YOUR-ORG/week1-portfolio-template.git
   git push -u origin main
   ```

3. **Verify upload**
   - Refresh your repository page
   - You should see all files: README.md, package.json, app/, tests/, etc.
   - Click through folders to verify structure is intact

### Step 1.2: Mark as Template Repository

1. Go to repository **Settings** (top right)
2. Scroll down to "Template repository" section
3. Check ✅ "Template repository"
4. Click "Save"

**Why?** This allows GitHub Classroom to efficiently create copies for each student.

---

## 🎓 Part 2: Create GitHub Classroom Assignment

### Step 2.1: Create New Assignment

1. **Go to GitHub Classroom**
   - Visit: https://classroom.github.com
   - Select your class organization

2. **Create assignment**
   - Click "New assignment"
   - Choose "Individual assignment"

3. **Configure basic settings**
   - **Assignment title:** `Week 1: Portfolio Website`
   - **Deadline:** Friday, November 21, 2025, 11:59 PM
   - **Repository prefix:** `week1-portfolio`
   - **Repository visibility:** Private (recommended for student work)

### Step 2.2: Configure Starter Code

1. **Add starter code**
   - Select "Add starter code from a template repository"
   - Choose: `YOUR-ORG/week1-portfolio-template`
   - ✅ Check "Grant students write access"

2. **Configure permissions**
   - ✅ Grant students admin access to repository
   - This allows them to configure Vercel deployment

### Step 2.3: Enable Autograding

1. **Enable autograding**
   - Toggle "Enable autograding" to **ON**
   - Click "Import tests from template repository"
   - This pulls from `.github/classroom/autograding.json`

2. **Verify autograding tests**
   You should see 6 tests:
   - ✅ Install Dependencies (no points - setup only)
   - ✅ File Structure Test (20 points)
   - ✅ Component Tests (20 points)
   - ✅ Code Quality Tests (20 points)
   - ✅ Build Test (20 points)
   - ✅ Lint Test (20 points)
   - **Total:** 100 points (automated portion)

3. **Adjust point values if needed**
   - Click on each test to edit points
   - Leave timeout at 10 minutes
   - Keep "comparison: included" for all tests

### Step 2.4: Configure Feedback Pull Request

1. **Enable feedback PR**
   - ✅ Check "Enable feedback pull request"
   - This creates a PR where you can leave code comments

2. **Protected branches** (Optional but recommended)
   - Require status checks before merging
   - Require autograding to pass

### Step 2.5: Final Assignment Settings

1. **Grading options**
   - Total points: 100 (autograding) + manual review
   - Passing threshold: 70 points (suggested)

2. **Create assignment**
   - Review all settings
   - Click "Create assignment"
   - **Copy the invitation link** - you'll share this with students!

---

## 📤 Part 3: Distribute to Students

### Step 3.1: Share Assignment Link

**Recommended Distribution Methods:**

**Method 1: LMS/Beacon (Preferred)**
1. Create assignment in your LMS
2. Add GitHub Classroom invitation link
3. Set due date: November 21, 2025, 11:59 PM
4. Include: Student Submission Guide (from Step 3)

**Method 2: Class Announcement**
```
📢 Week 1 Assignment: Portfolio Website

Accept the assignment here: [GitHub Classroom Link]

Due: Friday, Nov 21 at 11:59 PM

Instructions:
1. Click the link above
2. Accept the assignment (creates your repo)
3. Clone to your computer
4. Follow the README.md instructions
5. Deploy to Vercel by Friday
6. Submit your Vercel URL in Beacon

Need help? Check the Student Guide or come to office hours!
```

**Method 3: Email**
- Send invitation link via email
- Include Student Submission Guide PDF
- Set calendar reminder for deadline

### Step 3.2: Monitor Student Acceptance

1. **View roster**
   - In GitHub Classroom, click on assignment
   - Click "Students" tab
   - See who has accepted

2. **Send reminders**
   - Monday (Day 1): Initial announcement
   - Wednesday (Day 3): Check-in for stuck students
   - Thursday (Day 4): "Almost due!" reminder

---

## 🎯 Part 4: Monitor Student Progress

### Step 4.1: GitHub Classroom Dashboard

1. **View all submissions**
   - GitHub Classroom → Your Assignment
   - See list of all student repositories

2. **Check autograding status**
   - ✅ Green checkmark = all tests passing
   - ❌ Red X = tests failing
   - ⚠️ Yellow = in progress
   - ⭕ Gray = not started

3. **Click on student repository to see:**
   - Latest commit
   - Test results
   - Build status
   - Code (for manual review)

### Step 4.2: Help Students Debug

**Common Issues Dashboard:**

| Issue | Cause | Solution Link |
|-------|-------|---------------|
| ❌ Build failing | Missing dependencies | "Run npm install" |
| ❌ Tests failing | Missing files | "Check file structure" |
| ❌ Lint errors | Code style issues | "Run npm run lint" |
| ⚠️ No commits | Haven't started | "Send reminder email" |

**How to View Test Details:**
1. Click student's repository
2. Go to "Actions" tab
3. Click latest workflow run
4. Expand failed tests to see specific errors
5. You can share this info with student

---

## ✅ Part 5: Grading Workflow

### Step 5.1: Automated Grading (60 points)

**This happens automatically via GitHub Actions!**

1. **When it runs:**
   - Every time student pushes code
   - Final score calculated at deadline

2. **What it checks:**
   - File Structure (20 pts) - All required files exist
   - Components (20 pts) - Navbar/Footer created
   - Code Quality (20 pts) - Using Link/Image components
   - Build (20 pts) - Project builds without errors
   - Lint (20 pts) - Code passes ESLint checks

3. **View scores:**
   - GitHub Classroom dashboard shows aggregate score
   - Export to CSV for gradebook import

### Step 5.2: Manual Grading (40 points)

**You'll review these aspects manually:**

1. **Content Quality (10 points)**
   - [ ] Complete bio on About page
   - [ ] 3 project cards with descriptions
   - [ ] Contact information present
   - [ ] Grammar and spelling

2. **Visual Design (10 points)**
   - [ ] Professional appearance
   - [ ] Consistent color scheme
   - [ ] Good typography choices
   - [ ] Visual hierarchy clear

3. **Responsive Design (10 points)**
   - [ ] Works on mobile (320px+)
   - [ ] Works on tablet (768px+)
   - [ ] Works on desktop (1024px+)
   - [ ] No broken layouts

4. **Deployment (10 points)**
   - [ ] Deployed to Vercel
   - [ ] Live URL submitted
   - [ ] Site loads correctly
   - [ ] All pages accessible

**Grading Rubric Template:**
```
Student: ________________
Repo: ___________________
Vercel URL: _____________

AUTOMATED (60 pts) _______ (from GitHub Classroom)

MANUAL REVIEW:
[ ] Content Quality    ___/10
[ ] Visual Design      ___/10  
[ ] Responsive Design  ___/10
[ ] Deployment         ___/10

TOTAL: ______/100

Notes:
_____________________________
_____________________________
```

### Step 5.3: Provide Feedback

**Option 1: GitHub Feedback PR**
1. Go to student's repository
2. Click "Pull requests"
3. Find "Feedback" PR
4. Review code and leave comments
5. Student can see and respond

**Option 2: GitHub Issues**
1. Create issue on student's repo
2. Title: "Week 1 Feedback"
3. Use template:
```markdown
## Great work on:
- [ ] _______________
- [ ] _______________

## Areas for improvement:
- [ ] _______________
- [ ] _______________

## Next steps:
- [ ] _______________

Grade: __/100
```

**Option 3: LMS Comments**
- Leave feedback in Beacon/Canvas
- Include link to their deployed site
- Suggest improvements for Week 2

---

## 📊 Part 6: Export Grades

### Step 6.1: Download from GitHub Classroom

1. Go to assignment in GitHub Classroom
2. Click "Download grades" (CSV format)
3. Contains: Student name, repo URL, autograding score

### Step 6.2: Combine with Manual Grades

**Spreadsheet Setup:**
```
| Student Name | Repo | Auto (60) | Content (10) | Design (10) | Responsive (10) | Deploy (10) | Total (100) |
|--------------|------|-----------|--------------|-------------|-----------------|-------------|-------------|
```

**Formula for Total:**
```
=SUM(C2:G2)
```

### Step 6.3: Import to LMS

1. Export CSV from spreadsheet
2. Format columns to match LMS requirements
3. Import to Beacon/Canvas gradebook
4. Verify all grades transferred correctly

---

## 🆘 Troubleshooting Common Issues

### Issue 1: Autograding Not Running

**Symptoms:** No green checkmark or red X on student repos

**Causes & Solutions:**

1. **GitHub Actions disabled**
   - Go to Settings → Actions → General
   - Enable "Allow all actions and reusable workflows"

2. **Workflow file missing**
   - Check if `.github/workflows/classroom.yml` exists
   - Re-push template if missing

3. **Permissions issue**
   - Settings → Actions → General
   - Set "Workflow permissions" to "Read and write"

### Issue 2: Tests Failing for All Students

**Symptoms:** Everyone getting 0/100 on automated tests

**Causes & Solutions:**

1. **Test file path wrong**
   - Open `autograding.json`
   - Verify test commands match file structure
   - Should be: `npm test -- --run tests/portfolio.test.js`

2. **Dependencies not installing**
   - Check `package.json` is in root
   - Verify Node.js version in workflow (should be 20)

3. **Build failing due to environment**
   - Check `next.config.js` is present
   - Verify all config files uploaded

### Issue 3: Students Can't Push Code

**Symptoms:** "Permission denied" errors when pushing

**Causes & Solutions:**

1. **Admin access not granted**
   - Edit assignment settings
   - Check ✅ "Grant students admin access"

2. **SSH key not configured**
   - Have student add SSH key to GitHub
   - Or use HTTPS with Personal Access Token

3. **Wrong remote URL**
   ```bash
   git remote -v  # Check current remote
   git remote set-url origin [correct-url]  # Fix if wrong
   ```

### Issue 4: Vercel Deployment Failing

**Symptoms:** Student can't deploy to Vercel

**Causes & Solutions:**

1. **Build errors**
   - Run `npm run build` locally first
   - Fix any errors before deploying

2. **Environment variables missing**
   - Usually not needed for Week 1
   - If using external APIs, add to Vercel

3. **Vercel account issues**
   - Ensure student signed up with GitHub
   - Grant GitHub repo access in Vercel

---

## 📅 Week 1 Timeline & Checkpoints

### Monday (Nov 17)
- [ ] Publish assignment in LMS
- [ ] Share GitHub Classroom link
- [ ] Post announcement in class Slack

### Tuesday (Nov 18)
- [ ] Check acceptance rate (target: 80%)
- [ ] Send reminder to non-accepters
- [ ] Monitor first commits

### Wednesday (Nov 19)
- [ ] Review autograding status
- [ ] Reach out to students with failing tests
- [ ] Office hours: Help with debugging

### Thursday (Nov 20)
- [ ] Check deployment status
- [ ] Send "Almost due!" reminder
- [ ] Extended office hours

### Friday (Nov 21)
- [ ] Assignment due 11:59 PM
- [ ] Download grades from GitHub Classroom
- [ ] Begin manual review

### Monday (Nov 24)
- [ ] Complete manual grading
- [ ] Provide feedback on all submissions
- [ ] Upload grades to LMS
- [ ] Preview Week 2 assignment

---

## 📈 Success Metrics

Track these metrics to improve future assignments:

- **Acceptance Rate:** Target 100% by Wednesday
- **On-Time Submission:** Target 90%+
- **Autograding Pass Rate:** Target 80%+ on first push
- **Deployment Success:** Target 95%
- **Average Score:** Target 85/100

**Weekly Retrospective Questions:**
1. What did most students struggle with?
2. Which autograding tests had highest failure rate?
3. How can we improve instructions for next week?
4. Should point distribution change?

---

## 🔄 For Future Weeks

**Reusing This Template Process:**

1. **Clone Week 1 template**
2. **Modify for new competencies**
3. **Update README with new requirements**
4. **Adjust tests for new features**
5. **Create new GitHub Classroom assignment**
6. **Follow same distribution process**

**What to Change:**
- Project requirements
- Test criteria
- Point distribution
- Deadline

**What Stays the Same:**
- Overall structure
- GitHub Classroom workflow
- Grading process
- Tools and configuration

---

## 📚 Appendix A: First-Time GitHub Classroom Setup

### A.1: Create GitHub Organization

1. Go to github.com/organizations/new
2. Choose "Create a free organization"
3. Organization name: `LCCC-NextJS-Fall-2025` (or your format)
4. Contact email: Your school email
5. This organization belongs to: "My personal account"
6. Click "Next"
7. Skip adding members (you'll invite via Classroom)

### A.2: Set Up GitHub Classroom

1. Go to https://classroom.github.com
2. Click "Sign in with GitHub"
3. Authorize GitHub Classroom
4. Click "New classroom"
5. Select your organization
6. Name: "Next.js Fall 2025"
7. Add TAs or co-instructors if needed

### A.3: Import Student Roster

**Option 1: CSV Upload**
1. Create CSV with columns: `identifier,name`
2. Example:
   ```
   identifier,name
   student1@school.edu,John Doe
   student2@school.edu,Jane Smith
   ```
3. Upload in Classroom settings

**Option 2: GitHub Usernames**
1. Have students share GitHub usernames
2. Manually add in roster
3. Tedious but works

**Option 3: Email Identifiers**
1. Use student email addresses
2. Students link when accepting assignment
3. Most flexible method

---

## 📚 Appendix B: Quick Reference Commands

### For Students to Debug Issues

```bash
# Check Node.js version
node --version  # Should be 20+

# Install dependencies
npm install

# Run development server
npm run dev

# Run tests locally
npm test

# Build for production
npm run build

# Check for lint errors
npm run lint

# View git status
git status

# Commit changes
git add .
git commit -m "Your message"
git push
```

### For Instructor Debugging

```bash
# Clone student repository
git clone [student-repo-url]
cd [repo-name]

# Install and test
npm install
npm test
npm run build

# Check autograding config
cat .github/classroom/autograding.json

# Check workflow
cat .github/workflows/classroom.yml
```

---

## 📞 Support Resources

**For Instructor Help:**
- GitHub Classroom Docs: https://docs.github.com/en/education/manage-coursework-with-github-classroom
- GitHub Education Forum: https://github.community/c/education

**For Student Help:**
- Next.js Docs: https://nextjs.org/docs
- Vercel Deployment: https://vercel.com/docs
- GitHub Basics: https://docs.github.com/en/get-started

**Internal Resources:**
- Office hours: [Your schedule]
- Class Slack: [Your Slack link]
- Email: [Your email]

---

## ✅ Final Checklist Before Going Live

- [ ] Template repository created and public
- [ ] Template marked as "Template repository"
- [ ] All files verified in template
- [ ] GitHub Classroom assignment created
- [ ] Autograding enabled and tested
- [ ] Deadline set correctly
- [ ] Invitation link copied
- [ ] Student guide prepared
- [ ] LMS assignment created
- [ ] Calendar reminders set
- [ ] Office hours scheduled
- [ ] Grading rubric prepared

---

**Questions or Issues?**  
Contact: [Your Name] | [Your Email] | Office: [Location/Hours]

**Last Updated:** November 2025  
**Version:** 1.0
