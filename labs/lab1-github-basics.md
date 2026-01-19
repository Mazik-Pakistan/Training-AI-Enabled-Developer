# Lab 1: GitHub Basics - Build Your First Project

## Objective
Create a complete GitHub repository with proper structure, documentation, and collaboration features.

## Duration
60-90 minutes

## Prerequisites
- GitHub account created
- Basic understanding of Git commands
- Completed Module 1, Unit 1

---

## Lab Overview

You'll create a personal portfolio website project on GitHub, practicing:
- Repository creation
- Branch management
- Pull requests
- Issues and project boards
- GitHub Codespaces

---

## Part 1: Repository Setup (15 minutes)

### Step 1: Create Repository
1. Go to [github.com](https://github.com)
2. Click the **+** icon → **New repository**
3. Configure:
   - **Name:** `my-portfolio`
   - **Description:** "Personal portfolio website"
   - **Visibility:** Public
   - ✅ Add README file
   - ✅ Add .gitignore (choose: Node or Python)
   - ✅ Choose License: MIT
4. Click **Create repository**

### Step 2: Clone Repository Locally
```bash
# Clone your repository
git clone https://github.com/YOUR_USERNAME/my-portfolio.git

# Navigate to the directory
cd my-portfolio

# Verify remote
git remote -v
```

### Step 3: Initial Structure
Create the following structure:
```bash
mkdir -p src docs tests
touch src/index.html
touch docs/setup.md
touch tests/test_basic.py
```

---

## Part 2: Branch Management (15 minutes)

### Step 1: Create Feature Branch
```bash
# Create and switch to new branch
git checkout -b feature/add-homepage

# Verify you're on the new branch
git branch
```

### Step 2: Add Content
Edit `src/index.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Portfolio</title>
</head>
<body>
    <header>
        <h1>Welcome to My Portfolio</h1>
        <nav>
            <a href="#about">About</a>
            <a href="#projects">Projects</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>
    
    <main>
        <section id="about">
            <h2>About Me</h2>
            <p>I'm learning to become an AI-Enabled Developer!</p>
        </section>
        
        <section id="projects">
            <h2>My Projects</h2>
            <p>Coming soon...</p>
        </section>
        
        <section id="contact">
            <h2>Contact</h2>
            <p>Email: your.email@example.com</p>
        </section>
    </main>
</body>
</html>
```

### Step 3: Commit and Push
```bash
# Stage changes
git add src/index.html

# Commit with descriptive message
git commit -m "Add initial homepage structure"

# Push to remote
git push origin feature/add-homepage
```

---

## Part 3: Pull Request Workflow (15 minutes)

### Step 1: Create Pull Request
1. Go to your repository on GitHub
2. You'll see a notification about your new branch
3. Click **Compare & pull request**
4. Fill in details:
   - **Title:** "Add homepage structure"
   - **Description:** 
     ```markdown
     ## Changes
     - Created basic HTML structure
     - Added header with navigation
     - Added main sections: About, Projects, Contact
     
     ## Testing
     - [ ] HTML validates
     - [ ] All links work
     - [ ] Responsive on mobile
     ```
5. Click **Create pull request**

### Step 2: Review Your Own PR
1. Go to **Files changed** tab
2. Add inline comments on specific lines
3. Suggest improvements
4. Click **Review changes** → **Approve**

### Step 3: Merge Pull Request
1. Click **Merge pull request**
2. Confirm merge
3. Delete the branch when prompted
4. Update your local repository:
```bash
# Switch back to main
git checkout main

# Pull latest changes
git pull origin main

# Verify your changes are there
ls src/
```

---

## Part 4: Issues and Project Management (15 minutes)

### Step 1: Create Issues
Create 3 issues for your project:

**Issue 1: Add CSS Styling**
```markdown
Title: Add CSS styling to homepage

Description:
## Task
Create a CSS file and add styling to the homepage

## Acceptance Criteria
- [ ] Create `src/style.css`
- [ ] Add color scheme
- [ ] Style navigation
- [ ] Make responsive

Labels: enhancement
```

**Issue 2: Add Projects Section**
```markdown
Title: Populate projects section

Description:
Add at least 3 project showcases with:
- Project name
- Description
- Technologies used
- Link to repository

Labels: content
```

**Issue 3: Add Contact Form**
```markdown
Title: Implement contact form

Description:
Create a working contact form with:
- Name field
- Email field
- Message textarea
- Submit button

Labels: feature
```

### Step 2: Create Project Board
1. Go to **Projects** tab
2. Click **New project**
3. Choose **Board** template
4. Name it "Portfolio Development"
5. Add columns: **To Do**, **In Progress**, **Done**
6. Add your issues to the board

### Step 3: Work on an Issue
1. Pick Issue #1 (Add CSS Styling)
2. Move it to **In Progress**
3. Create a branch:
```bash
git checkout -b feature/add-css-styling
```
4. Create `src/style.css`:
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    color: #333;
}

