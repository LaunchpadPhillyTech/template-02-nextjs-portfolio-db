# Week 1 Day 1: Introduction to Next.js
## Presentation Slide Outline with Speaker Notes

**Total Slides:** 62  
**Duration:** 90-minute lecture + 60-minute lab  
**Date:** Monday, November 17, 2025

---

## OPENING CIRCLE (15 minutes)

### Slide 1: Welcome
**Visual:** Large welcome text with Next.js logo
**Content:**
- Week 1: Next.js Foundation & Routing
- Day 1: Getting Started

**Speaker Notes:**
"Good morning everyone! Welcome to Week 1 of our Next.js journey. By Friday, you'll have your own portfolio website live on the internet. Today is all about understanding what Next.js is and creating your first project."

---

### Slide 2: Circle Question
**Visual:** Thought bubble illustration
**Content:**
"If your life was a website, what would be on the homepage?"

**Speaker Notes:**
"Let's start with our opening circle question. Turn to your neighbor and discuss this for 2 minutes. This gets us thinking about personal branding and what we want to showcase."

---

### Slide 3: This Week's Journey
**Visual:** Road map with 5 stops (Mon-Fri)
**Content:**
- Monday: What is Next.js? Create first project
- Tuesday: Styling with Tailwind CSS
- Wednesday: Layouts and components
- Thursday: Images and testing
- Friday: Deploy to the internet!

**Speaker Notes:**
"Here's our week at a glance. Each day builds on the previous one. By Friday, you'll have something you can show your family and friends!"

---

## LECTURE SEGMENT 1: WHAT IS NEXT.JS? (20 minutes)

### Slide 4: What You'll Build This Week
**Visual:** Screenshot of example portfolio
**Content:**
- 4-page personal portfolio
- Home, About, Projects, Contact
- Responsive design
- Deployed to the internet

**Speaker Notes:**
"This is what you're building - your own portfolio website. It will work on phones, tablets, and computers. And it will be LIVE on the internet with its own URL."

---

### Slide 5: What is React?
**Visual:** React logo with component illustration
**Content:**
- JavaScript library for building UIs
- Made by Facebook (Meta)
- Uses "components" - reusable pieces

**Analogy Box:**
"React is like having a box of LEGO blocks. Each block is a piece of your website that you can use over and over."

**Speaker Notes:**
"Before we understand Next.js, we need to understand React. React lets us build websites using components - small, reusable pieces. Think of it like LEGO blocks."

---

### Slide 6: What is Next.js?
**Visual:** Next.js logo + React logo with "+" between them
**Content:**
- Framework built ON TOP of React
- Made by Vercel
- Adds "superpowers" to React

**Analogy Box:**
"React is like having LEGO blocks. Next.js is like having those blocks PLUS an instruction manual, a building platform, and someone who delivers your creation to people all over the world."

**Speaker Notes:**
"Next.js takes React and adds a bunch of superpowers. It makes building websites easier and faster."

---

### Slide 7: Next.js Superpowers
**Visual:** 4 icons with labels
**Content:**
1. 🗂️ **Automatic Routing** - Folders become pages automatically
2. ⚡ **Built-in Optimization** - Your site loads super fast
3. 🖼️ **Image Optimization** - Photos load perfectly every time
4. 🚀 **Easy Deployment** - One-click publish to internet

**Speaker Notes:**
"These are the four main superpowers Next.js gives you. Don't worry if you don't understand them all yet - you'll experience them this week!"

---

### Slide 8: Who Uses Next.js?
**Visual:** Logos of major companies
**Content:**
- Netflix
- TikTok
- Twitch
- Nike
- Hulu
- ChatGPT

**Speaker Notes:**
"These are billion-dollar companies that trust Next.js for their websites. If it's good enough for them, it's definitely worth learning!"

---

### Slide 9: Why We're Learning Next.js
**Visual:** Bar chart showing demand
**Content:**
- #1 most in-demand React framework in 2025
- 79% year-over-year growth
- Companies want Next.js developers
- Easier than building from scratch

**Speaker Notes:**
"This is not just a random choice. Next.js is THE most requested skill for React developers. Learning this makes you more employable."

