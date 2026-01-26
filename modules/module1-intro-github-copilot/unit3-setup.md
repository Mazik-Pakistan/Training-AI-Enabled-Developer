# Unit 3: GitHub Copilot Primer & Environment Setup

## Learning Objectives
After completing this unit, you will be able to:
- Compare different GitHub Copilot plans and choose the right one
- Understand various GitHub Copilot Chat Modes
- Set up GitHub Copilot in your development environment
- Configure Copilot for optimal performance
- Navigate Copilot's interface and features

---

## 1. GitHub Copilot Plans

### Available Plans

GitHub Copilot offers different plans for individuals, teams, and enterprises:

#### **Copilot Individual** 💻
**Best for**: Individual developers, freelancers, students

**Features:**
- ✅ Code completions in your IDE
- ✅ Copilot Chat in IDE and mobile
- ✅ CLI assistance
- ✅ Security vulnerability filter
- ✅ Code referencing
- ✅ Public code filter

**Pricing:** $10/month 

**Free for:**
- Verified students
- Maintainers of popular open-source projects

#### **Copilot Business** 🏢
**Best for**: Organizations and development teams

**Features:**
- ✅ All Individual features
- ✅ Organization-wide policy management
- ✅ Usage data and insights
- ✅ Audit logs
- ✅ Content exclusions
- ✅ Enterprise-grade security
- ✅ Indemnity coverage

**Pricing:** $19/user/month

#### **Copilot Enterprise** 🏭
**Best for**: Large organizations with advanced needs

**Features:**
- ✅ All Business features
- ✅ Fine-tuned models on your codebase
- ✅ Documentation search and summarization
- ✅ Pull request summaries
- ✅ Code review assistance
- ✅ Knowledge bases
- ✅ Advanced security controls

**Pricing:** $39/user/month

### Feature Comparison Table

| Feature | Individual | Business | Enterprise |
|---------|-----------|----------|------------|
| Code Completions | ✅ | ✅ | ✅ |
| Copilot Chat | ✅ | ✅ | ✅ |
| CLI Integration | ✅ | ✅ | ✅ |
| Mobile App | ✅ | ✅ | ✅ |
| Organization Policies | ❌ | ✅ | ✅ |
| Usage Analytics | ❌ | ✅ | ✅ |
| Audit Logs | ❌ | ✅ | ✅ |
| Content Exclusions | ❌ | ✅ | ✅ |
| Fine-tuned Models | ❌ | ❌ | ✅ |
| PR Summaries | ❌ | ❌ | ✅ |
| Code Review | ❌ | ❌ | ✅ |
| Documentation Search | ❌ | ❌ | ✅ |

### Choosing the Right Plan

**Choose Individual if:**
- You're working on personal projects
- You're a student or open-source maintainer
- You don't need organization-level features

**Choose Business if:**
- You're part of a development team
- You need centralized management
- You want usage insights and audit logs
- You need enterprise security

**Choose Enterprise if:**
- You have a large codebase to leverage
- You need custom model training
- You want advanced code review features
- You need integration with enterprise systems

---

## 2. GitHub Copilot Chat Modes

### Understanding Chat Modes

GitHub Copilot offers different interaction modes for various development scenarios:

### **1. Inline Chat** 💬
Quick conversations directly in your code editor.

**When to use:**
- Quick questions about specific code
- Inline code explanations
- Small refactoring tasks

**How to access:**
- Press `Ctrl+I` (Windows/Linux) or `Cmd+I` (Mac)
- Type your question
- Get instant responses

**Example:**
```python
# Select this code and press Ctrl+I
def calculate_tax(income):
    return income * 0.3

# Ask: "How can I make this progressive tax?"
```

### **2. Chat Panel** 📱
Dedicated chat sidebar for extended conversations.

**When to use:**
- Complex questions
- Multi-step tasks
- Learning about concepts
- Debugging sessions

**How to access:**
- Click the chat icon in VS Code
- Press `Ctrl+Alt+I` (Windows/Linux)
- Use Command Palette: "GitHub Copilot: Open Chat"

**Features:**
- Maintains conversation history
- Share code snippets
- Reference files and symbols
- Use slash commands

### **3. Agent Mode** 🤖
Autonomous mode where Copilot performs multi-step tasks.

**When to use:**
- Complex refactoring
- Feature implementation
- Test generation
- Documentation creation