header {
    background: #2c3e50;
    color: white;
    padding: 1rem;
    text-align: center;
}

nav a {
    color: white;
    text-decoration: none;
    padding: 0.5rem 1rem;
    display: inline-block;
}

nav a:hover {
    background: #34495e;
}

main {
    max-width: 800px;
    margin: 2rem auto;
    padding: 0 1rem;
}

section {
    margin: 2rem 0;
    padding: 1rem;
    border-left: 3px solid #2c3e50;
}

h2 {
    color: #2c3e50;
    margin-bottom: 1rem;
}
```

5. Update `index.html` to include CSS:
```html
<head>
    <!-- ... existing head content ... -->
    <link rel="stylesheet" href="style.css">
</head>
```

6. Commit and push:
```bash
git add .
git commit -m "Add CSS styling - Closes #1"
git push origin feature/add-css-styling
```

7. Create PR and mention the issue
8. Merge PR
9. Move issue to **Done**

---

## Part 5: GitHub Codespaces (15 minutes)

### Step 1: Launch Codespace
1. Go to your repository
2. Click **Code** button (green)
3. Select **Codespaces** tab
4. Click **Create codespace on main**
5. Wait for environment to load

### Step 2: Work in Codespace
1. Explore the VS Code interface in browser
2. Open `src/index.html`
3. Make a small change (add a footer)
4. Use the integrated terminal to commit:
```bash
git add .
git commit -m "Add footer to homepage"
git push
```

### Step 3: Live Server (Optional)
1. In Codespace, install Live Server extension
2. Right-click `index.html`
3. Select **Open with Live Server**
4. View your site in the browser

---

## Part 6: Documentation (10 minutes)

### Update README.md
Replace the content with:

```markdown
# My Portfolio Website

Personal portfolio website showcasing my projects and skills as an AI-Enabled Developer.

## 🌟 Features

- Responsive design
- Clean, modern UI
- Project showcase
- Contact information

## 🛠️ Technologies

- HTML5
- CSS3
- Git & GitHub

## 📦 Setup

1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/my-portfolio.git
```

2. Open `src/index.html` in your browser

## 🚀 Deployment

This site can be deployed using:
- GitHub Pages
- Netlify
- Vercel

## 📝 License

MIT License - see LICENSE file

## 👤 Author

Your Name
- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)
- Email: your.email@example.com
```

Commit and push:
```bash
git add README.md
git commit -m "Update README with project documentation"
git push
```

---

## Deliverables

By the end of this lab, you should have:

✅ A complete GitHub repository
✅ Multiple branches and merged PRs
✅ Issues and project board setup
✅ Working homepage with CSS
✅ Professional documentation
✅ Experience with GitHub Codespaces

---

## Bonus Challenges

### Challenge 1: Enable GitHub Pages
1. Go to Settings → Pages
2. Select source: main branch, /src folder
3. Save and visit your published site

### Challenge 2: Add GitHub Actions
Create `.github/workflows/validate.yml`:
```yaml
name: Validate HTML

on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Validate HTML
        run: |
          echo "HTML validation would go here"
```

### Challenge 3: Collaborate
1. Invite a classmate as collaborator
2. Have them submit a PR
3. Review and merge their changes

---

## Reflection Questions

1. What was the most challenging part of this lab?
2. How does branching help in development?
3. When would you use issues vs project boards?
4. What are the benefits of GitHub Codespaces?
5. How could you improve this workflow?

---

## Next Steps

- Complete the remaining issues in your project board
- Add more projects to your portfolio
- Explore GitHub Pages for deployment
- Try GitHub Actions for CI/CD

**Continue to:** [Lab 2 - GitHub Copilot Fundamentals](lab2-copilot-fundamentals.md)