---

### Slide 10: React vs Next.js
**Visual:** Side-by-side comparison table
**Content:**

| React | Next.js |
|-------|---------|
| Just UI library | Full framework |
| You set up routing | Routing built-in |
| Manual optimization | Auto-optimized |
| Complex deployment | One-click deploy |

**Speaker Notes:**
"Here's the difference. React is great, but Next.js gives you everything you need in one package. Less work for you!"

---

## LECTURE SEGMENT 2: CREATING YOUR FIRST PROJECT (30 minutes)

### Slide 11: Prerequisites Check
**Visual:** Checklist with checkboxes
**Content:**
Before we start, you need:
- ✅ Node.js installed (v20+)
- ✅ VS Code installed
- ✅ Terminal/Command Prompt
- ✅ Internet connection

**Speaker Notes:**
"Let's make sure everyone has what they need. Open VS Code and let's verify Node.js is installed."

---

### Slide 12: Check Node.js Version
**Visual:** Terminal screenshot
**Content:**
```bash
node --version
```

**Expected output:** `v20.x.x` or higher

**Speaker Notes:**
"Everyone type this command in your terminal. You should see version 20 or higher. If not, raise your hand and we'll help you install it."

---

### Slide 13: Create Next.js Project - The Command
**Visual:** Terminal with command highlighted
**Content:**
```bash
npx create-next-app@latest my-portfolio
```

**What this does:**
- `npx` = Run a package without installing it
- `create-next-app` = Next.js project creator
- `@latest` = Use newest version
- `my-portfolio` = Your project name

**Speaker Notes:**
"This is the magic command that creates a Next.js project. Let's break down what each part means."

---

### Slide 14: Installation Prompts - TypeScript
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to use TypeScript? › No / Yes
```

**Our choice:** No

**Why?** We're learning to walk before we run. TypeScript is more advanced.

**Speaker Notes:**
"You'll see several questions. For this one, we're choosing No. TypeScript is great but it's extra complexity we don't need yet."

---

### Slide 15: Installation Prompts - ESLint
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to use ESLint? › No / Yes
```

**Our choice:** Yes

**Analogy:** ESLint is like spell-checker for your code!

**Speaker Notes:**
"ESLint catches mistakes in your code before they become bugs. It's like having a helpful assistant checking your work."

---

### Slide 16: Installation Prompts - Tailwind
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to use Tailwind CSS? › No / Yes
```

**Our choice:** Yes

**Analogy:** Tailwind is like Instagram filters for your website!

**Speaker Notes:**
"Tailwind CSS is what we'll use to make our site look good. It's like having pre-made design choices ready to go."

---

### Slide 17: Installation Prompts - src/ directory
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like your code inside a `src/` directory? › No / Yes
```

**Our choice:** No

**Why?** Keeping it simple! Less folders to navigate.

**Speaker Notes:**
"For learning, we'll keep our structure simple. No need for extra folders right now."

---

### Slide 18: Installation Prompts - App Router
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to use App Router? › No / Yes
```

**Our choice:** Yes

**Analogy:** This is like upgrading from a flip phone to a smartphone!

**Speaker Notes:**
"App Router is the modern way to build with Next.js. It's newer and better than the old way."

---

### Slide 19: Installation Prompts - Turbopack
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to use Turbopack for `next dev`? › No / Yes
```

**Our choice:** Yes

**Analogy:** Turbopack is like having fast WiFi vs slow WiFi!

**Speaker Notes:**
"Turbopack makes your code reload faster when you make changes. Faster is better!"

---

### Slide 20: Installation Prompts - Import Alias
**Visual:** Screenshot of prompt
**Content:**
```
? Would you like to customize the import alias? › No / Yes
```

**Our choice:** No

**Why?** Defaults are fine for now!

**Speaker Notes:**
"Last question! We'll stick with defaults here. One less thing to think about."

---

### Slide 21: Installation in Progress
**Visual:** Animation of progress bars
**Content:**
- Creating project... ⏳
- Installing dependencies... ⏳
- This takes 1-2 minutes ☕