**How it works:**
```
You: "Create a REST API for user management"
     │
     ▼
Agent analyzes requirements
     │
     ▼
Agent creates files: routes.py, models.py, tests.py
     │
     ▼
Agent implements complete feature
```

### **4. Quick Chat** ⚡
Fast access to Copilot without leaving your workflow.

**When to use:**
- One-off questions
- Quick lookups
- Terminal command help

**How to access:**
- Press `Ctrl+Shift+I`
- Ask question
- Get quick answer

### Chat Mode Comparison

```
┌──────────────┬────────────────────────────────────┐
│  Mode        │  Best For                          │
├──────────────┼────────────────────────────────────┤
│  Inline      │  Quick fixes, explanations         │
│  Chat Panel  │  Detailed help, conversations      │
│  Agent       │  Complex tasks, autonomy           │
│  Quick Chat  │  One-off questions                 │
└──────────────┴────────────────────────────────────┘
```

### Slash Commands

Powerful commands to direct Copilot's behavior:

| Command | Purpose | Example |
|---------|---------|---------|
| `/explain` | Explain selected code | `/explain this regex` |
| `/fix` | Fix bugs or issues | `/fix the syntax error` |
| `/tests` | Generate test cases | `/tests for this function` |
| `/help` | Get help with Copilot | `/help with commands` |
| `/clear` | Clear chat history | `/clear` |
| `/doc` | Generate documentation | `/doc for this class` |

### Context Anchors

Tell Copilot what to focus on:

- `#file` - Reference a specific file
- `#selection` - Reference selected code
- `#terminal` - Reference terminal output
- `#git` - Reference Git changes

**Example:**
```
"Explain the bug in #file:utils.py at #selection"
```

---

## 3. Setting Up Development Environment

### Prerequisites

Before installing GitHub Copilot:

**Requirements:**
- ✅ GitHub account with Copilot access
- ✅ Supported IDE (VS Code, Visual Studio, JetBrains, Neovim)
- ✅ Internet connection
- ✅ Modern operating system

### Step-by-Step Setup for VS Code

#### **Step 1: Install VS Code**