**Speaker Notes:**
"Now sit back for a minute or two while it downloads and installs everything. This is a good time to stretch!"

---

### Slide 22: Success!
**Visual:** Checkmark and celebration GIF
**Content:**
```
✓ Success! Created my-portfolio
```

**What happens next:**
```bash
cd my-portfolio
npm run dev
```

**Speaker Notes:**
"When you see this success message, you're ready! Now we'll open the project and start the development server."

---

## LECTURE SEGMENT 3: UNDERSTANDING PROJECT STRUCTURE (25 minutes)

### Slide 23: Open in VS Code
**Visual:** VS Code window
**Content:**
```bash
cd my-portfolio
code .
```

**What this does:**
- `cd my-portfolio` = Go into the folder
- `code .` = Open current folder in VS Code

**Speaker Notes:**
"These two commands will open your project in VS Code. Let's all do this together."

---

### Slide 24: Project Structure - The Apartment Building
**Visual:** Illustration of apartment building
**Content:**
"Think of your project like an apartment building..."

- 🏢 **Building** = Your project folder
- 🏠 **Floors** = Different folders (app/, public/, etc.)
- 🚪 **Apartments** = Individual files (page.js, layout.js)
- 📬 **Mailbox** = public/ folder (shared files)

**Speaker Notes:**
"I want you to think of your project like an apartment building. This analogy will help you understand where everything goes."

---

### Slide 25: Key Folders
**Visual:** Folder tree diagram
**Content:**
```
my-portfolio/
├── app/              ← Your website pages live here
├── public/           ← Images and static files
├── node_modules/     ← Don't touch! (libraries)
└── package.json      ← Project settings
```

**Speaker Notes:**
"These are the four main folders you'll see. You'll spend 90% of your time in the app/ folder."

---

### Slide 26: The app/ Folder
**Visual:** Zoomed folder view
**Content:**
```
app/
├── layout.js     ← The picture frame (wraps everything)
├── page.js       ← Your homepage
└── globals.css   ← Styling for whole site
```

**Speaker Notes:**
"Inside app/, these three files are the most important to understand right now."

---

### Slide 27: What is layout.js?
**Visual:** Picture frame illustration
**Content:**
```javascript
export default function RootLayout({ children }) {
  return (
    <html>
      <body>{children}</body>
    </html>
  )
}
```

**Analogy:** The picture frame. The frame stays the same, but you can swap out different pictures (pages).

**Speaker Notes:**
"Layout is like a picture frame. {children} is where the picture (your page) goes. The frame stays the same for every page."

---

### Slide 28: What is page.js?
**Visual:** Homepage preview
**Content:**
```javascript
export default function Home() {
  return (
    <main>
      <h1>Welcome to My Site!</h1>
    </main>
  )
}
```

**This file controls:** Your homepage (/)

**Speaker Notes:**
"Page.js is what people see when they visit yoursite.com. This is your homepage."

---

### Slide 29: What is globals.css?
**Visual:** Paint palette
**Content:**
- Global styles for your entire site
- Tailwind CSS is loaded here
- Default colors and fonts

**Speaker Notes:**
"This file handles the overall look and feel. We won't edit this much - Tailwind does most of the styling for us."

---

### Slide 30: Files You Should NOT Edit
**Visual:** Warning sign
**Content:**
❌ **Don't edit these:**
- package.json
- next.config.js
- node_modules/ (never!)
- tailwind.config.js (not yet)

**Why?** These are configuration files. Changing them can break things!

**Speaker Notes:**
"Important! Leave these files alone for now. They're set up correctly and changing them can cause errors."

---

## LECTURE SEGMENT 4: RUNNING YOUR FIRST DEV SERVER (15 minutes)

### Slide 31: Start the Development Server
**Visual:** Terminal screenshot
**Content:**
```bash
npm run dev
```

**What this command does:**
- Starts Next.js in development mode
- Opens your site at localhost:3000
- Enables hot reload (instant updates!)

**Speaker Notes:**
"This is the command you'll use every day. It starts your development server so you can see your website."

---

### Slide 32: What You'll See
**Visual:** Terminal output
**Content:**
```
  ▲ Next.js 15.0.0
  - Local:        http://localhost:3000
  
 ✓ Starting...
 ✓ Ready in 1.2s
```

**What this means:**
- ✓ Server is running
- Visit: http://localhost:3000

**Speaker Notes:**
"When you see this 'Ready' message, your server is running! Now you can visit localhost:3000 in your browser."

---

### Slide 33: localhost:3000 - What Does This Mean?
**Visual:** Simple diagram
**Content:**
- **localhost** = Your own computer
- **3000** = Port number (like an apartment number)
- Only YOU can see it (not on internet yet!)

**Analogy:** Like looking in a mirror before going out. Only you can see it until you deploy!

**Speaker Notes:**
"Localhost means 'my computer'. Port 3000 is just a number. This site is only visible to you right now."

---

### Slide 34: Opening Your Site
**Visual:** Browser screenshot
**Content:**
**Two ways to open:**

1. Hold Ctrl (or Cmd) and click the URL in terminal
2. Manually type: `http://localhost:3000` in browser

**Speaker Notes:**
"Let's all open it now. You should see the default Next.js welcome page!"

---

### Slide 35: The Default Next.js Page
**Visual:** Screenshot of default page
**Content:**
- Next.js logo
- "Get started by editing app/page.js"
- Links to docs

**What this proves:** Your setup works! 🎉

**Speaker Notes:**
"If you see this page, congratulations! Your Next.js installation is working perfectly."

---

### Slide 36: Hot Reload - The Magic
**Visual:** Split screen: code editor + browser
**Content:**
**Hot Reload = Instant Updates**

Change your code → Save → Browser updates automatically!

No manual refresh needed!

**Speaker Notes:**
"This is one of the coolest features. Watch what happens when I change the code..."

---

### Slide 37: Live Demo: Making Your First Change
**Visual:** Code editor focused
**Content:**
**Open:** app/page.js

**Find this:**
```javascript
<h1>Welcome to Next.js!</h1>
```

**Change to:**
```javascript
<h1>Welcome to My Portfolio!</h1>
```

**Save and watch browser update!**

**Speaker Notes:**
"I'm going to make this change live. Watch the browser - I don't have to refresh it manually!"

---

### Slide 38: Hot Reload Analogy
**Visual:** Mirror illustration
**Content:**
**Regular websites:** Change outfit → Walk to mirror → See change

**Next.js Hot Reload:** Change outfit → Mirror updates instantly! ✨

**Speaker Notes:**
"Hot reload is like having a magic mirror that shows your changes the second you make them. No walking required!"

---

### Slide 39: Important: Keep Terminal Running!
**Visual:** Terminal window with warning
**Content:**
⚠️ **Don't close this terminal window!**

While you're working:
- Terminal must stay open
- Server must keep running
- You'll see logs here