1. Download from [code.visualstudio.com](https://code.visualstudio.com/)
2. Install for your operating system
3. Launch VS Code

#### **Step 2: Get GitHub Copilot Access**

1. Go to [github.com/features/copilot](https://github.com/features/copilot)
2. Click **"Start free trial"** or **"Buy now"**
3. Choose your plan
4. Complete the purchase/enrollment

**For Students:**
1. Go to [education.github.com](https://education.github.com/)
2. Apply for Student Developer Pack
3. Get free Copilot access

#### **Step 3: Install Copilot Extension**

1. Open VS Code
2. Click Extensions icon (or `Ctrl+Shift+X`)
3. Search for **"GitHub Copilot"**
4. Click **Install** on two extensions:
   - GitHub Copilot
   - GitHub Copilot Chat

#### **Step 4: Sign In to GitHub**

1. After installation, VS Code prompts for sign-in
2. Click **"Sign in to GitHub"**
3. Authorize VS Code in browser
4. Return to VS Code

#### **Step 5: Verify Installation**

1. Open a new file (e.g., `test.py`)
2. Type a comment: `# Function to add two numbers`
3. Press Enter
4. Wait for Copilot suggestion
5. If you see a suggestion, you're ready! ✅

### Configuration Settings

#### **Access Settings**
- Go to: File → Preferences → Settings
- Search for "Copilot"

#### **Recommended Settings**

**Enable Copilot:**
```json
{
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": true,
    "yaml": true
  }
}
```

**Inline Suggestions:**
```json
{
  "editor.inlineSuggest.enabled": true,
  "github.copilot.editor.enableAutoCompletions": true
}
```

**Chat Settings:**
```json
{
  "github.copilot.chat.localeOverride": "en",
  "github.copilot.editor.enableCodeActions": true
}
```

#### **Keyboard Shortcuts**

| Action | Windows/Linux | Mac |
|--------|--------------|-----|
| Accept suggestion | `Tab` | `Tab` |
| Reject suggestion | `Esc` | `Esc` |
| Next suggestion | `Alt+]` | `Opt+]` |
| Previous suggestion | `Alt+[` | `Opt+[` |
| Open inline chat | `Ctrl+I` | `Cmd+I` |
| Open chat panel | `Ctrl+Alt+I` | `Cmd+Shift+I` |
| Trigger suggestion | `Alt+\` | `Opt+\` |

### Setting Up Other IDEs

#### **Visual Studio**
1. Install Visual Studio 2022 or later
2. Go to Extensions → Manage Extensions
3. Search "GitHub Copilot"
4. Install and restart
5. Sign in to GitHub

#### **JetBrains IDEs** (IntelliJ, PyCharm, WebStorm)
1. Open IDE
2. Go to Settings → Plugins
3. Search "GitHub Copilot"
4. Install plugin
5. Restart IDE
6. Sign in to GitHub

#### **Neovim**
```bash
# Using vim-plug
Plug 'github/copilot.vim'

# Using packer
use 'github/copilot.vim'

# Authenticate
:Copilot setup
```

### Troubleshooting Common Issues

#### **Issue 1: Copilot Not Showing Suggestions**

**Solutions:**
- Check internet connection
- Verify subscription is active
- Check if file type is supported
- Toggle Copilot: `Ctrl+Shift+P` → "GitHub Copilot: Toggle"
- Restart VS Code

#### **Issue 2: Sign-In Problems**

**Solutions:**
- Clear VS Code cache
- Sign out and sign in again
- Check GitHub account has Copilot access
- Try different browser for authentication

#### **Issue 3: Slow Suggestions**

**Solutions:**
- Check internet speed
- Close unnecessary files
- Reduce number of extensions
- Clear Copilot cache
- Update to latest Copilot version

#### **Issue 4: Suggestions Not Relevant**

**Solutions:**
- Write clearer comments
- Provide more context
- Use descriptive variable names
- Break down complex tasks
- Try different phrasing

---

## Hands-On Exercises

### Exercise 1: Enable Copilot
1. Install GitHub Copilot extension in VS Code
2. Sign in with your GitHub account
3. Verify installation by getting your first suggestion

### Exercise 2: Test Different Chat Modes
1. **Inline Chat**: Select code and press `Ctrl+I`, ask "Explain this"
2. **Chat Panel**: Open chat panel, ask "How do I read a CSV file in Python?"
3. **Quick Chat**: Press `Ctrl+Shift+I`, ask "What is a decorator?"

### Exercise 3: Use Slash Commands
Try each slash command:
```python
# Write a function
def process_data(data):
    # TODO: implement

# Use /explain on the function
# Use /tests to generate tests
# Use /fix if there are errors
# Use /doc to add documentation
```

### Exercise 4: Configure Settings
1. Open VS Code settings
2. Search for "copilot"
3. Enable/disable suggestions for specific languages
4. Customize keyboard shortcuts
5. Test your configuration

### Exercise 5: Context Anchors
1. Create two files: `main.py` and `utils.py`
2. In chat, ask: "Explain the function in #file:utils.py"
3. Select code in `main.py`
4. Ask: "Refactor #selection to use the function from #file:utils.py"

---

## Code Examples

### Example 1: First Copilot Suggestion

**Your Input:**
```python
# Function to calculate the area of a circle
```

**Copilot Suggests:**
```python
# Function to calculate the area of a circle
def calculate_circle_area(radius):
    """Calculate the area of a circle given its radius."""
    import math
    return math.pi * radius ** 2
```

### Example 2: Using Chat for Help

**Chat Conversation:**
```
You: How do I connect to a PostgreSQL database in Python?

Copilot: Here's how to connect to PostgreSQL using psycopg2:

```python
import psycopg2

# Connect to database
conn = psycopg2.connect(
    host="localhost",
    database="mydb",
    user="postgres",
    password="your_password"
)

# Create cursor
cur = conn.cursor()

# Execute query
cur.execute("SELECT * FROM users")

# Fetch results
rows = cur.fetchall()

# Close connection
cur.close()
conn.close()
```

Install: pip install psycopg2-binary
```

### Example 3: Agent Mode Task

**Your Prompt:**
```
Create a simple Flask API with the following endpoints:
- GET /api/users - List all users
- GET /api/users/:id - Get user by ID
- POST /api/users - Create new user
- PUT /api/users/:id - Update user
- DELETE /api/users/:id - Delete user
```

**Copilot Agent Creates:**
```
app.py
models.py
routes.py
database.py
tests/test_api.py
requirements.txt
README.md
```

---

## Real-World Scenario 

### Scenario: Setting Up a Team Development Environment

**Context**: You're leading a team of 5 developers starting a new project.

**Setup Process:**

#### **Step 1: Choose Plan**
- Select **Copilot Business** for team
- Benefits: Organization management, usage insights, security

#### **Step 2: Organization Setup**
```bash
# Admin actions:
1. Go to Organization Settings
2. Enable GitHub Copilot for organization
3. Assign licenses to team members
4. Configure policies (content filters, etc.)
5. Set up audit logging
```

#### **Step 3: IDE Configuration**
Create a shared settings file (`.vscode/settings.json`):
```json
{
  "github.copilot.enable": {
    "*": true
  },
  "github.copilot.editor.enableAutoCompletions": true,
  "github.copilot.editor.enableCodeActions": true,
  "editor.inlineSuggest.enabled": true,
  "editor.suggest.showInlineDetails": true
}
```

#### **Step 4: Team Guidelines**
Create `COPILOT_GUIDELINES.md`:
```markdown
# Team Copilot Guidelines

## Best Practices
- Always review generated code
- Write clear prompts
- Use descriptive variable names
- Test all AI-generated code
- Apply responsible AI principles

## Dos and Don'ts
✅ DO use for boilerplate code
✅ DO use for test generation
✅ DO use for documentation

❌ DON'T share sensitive data in prompts
❌ DON'T skip code reviews
❌ DON'T assume correctness
```
---

## Lab: Complete Environment Setup (If you already setup don't need to setup again)

### Objective
Set up a fully configured development environment with GitHub Copilot optimized for your workflow.

### Instructions

#### **Part 1: Installation & Authentication**
1. Install VS Code
2. Install GitHub Copilot extensions
3. Sign in to GitHub
4. Verify installation with test file

#### **Part 2: Configuration**
1. Create custom settings for Copilot
2. Set up keyboard shortcuts
3. Configure language-specific settings
4. Install complementary extensions:
   - GitLens
   - Python (if using Python)
   - ESLint (if using JavaScript)
   - Prettier

#### **Part 3: Test Chat Modes**
Create a test file and try each mode:
1. **Inline Chat**: Get explanation of code
2. **Chat Panel**: Have a conversation about design patterns
3. **Quick Chat**: Ask for command help
4. Try all slash commands

#### **Part 4: Create Project Template**
Use Copilot to create a project template:
```
project-template/
├── .vscode/
│   ├── settings.json (Copilot configured)
│   └── extensions.json (Recommended extensions)
├── .github/
│   └── COPILOT_GUIDELINES.md
├── src/
│   └── main.py
├── tests/
│   └── test_main.py
├── .gitignore
├── requirements.txt
└── README.md
```

#### **Part 5: Document Your Setup**
Create `SETUP.md` documenting:
- Installation steps
- Configuration choices
- Custom shortcuts
- Troubleshooting tips
- Team guidelines (if applicable)

### Expected Outcome
- ✅ Fully functional Copilot environment
- ✅ Optimized settings for your workflow
- ✅ Understanding of all chat modes
- ✅ Proficiency with shortcuts and commands
- ✅ Project template for future use

### Deliverables
- Screenshot of working Copilot suggestion
- Your `settings.json` configuration
- `SETUP.md` documentation
- `project-template/` folder
- Reflection on setup experience

---

## Additional Resources

### Documentation
- [GitHub Copilot Plans](https://docs.github.com/en/copilot/overview-of-github-copilot/about-github-copilot-for-individuals)
- [Setting Up Copilot](https://docs.github.com/en/copilot/getting-started-with-github-copilot)
- [VS Code Copilot Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)

### Video Tutorials
- [Getting Started with GitHub Copilot](https://www.youtube.com/watch?v=hPVatUSvZq0)
- [VS Code Setup Guide](https://www.youtube.com/watch?v=XXXXXXXXXXXX)

### Community
- [GitHub Copilot Discussion Forum](https://github.com/Mazik-Pakistan/Training-AI-Enabled-Developer/discussions)
- [VS Code Community](https://code.visualstudio.com/community)

---

## Summary

In this unit, you learned:
- ✅ Different GitHub Copilot plans and how to choose
- ✅ Various chat modes and when to use them
- ✅ How to set up and configure Copilot
- ✅ Slash commands and context anchors
- ✅ Troubleshooting common issues
- ✅ Best practices for team setup

**Next:** Module 2 - Foundations & Inline Code

---

## Module 1 Complete! 🎉

You've finished the Introduction to GitHub & Copilot module. You now have:
- ✅ Understanding of GitHub fundamentals
- ✅ Knowledge of GitHub Copilot capabilities
- ✅ Configured development environment
- ✅ Experience with responsible AI principles

Ready to dive deeper? Let's move to **Module 2: Foundations & Inline Code**!