**To stop:** Press Ctrl+C (but don't do it yet!)

**Speaker Notes:**
"Critical reminder: Keep this terminal window open the whole time you're working. Closing it stops your server."

---

### Slide 40: Wrap-Up Segment 4
**Visual:** Checklist
**Content:**
✅ What we learned:
- Created a Next.js project
- Understood folder structure
- Started development server
- Saw hot reload in action

**Next:** Making this site YOUR own!

**Speaker Notes:**
"Great work! You now have a running Next.js project. After break, we'll learn how to create multiple pages."

---

## MORNING BREAK (15 minutes)

### Slide 41: Break Time!
**Visual:** Coffee cup
**Content:**
- 15-minute break
- Keep your terminal running
- Stretch your legs!
- Back at [TIME]

---

## LAB ACTIVITY INTRODUCTION (5 minutes)

### Slide 42: Lab Time - What You'll Do
**Visual:** Activity checklist
**Content:**
**Next 60 minutes:**

**Milestone 1:** Create & run your project (25 min)
**Milestone 2:** Make your first edit (20 min)
**Milestone 3:** Explore & document (15 min)

**Goal:** Everyone has Next.js running!

**Speaker Notes:**
"For the next hour, you'll work independently on these three milestones. I'll be walking around helping anyone who gets stuck."

---

### Slide 43: Milestone 1 - Create Your Project
**Visual:** Progress bar showing step 1 of 3
**Content:**
**Time:** 25 minutes

**Tasks:**
1. Open terminal
2. Run: `npx create-next-app@latest [your-name]-portfolio`
3. Answer prompts (write down your answers!)
4. Navigate into folder
5. Run: `npm run dev`
6. Open in browser

**Success:** You see the Next.js welcome page!

**Speaker Notes:**
"Start with this first. Raise your hand if you get stuck on any step. Don't move to Milestone 2 until this works!"

---

### Slide 44: Milestone 2 - Make Your First Edit
**Visual:** Progress bar showing step 2 of 3
**Content:**
**Time:** 20 minutes

**Tasks:**
1. Open `app/page.js` in VS Code
2. Find the `<h1>` tag
3. Change text to: "Welcome to [Your Name]'s Portfolio"
4. Save file
5. Watch browser update automatically
6. Add a `<p>` tag with your bio

**Success:** Your name appears on the page!

**Speaker Notes:**
"Once your server is running, try making changes. Remember: save the file and the browser updates automatically!"

---

### Slide 45: Milestone 3 - Explore & Document
**Visual:** Progress bar showing step 3 of 3
**Content:**
**Time:** 15 minutes

**Tasks:**
1. Create file: `notes.md`
2. Document what these files do:
   - app/page.js
   - app/layout.js
   - app/globals.css
3. Take screenshots of your project
4. Write one question you have

**Success:** Notes file with your observations!

**Speaker Notes:**
"Use this time to explore and document. Writing things down helps you remember them!"

---

### Slide 46: Lab Activity - Help Resources
**Visual:** Icons for help
**Content:**
**If you get stuck:**

1. 🔍 Check the error message
2. 📖 Re-read the slide instructions
3. 🤝 Ask your neighbor
4. 🙋 Raise your hand for instructor help

**Remember:** No question is too small!

**Speaker Notes:**
"I'll be walking around, but try these steps first. Often the error message tells you exactly what's wrong!"

---

## LAB TIMER SLIDES (Projected during lab)

### Slide 47: Milestone 1 Timer - 25 Minutes
**Visual:** Large countdown timer + checklist
**Content:**
⏰ **Milestone 1: Create Your Project**

Time remaining: [25:00]

**Checklist:**
- [ ] Ran create-next-app command
- [ ] Answered all prompts
- [ ] Project created successfully
- [ ] Navigated into folder
- [ ] Started dev server
- [ ] Opened localhost:3000

---

### Slide 48: Milestone 2 Timer - 20 Minutes
**Visual:** Large countdown timer + checklist
**Content:**
⏰ **Milestone 2: Make Your First Edit**

Time remaining: [20:00]

**Checklist:**
- [ ] Opened app/page.js
- [ ] Changed heading text
- [ ] Added your name
- [ ] Saved file
- [ ] Saw hot reload work
- [ ] Added paragraph with bio

---

### Slide 49: Milestone 3 Timer - 15 Minutes
**Visual:** Large countdown timer + checklist
**Content:**
⏰ **Milestone 3: Explore & Document**

Time remaining: [15:00]

**Checklist:**
- [ ] Created notes.md file
- [ ] Documented page.js purpose
- [ ] Documented layout.js purpose
- [ ] Documented globals.css purpose
- [ ] Took screenshots
- [ ] Wrote one question

---

## LAB WRAP-UP (10 minutes)

### Slide 50: Lab Debrief
**Visual:** Group discussion
**Content:**
**Quick poll:**

Raise your hand if...
- ✋ You got Next.js running
- ✋ You saw hot reload work
- ✋ You made changes to page.js
- ✋ You have questions

**Speaker Notes:**
"Let's see where everyone is at. Don't worry if you're not done - we'll have more time tomorrow."

---

### Slide 51: Common Issues You Might Have Hit
**Visual:** Troubleshooting checklist
**Content:**
**Issue:** "npm: command not found"  
**Solution:** Need to install Node.js

**Issue:** "Port 3000 in use"  
**Solution:** Close other apps using port 3000

**Issue:** "Module not found"  
**Solution:** Run `npm install` again

**Speaker Notes:**
"These are the most common issues. We'll post solutions in Slack for reference."

---

### Slide 52: What's Coming This Afternoon
**Visual:** Preview of upcoming topics
**Content:**
**After lunch (12:45 PM):**

📚 **Lecture:** File-Based Routing
- How folders become URLs
- Creating multiple pages
- Link component for navigation

💻 **Lab:** Build your portfolio structure

**Speaker Notes:**
"This afternoon we'll learn how to create multiple pages. By end of day, you'll have 4 pages with navigation!"

---

## MORNING SESSION WRAP (5 minutes)

### Slide 53: Morning Recap
**Visual:** Summary checklist
**Content:**
**What we covered:**
✅ What Next.js is and why it matters
✅ How to create a Next.js project
✅ Understanding project structure
✅ Running the development server
✅ Hot reload magic

**Speaker Notes:**
"That's a lot for one morning! You should be proud of getting Next.js running on your computer."

---

### Slide 54: Homework/Pre-Work for Tomorrow
**Visual:** Homework checklist
**Content:**
**Before tomorrow:**
- [ ] Make sure your project still runs
- [ ] Experiment with changing text
- [ ] Try changing colors in Tailwind classes
- [ ] Think about what to put on your About page

**Optional:** Watch "Next.js in 100 Seconds" on YouTube

**Speaker Notes:**
"No formal homework, but play around with your project tonight. The more you experiment, the faster you'll learn!"

---

### Slide 55: Questions?
**Visual:** Large Q&A
**Content:**
**Questions before lunch?**

Ask now or:
- Post in Slack
- Come to office hours (3-4 PM)
- Email instructor

**Speaker Notes:**
"Any questions before we break for lunch? Remember, office hours start at 3 PM if you need extra help."

---

### Slide 56: Lunch Break
**Visual:** Food icon
**Content:**
- Lunch: 12:00 - 12:45 PM
- Back for afternoon session at 12:45 PM
- Keep your project folder safe!

**See you in 45 minutes!**

---

## AFTERNOON SESSION PREVIEW (For reference)

### Slide 57-62: Preview Slides (Not presented yet)
**Content:** File-based routing introduction (will be covered after lunch)

**These slides include:**
- How folders become routes
- Creating your first route
- The Link component
- Navigation between pages
- Dynamic routing preview
- Lab activity: Create 4 pages

**Speaker Notes:**
"These topics are for this afternoon. Just wanted you to see what's coming!"

---

## END OF DAY 1 MORNING SESSION

**Total Slides Presented:** 56  
**Lab Activity:** 3 micro-milestones  
**Duration:** 9:15 AM - 12:00 PM (2 hours 45 minutes)

---

## SPEAKER NOTES SUMMARY

**Key Teaching Points:**
1. Use analogies consistently (LEGO blocks, apartment building, picture frame)
2. Show, don't just tell (live demos are critical)
3. Check for understanding frequently (polls, raise hands)
4. Celebrate small wins (project running, hot reload working)
5. Normalize struggle (everyone gets errors, it's part of learning)

**Timing Notes:**
- Each code slide: 3-4 minutes
- Each analogy slide: 2-3 minutes
- Live demos: 5-7 minutes each
- Transition slides: 1 minute

**Engagement Strategies:**
- Ask questions during slides (not just at end)
- Have students do live exercises during lecture
- Use "turn to your neighbor" moments
- Show error messages and how to fix them
- Celebrate when things work!

---

## MATERIALS NEEDED

**Instructor:**
- [ ] Laptop with Next.js project prepared
- [ ] Projector/screen
- [ ] Timer for lab activities
- [ ] Printed troubleshooting guide

**Students:**
- [ ] Laptop with Node.js installed
- [ ] VS Code installed
- [ ] Internet connection
- [ ] Notebook for notes

---

**End of Day 1 Slide Deck**

This slide deck would be converted to PowerPoint/Google Slides with:
- Visual diagrams
- Code syntax highlighting
- Consistent color scheme
- Large, readable fonts
- Animations for reveals
- Timer functionality for lab slides
