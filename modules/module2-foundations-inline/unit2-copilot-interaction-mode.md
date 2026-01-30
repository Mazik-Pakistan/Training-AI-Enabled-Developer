# Unit 2: Copilot Interaction Modes

## Learning Objectives
After completing this unit, you will be able to:
- Master the three core Copilot interaction modes: Ask, Edit, and Agent
- Use GitHub Copilot Ask Mode for learning and problem-solving
- Use GitHub Copilot Edit Mode for code modifications and refactoring
- Use GitHub Copilot Agent Mode for autonomous complex tasks
- Apply Copilot across multiple programming languages and environments
- Choose the right mode for different development scenarios

---

## 1. Understanding Copilot Interaction Modes

### The Three Core Interaction Modes

GitHub Copilot provides three primary interaction modes, each designed for different development tasks:

**1. Ask Mode** - Conversational Learning & Guidance
- Ask questions, get explanations
- Learn concepts and best practices
- Explore solutions without generating code
- Best for: Understanding, learning, problem-solving

**2. Edit Mode** - Code Modification & Refactoring
- Make targeted code changes
- Fix issues, add features, refactor
- Quick edits with context awareness
- Best for: Modifying existing code, quick fixes

**3. Agent Mode** - Autonomous Complex Tasks
- Multi-step task execution
- Work across multiple files
- Complex implementations and refactoring
- Best for: Sophisticated features, large-scale changes

### Mode Selection Guide

| Scenario | Mode | Why |
|----------|------|-----|
| "How do I implement OAuth?" | Ask | Need guidance and understanding |
| "Add error handling to this function" | Edit | Modify specific code |
| "Create a full API with auth" | Agent | Complex multi-file task |
| "What's the difference between async/await?" | Ask | Learning conceptual knowledge |
| "Refactor this component" | Edit | Improve specific code |
| "Build a microservice" | Agent | Large autonomous task |

<p align="center">
  <a href="https://www.youtube.com/watch?v=s7Qzq0ejhjg">
    <img src="https://img.youtube.com/vi/s7Qzq0ejhjg/maxresdefault.jpg" width="600" alt="Click to play video">
  </a><br>
  <em>▶ Click to play video</em>
</p>

---

## 2. Ask Mode: Learning & Problem-Solving

### Multi-Language Across All Modes

GitHub Copilot supports **dozens of programming languages** across Ask, Edit, and Agent modes.

**Supported Languages:**
- Python, JavaScript, TypeScript, Java, C#, C++, Go, Ruby, PHP
- HTML, CSS, SQL, Shell scripts, PowerShell
- Rust, Swift, Kotlin, Scala, R, Julia, Dart
- And many more...

### How Copilot Adapts to Different Languages

```
Same Intent, Different Languages:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Comment: "Function to calculate factorial"

┌──────────┬──────────────────────────────┐
│ Python   │ def factorial(n):            │
│          │     if n == 0: return 1      │
│          │     return n * factorial(n-1)│
├──────────┼──────────────────────────────┤
│JavaScript│ function factorial(n) {      │
│          │   if (n === 0) return 1;     │
│          │   return n * factorial(n-1); │
│          │ }                            │
├──────────┼──────────────────────────────┤
│ Java     │ public int factorial(int n) {│
│          │   if (n == 0) return 1;      │
│          │   return n * factorial(n-1); │
│          │ }                            │
└──────────┴──────────────────────────────┘
```

### Language-Specific Features

#### **Python**
Copilot understands Python idioms and conventions:

```python
# Type hints and docstrings
def process_data(data: list[dict]) -> pd.DataFrame:
    """Process raw data into DataFrame."""
    # Copilot suggests pandas-based implementation

# List comprehensions
numbers = [1, 2, 3, 4, 5]
# Type: squares = 
# Copilot suggests: squares = [n**2 for n in numbers]

# Context managers
# Type: with open
# Copilot suggests: with open('file.txt', 'r') as f:

# Decorators
# Type: @property
# Copilot understands property pattern
```

#### **JavaScript/TypeScript**
Copilot adapts to JavaScript patterns:

```javascript
// Arrow functions
// Type: const sum = 
// Copilot suggests: const sum = (a, b) => a + b;

// Promises and async/await
// Type: async function fetchData
async function fetchData(url) {
    // Copilot suggests Promise-based implementation
    try {
        const response = await fetch(url);
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
    }
}

// React components
// Type: function UserCard
function UserCard({ name, email, avatar }) {
    // Copilot suggests JSX structure
    return (
        <div className="user-card">
            <img src={avatar} alt={name} />
            <h3>{name}</h3>
            <p>{email}</p>
        </div>
    );
}
```

#### **TypeScript**
Copilot leverages type information:

```typescript
// Interface-driven development
interface User {
    id: number;
    name: string;
    email: string;
}

// Type: function createUser
// Copilot suggests with proper types
function createUser(data: Partial<User>): User {
    return {
        id: Date.now(),
        name: data.name || 'Anonymous',
        email: data.email || ''
    };
}

// Generics
// Type: function identity<T>
function identity<T>(arg: T): T {
    return arg;
}
```

#### **Java**
Copilot follows Java conventions:

```java
// Class structure
// Type: public class BankAccount
public class BankAccount {
    private String accountNumber;
    private double balance;
    
    public BankAccount(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0.0;
    }
    
    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        }
    }
    
    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            this.balance -= amount;
            return true;
        }
        return false;
    }
}
```

#### **SQL**
Copilot generates database queries:

```sql
-- Type: SELECT users with orders
SELECT 
    u.id,
    u.name,
    u.email,
    COUNT(o.id) as order_count,
    SUM(o.total) as total_spent
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name, u.email
HAVING COUNT(o.id) > 0
ORDER BY total_spent DESC;

-- Type: CREATE TABLE products
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL,
    stock INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Cross-Language Development

Working on projects with multiple languages:

**Example: Full-Stack Application**

**Backend (Python - Flask):**
```python
# app.py
from flask import Flask, jsonify, request

app = Flask(__name__)

# Type: @app.route('/api/users', methods=['GET'])
@app.route('/api/users', methods=['GET'])
def get_users():
    # Copilot suggests database query and JSON response
    users = User.query.all()
    return jsonify([user.to_dict() for user in users])

@app.route('/api/users', methods=['POST'])
def create_user():
    data = request.get_json()
    # Copilot suggests validation and creation
    user = User(name=data['name'], email=data['email'])
    db.session.add(user)
    db.session.commit()
    return jsonify(user.to_dict()), 201
```

**Frontend (JavaScript - React):**
```javascript
// UserList.js
import React, { useState, useEffect } from 'react';

// Type: function UserList
function UserList() {
    // Copilot suggests state management and API calls
    const [users, setUsers] = useState([]);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        fetch('/api/users')
            .then(response => response.json())
            .then(data => {
                setUsers(data);
            .catch(error => console.error('Error:', error));
    }, []);

    if (loading) return <div>Loading...</div>;

    return (
        <div className="user-list">
            {users.map(user => (
                <div key={user.id} className="user-card">
                    <h3>{user.name}</h3>
                    <p>{user.email}</p>
                </div>
            ))}
        </div>
    );
}
```

**Database (SQL):**
```sql
-- schema.sql
-- Type: CREATE TABLE users
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Type: CREATE INDEX for email lookups
CREATE INDEX idx_users_email ON users(email);
```

---

## 2. GitHub Copilot Ask Mode

### What is Ask Mode?

Ask Mode is Copilot's conversational interface where you can ask questions, get explanations, and receive guidance without generating code directly.

**Difference from Code Completion:**
- **Code Completion**: Generates code inline
- **Ask Mode**: Provides explanations, answers, and guidance

### When to Use Ask Mode

✅ **Learning and Understanding**
- "How does async/await work in JavaScript?"
- "What's the difference between let and const?"
- "Explain the SOLID principles"

✅ **Problem Solving**
- "How do I handle CORS errors in Express?"
- "What's the best way to validate email in Python?"
- "How can I optimize this database query?"

✅ **Best Practices**
- "What are REST API best practices?"
- "How should I structure my React application?"
- "What's the recommended way to handle errors in Go?"

✅ **Debugging Help**
- "Why is my useState not updating?"
- "What causes 'Cannot read property of undefined'?"
- "How do I debug memory leaks in Node.js?"

### Accessing Ask Mode

**Method 1: Chat Panel**
1. Open Copilot Chat (`Ctrl+Alt+I`)
2. Type your question
3. Press Enter

**Method 2: Quick Chat**
1. Press `Ctrl+Shift+I`
2. Ask quick question
3. Get instant answer

**Method 3: Inline Chat**
1. Press `Ctrl+I` in editor
2. Ask contextual question
3. Get response inline

### Effective Questions in Ask Mode

#### **Poor Questions:**
❌ "Code"
❌ "Help"
❌ "Fix"

#### **Good Questions:**
✅ "How do I implement JWT authentication in Express.js?"
✅ "What's the difference between @Component and @Injectable in Angular?"
✅ "Explain how garbage collection works in Python"

### Ask Mode Examples

**Example 1: Learning Concepts**

**You ask:** 
```
What is the difference between SQL JOIN types?
```

**Copilot responds:**
```
SQL has several JOIN types:

1. INNER JOIN
   - Returns only matching rows from both tables
   - Example: Users who have placed orders

2. LEFT JOIN (LEFT OUTER JOIN)
   - Returns all rows from left table
   - Matching rows from right table (NULL if no match)
   - Example: All users, with their orders if any

3. RIGHT JOIN (RIGHT OUTER JOIN)
   - Returns all rows from right table
   - Matching rows from left table (NULL if no match)

4. FULL OUTER JOIN
   - Returns all rows from both tables
   - NULL where no match exists

Visual representation:
```sql
-- INNER JOIN
SELECT u.name, o.order_id
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN
SELECT u.name, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```
```

**Example 2: Problem Solving**

**You ask:**
```
How do I make multiple API calls in parallel in JavaScript?
```

**Copilot responds:**
```
You can use Promise.all() to make parallel API calls:

```javascript
// Method 1: Promise.all (fails if any request fails)
async function fetchAllData() {
    try {
        const [users, posts, comments] = await Promise.all([
            fetch('/api/users').then(r => r.json()),
            fetch('/api/posts').then(r => r.json()),
            fetch('/api/comments').then(r => r.json())
        ]);
        return { users, posts, comments };
    } catch (error) {
        console.error('One or more requests failed:', error);
    }
}

// Method 2: Promise.allSettled (continues even if some fail)
async function fetchAllDataSafely() {
    const results = await Promise.allSettled([
        fetch('/api/users').then(r => r.json()),
        fetch('/api/posts').then(r => r.json()),
        fetch('/api/comments').then(r => r.json())
    ]);
    
    return results.map(result => 
        result.status === 'fulfilled' ? result.value : null
    );
}
```

Choose Promise.all when all requests must succeed.
Choose Promise.allSettled when you want partial results.
```


**Example 3: Debugging**

**You ask:**
```
Why does this React component render twice?
```javascript
function Counter() {
    const [count, setCount] = useState(0);
    console.log('Rendering...', count);
    return <div onClick={() => setCount(count + 1)}>{count}</div>;
}
```
```

**Copilot responds:**
```
Your component renders twice due to React 18's Strict Mode:

1. In development, React deliberately mounts components twice to help find bugs
2. This only happens in development mode, not production
3. It helps detect side effects in component lifecycle

To verify this is the cause:
- Check if you're using <React.StrictMode> in your app
- This is intentional and helps catch bugs early

If you want to disable double rendering (not recommended):
Remove <React.StrictMode> from index.js

If the double rendering causes issues with side effects:
Use useEffect with cleanup:
```javascript
function Counter() {
    const [count, setCount] = useState(0);
    
    useEffect(() => {
        console.log('Effect running', count);
        // Cleanup function
        return () => {
            console.log('Cleanup', count);
        };
    }, [count]);
    
    return <div onClick={() => setCount(count + 1)}>{count}</div>;
}
```


---

## 3. Edit Mode: Code Modification & Refactoring

### What is Edit Mode?

Edit Mode enables quick, targeted code modifications using Copilot's contextual understanding. It's the fastest way to make changes to existing code.

**Edit Mode Methods:**
- **Inline Chat** (`Ctrl+I`): Direct editing with code context
- **Code Actions**: Right-click or lightbulb menu suggestions
- **Context-Aware Editing**: Understand surrounding code

### When to Use Edit Mode

✅ **Code Modification**
- "Add error handling to this function"
- "Add logging to this component"
- "Refactor this code to use async/await"

✅ **Bug Fixes**
- "Fix the null reference issue"
- "Handle edge cases in this function"
- "Add validation to this form"

✅ **Enhancement**
- "Add comments explaining this logic"
- "Optimize this query"
- "Add type hints"

✅ **Code Generation**
- "Generate unit tests for this function"
- "Create a mock object for testing"
- "Add JSDoc comments"

### Using Inline Chat (Edit Mode)

**Step-by-Step:**
1. Select code to modify
2. Press `Ctrl+I`
3. Describe the change you want
4. Review Copilot's suggestion
5. Accept or iterate

**Example: Adding Error Handling**

```python
# Original code
def process_data(data):
    result = json.loads(data)
    return result['value'] * 2

# Selected entire function
# Press Ctrl+I
# Type: "Add error handling and logging"

# Result:
def process_data(data):
    try:
        result = json.loads(data)
        if 'value' not in result:
            raise ValueError("Missing 'value' key")
        logger.info(f"Processing data: {data}")
        return result['value'] * 2
    except json.JSONDecodeError as e:
        logger.error(f"Invalid JSON: {e}")
        raise
    except ValueError as e:
        logger.error(f"Validation error: {e}")
        raise
```

### Edit Mode Code Actions

**Available Actions:**
- **Explain**: Understand code functionality
- **Fix**: Address errors and issues
- **Generate Tests**: Create unit tests
- **Document**: Add comments and docstrings
- **Refactor**: Improve code structure

**Using Code Actions:**
1. Select code
2. Right-click or click lightbulb icon
3. Choose action from menu
4. Copilot implements the action

### Edit Mode Examples

**Example 1: Refactor to Async**

```javascript
// Original
function fetchUserData(userId) {
    const userData = fetch(`/api/users/${userId}`);
    return userData;
}

// Select and press Ctrl+I
// Prompt: "Convert to async/await"

// Result:
async function fetchUserData(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`);
        const userData = await response.json();
        return userData;
    } catch (error) {
        console.error('Error fetching user data:', error);
        throw error;
    }
}
```

**Example 2: Add Type Safety**

```typescript
// Original
function calculateTotal(items) {
    return items.reduce((sum, item) => sum + item.price, 0);
}

// Select and press Ctrl+I
// Prompt: "Add TypeScript types"

// Result:
interface Item {
    name: string;
    price: number;
}

function calculateTotal(items: Item[]): number {
    return items.reduce((sum, item) => sum + item.price, 0);
}
```

**Example 3: Add Validation**

```python
# Original
def create_user(name, email):
    user = User(name=name, email=email)
    db.session.add(user)
    db.session.commit()
    return user

# Select and press Ctrl+I
# Prompt: "Add input validation"

# Result:
def create_user(name: str, email: str) -> User:
    if not name or len(name.strip()) == 0:
        raise ValueError("Name cannot be empty")
    
    if not email or '@' not in email:
        raise ValueError("Invalid email format")
    
    if User.query.filter_by(email=email).first():
        raise ValueError("Email already exists")
    
    user = User(name=name, email=email)
    db.session.add(user)
    db.session.commit()
    return user
```

---

## 4. Agent Mode: Autonomous Complex Tasks

### What is Agent Mode?

Agent Mode is Copilot's most sophisticated interaction method. It autonomously handles complex, multi-step tasks that span multiple files and require sophisticated decision-making.

**Characteristics:**
- **Autonomous**: Works independently on complex tasks
- **Multi-file**: Creates and modifies multiple files
- **Intelligent**: Makes architectural decisions
- **Complete**: Produces fully functional implementations

### When to Use Agent Mode

✅ **Creating Complex Features**
- "Build a REST API with authentication"
- "Create a user management system"
- "Implement a payment processing module"

✅ **Large Refactoring**
- "Convert this codebase from callbacks to async/await"
- "Migrate from JavaScript to TypeScript"
- "Extract common utilities into a shared library"

✅ **Full Application Building**
- "Create a blog application with posts, comments, and user authentication"
- "Build a task management system"
- "Generate a microservice architecture"

✅ **Complex Integration**
- "Integrate OAuth2 authentication"
- "Add database migrations and seeders"
- "Set up comprehensive testing framework"

### Using Agent Mode

**Access Agent Mode:**
- Open Copilot Chat (`Ctrl+Alt+I`)
- Click "Agent" toggle or use `@agent` mention
- Describe your complex task
- Copilot handles multi-file implementation

**Best Practices:**
1. Be specific about requirements
2. Mention technology stack
3. Describe architectural needs
4. Include testing requirements

### Agent Mode Example

**Prompt:**
```
@agent Create a REST API for a blog application with:
- User authentication using JWT
- Post management (CRUD operations)
- Comment system on posts
- Error handling and logging
- Unit tests for all endpoints
Use Python with Flask and SQLAlchemy.
```

**Agent Creates:**
```
✓ app.py - Main Flask application
✓ models.py - SQLAlchemy models (User, Post, Comment)
✓ auth.py - Authentication logic with JWT
✓ routes.py - All API endpoints
✓ requirements.txt - Python dependencies
✓ tests/test_api.py - Comprehensive unit tests
✓ config.py - Configuration management
✓ README.md - Setup instructions
```

### Agent Mode vs. Other Modes

| Task | Agent Mode | Edit Mode | Ask Mode |
|------|-----------|-----------|----------|
| "Build API" | ✅ Best | ❌ Too slow | ✅ Ask first |
| "Fix one function" | ❌ Overkill | ✅ Best | ❌ Not applicable |
| "Understand OAuth" | ❌ Not useful | ❌ Not useful | ✅ Best |
| "Add tests" | ✅ Good | ✅ Also good | ❌ Not applicable |
| "Refactor codebase" | ✅ Best | ✅ Tedious | ❌ Not applicable |

---

## 5. Multi-Language Support Across Modes

### Work Across Multiple Programming Languages

---

## 6. Putting It All Together: Mode Workflows

### Integrated Development Workflow

**Scenario: Build a feature with all three modes**

```
Task: Add user authentication to existing app

┌─────────────────────────────────────────────────────────────────┐
│ Step 1: ASK MODE (Learn & Plan)                                 │
├─────────────────────────────────────────────────────────────────┤
│ Open Chat Panel (Ctrl+Alt+I)                                    │
│ Ask: "What's the best approach for JWT auth?"                   │
│ Get: Overview, best practices, considerations                   │
│                                                                 │
│ Output: Understanding of implementation approach                │
└─────────────────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 2: AGENT MODE (Build Complex Feature)                      │
├─────────────────────────────────────────────────────────────────┤
│ Mention: @agent                                                 │
│ Request: "Implement JWT authentication with                     │
│          refresh tokens, password hashing,                      │
│          and middleware"                                        │
│                                                                 │
│ Output: Complete auth system across multiple files              │
└─────────────────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────────────────┐
│ Step 3: EDIT MODE (Refine & Customize)                          │
├─────────────────────────────────────────────────────────────────┤
│ Select auth function                                            │
│ Ctrl+I: "Add rate limiting to login endpoint"                   │
│ Review and accept changes                                       │
│                                                                 │
│ Output: Enhanced and hardened implementation                    │
└─────────────────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────────────────┐
│ RESULT: Fully implemented, tested, optimized                    │
└─────────────────────────────────────────────────────────────────┘
```

### Common Workflows by Scenario

**Workflow 1: Learning & Implementation**
```
Ask → Understand concept
  ↓
Agent → Build basic implementation
  ↓
Edit → Add advanced features
  ↓
Ask → Learn testing strategies
  ↓
Edit → Add comprehensive tests
```

**Workflow 2: Debugging & Fixing**
```
Ask → Understand the error
  ↓
Edit → Apply quick fix
  ↓
Edit → Add error handling
  ↓
Agent → Refactor for robustness
```

**Workflow 3: Feature Development**
```
Ask → Explore best practices
  ↓
Agent → Create feature framework
  ↓
Edit → Customize to requirements
  ↓
Edit → Add edge case handling
  ↓
Agent → Generate tests
```

---

## Hands-On Exercises

### Exercise 1: Master All Three Modes

**Objective**: Use Ask, Edit, and Agent modes in sequence

**Task**: Create a data validation system

**Step 1: Ask Mode**
```
Open Chat Panel (Ctrl+Alt+I)
Ask: "What are best practices for input validation in [your language]?"
Take notes on recommended patterns
```

**Step 2: Agent Mode**
```
Use @agent mention
Request: "Create a comprehensive data validator with:
  - Email validation
  - Phone number validation
  - URL validation
  - Custom rule support"
Review generated code
```

**Step 3: Edit Mode**
```
Select one validator function
Press Ctrl+I
Request: "Add comprehensive error messages and logging"
Review and accept changes
```

**Reflection**:
- How did each mode contribute to the final result?
- When would you choose one mode over another?
- How did understanding (Ask) improve your edits?

### Exercise 2: Multi-Language Challenge

Create the same feature in three different languages:

**Feature:** Function to validate email, check if it exists in database

**Instructions:**
1. Use Inline Completion to generate each function
2. Ask Copilot to add error handling
3. Use Ask Mode to explain differences between implementations

**Python:**
```python
# Prompt: "Function to validate email format and check if exists in database using SQLAlchemy"
# Copilot will suggest:
# - regex pattern matching for email validation
# - SQLAlchemy query to check database
# - proper error handling
import re
from models import User

def validate_and_check_email(email):
    """Validate email format and check if exists in database."""
    # Start typing and let Copilot complete
```

**JavaScript:**
```javascript
// Prompt: "Function to validate email format and check if user exists in database using Mongoose"
// Copilot will suggest:
// - regex pattern for validation
// - async/await for database query
// - Promise-based error handling
const User = require('./models/User');

async function validateAndCheckEmail(email) {
    // Start typing and let Copilot complete
}
```

**TypeScript:**
```typescript
// Prompt: "Function to validate email format and check if exists in database with type safety"
// Copilot will suggest:
// - interface definitions for User
// - typed return values
// - strict null checks
interface User {
    id: number;
    email: string;
}

async function validateAndCheckEmail(email: string): Promise<boolean> {
    // Start typing and let Copilot complete
}
```

**Reflection Questions:**
- How did the implementations differ across languages?
- What patterns did Copilot use in each language?
- How would you handle errors differently in each language?

### Exercise 3: Ask Mode Deep Dive

Use Ask Mode (Chat Panel) to explore:
1. "What are Python generators and when should I use them?"
2. "Explain the difference between var, let, and const in JavaScript"
3. "What is the purpose of Docker and how does it work?"
4. "How do I optimize SQL queries for large datasets?"

**Follow-up**: For each answer, ask 2-3 follow-up questions to deepen understanding

### Exercise 4: Edit Mode Mastery

Practice targeted code modifications:

1. **Create** a simple function (or find existing code)
2. **Use Ctrl+I** to request these edits:
   - "Add comprehensive error handling"
   - "Add logging statements"
   - "Add input validation"
   - "Add TypeScript/type hints"
3. **Review** each change
4. **Iterate** on the suggestions

### Exercise 5: Agent Mode Complete Build

Build a complete feature using Agent Mode:

1. Open Chat Panel (`Ctrl+Alt+I`)
2. Use `@agent` to access Agent Mode
3. Request: "Create a user registration system with:
   - Email validation
   - Password requirements
   - Duplicate email checking
   - JWT token generation
   - Unit tests"
4. Review the generated structure
5. Use Edit Mode to customize specific parts

### Exercise 6: Integrated Workflow

Combine all three modes to build a feature:

1. **Ask**: "What's the best way to implement caching?"
2. **Agent**: "Create a caching layer for database queries"
3. **Edit**: "Optimize the cache invalidation logic"
4. **Ask**: "How do I test caching behavior?"
5. **Edit**: "Generate tests for cache operations"

---

## 7. Real-World Scenarios

### Scenario 1: Learning & Building (Ask → Agent → Edit)

**Context**: Implementing OAuth2 authentication

**Step 1: Ask Mode - Understand OAuth2**
```
Chat: "Explain OAuth2 flow and when to use it"
Result: Comprehensive understanding of OAuth2 concepts
```

**Step 2: Agent Mode - Build OAuth2 Implementation**
```
@agent: "Create OAuth2 authentication with:
  - GitHub provider integration
  - Secure token storage
  - Refresh token mechanism
  - Middleware for protected routes"
Result: Complete OAuth2 system across multiple files
```

**Step 3: Edit Mode - Enhance Security**
```
Ctrl+I on token storage: "Add encryption for sensitive tokens"
Ctrl+I on middleware: "Add rate limiting to auth endpoints"
Result: Production-ready security enhancements
```

### Scenario 2: Debugging (Ask → Edit)

**Context**: Fixing authentication issues

**Step 1: Ask Mode - Understand the Issue**
```
Chat: "Why might JWT tokens fail after deployment?"
Result: Understanding of common JWT issues
```

**Step 2: Edit Mode - Apply Fixes**
```
Ctrl+I: "Add JWT expiration handling and refresh logic"
Ctrl+I: "Add proper error messages for token validation"
Result: Fixed authentication system
```

### Scenario 3: Large Refactoring (Ask → Agent → Edit)

**Context**: Modernizing legacy code

**Step 1: Ask Mode - Learn Best Practices**
```
Chat: "What's the best way to modernize a callback-based codebase?"
Result: Understanding of migration strategies
```

**Step 2: Agent Mode - Large-Scale Refactoring**
```
@agent: "Convert this callback-based API to use async/await"
Result: Entire codebase modernized
```

**Step 3: Edit Mode - Polish & Optimize**
```
Ctrl+I: "Optimize for performance and add error handling"
Result: Production-ready modernized code
```

---

## Lab: Full-Stack Development with Copilot Modes

### Objective
Build a complete application using Ask, Edit, and Agent modes across multiple languages.

### Project: Task Management System

**Requirements:**
1. **Backend API** (Python/Flask)
   - User authentication
   - Task CRUD operations
   - RESTful endpoints

2. **Frontend** (HTML/CSS/JavaScript)
   - Login form
   - Task list display
   - Add/edit/delete tasks

3. **Database** (SQL)
   - User table
   - Tasks table
   - Proper relationships

4. **CLI Tool** (Python)
   - Command-line task manager
   - Uses the API

### Instructions

**Part 1: Ask Mode - Understand the Architecture**

1. Open Chat Panel (`Ctrl+Alt+I`)
2. Ask:
   - "What's the best architecture for a task management app?"
   - "How should I structure authentication and authorization?"
   - "What testing strategy should I use for both frontend and backend?"
3. Document the recommendations

**Part 2: Agent Mode - Build Complete Backend**

1. Use `@agent` in Chat Panel
2. Request:
```
@agent Create a Flask API for task management with:
- User authentication using JWT
- Task CRUD endpoints
- Category system for tasks
- Due date and priority tracking
- Comprehensive error handling
- Database migrations
- Unit tests for all endpoints

Include models.py, routes.py, auth.py, config.py, tests/
```

**Part 3: Agent Mode - Build Frontend**

1. Use `@agent` again
2. Request:
```
@agent Create a React-based frontend for task management:
- Login/registration interface
- Task list with filters
- Add/edit/delete task forms
- Task detail view
- API client integration
- Responsive design
```

**Part 4: Edit Mode - Customize and Enhance**

1. Select authentication logic → `Ctrl+I` → "Add rate limiting and security headers"
2. Select frontend form → `Ctrl+I` → "Add client-side validation and error display"
3. Select database models → `Ctrl+I` → "Add data integrity constraints"

**Part 5: Agent Mode - Database & Tests**

1. Use `@agent` to generate:
```
@agent Generate:
- SQL schema for users, tasks, and categories
- Database migration scripts
- Seed data for testing
- Integration tests
```

**Part 6: Documentation**

Use Ask Mode for documentation questions:
- "What should be in a comprehensive API documentation?"
- "How do I document authentication flows?"
- "What deployment considerations matter most?"

Create:
- `README.md` - Setup and usage
- `API.md` - Endpoint documentation
- `ARCHITECTURE.md` - System design
- `DEPLOYMENT.md` - Deployment guide

### Deliverables
- ✅ Complete working application (frontend + backend + database)
- ✅ All files properly organized
- ✅ Comprehensive tests
- ✅ Complete documentation
- ✅ REFLECTION.md on using different Copilot modes

**Reflection Questions:**
- How did Ask Mode prepare you for Agent Mode?
- When was Edit Mode most useful?
- How did combining modes improve the final product?
- Which mode was most productive for your workflow?

---

## Additional Resources

### Documentation
- [GitHub Copilot Interaction Modes](https://docs.github.com/en/copilot/using-github-copilot/getting-started-with-github-copilot)
- [Chat Interface Documentation](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-chat)
- [Agent Mode Documentation](https://docs.github.com/en/copilot/using-github-copilot/agent-mode)
- [Multi-Language Support](https://docs.github.com/en/copilot/getting-started-with-github-copilot/supported-languages)

### Community
- [Copilot Discussions](https://github.com/orgs/community/discussions/categories/copilot)
- [GitHub Copilot Tips & Tricks](https://github.com/topics/github-copilot)

---

## Knowledge Check

### Quick Quiz

1. What are the three core Copilot interaction modes?
2. When should you use Ask Mode vs. Edit Mode?
3. What types of tasks is Agent Mode best for?
4. Describe a workflow that uses all three modes together
5. How does context affect mode selection?
6. Name 5 programming languages Copilot supports

### Answers
1. **Ask Mode** (learning & guidance), **Edit Mode** (code modification), **Agent Mode** (autonomous complex tasks)
2. **Ask Mode** for understanding and learning; **Edit Mode** for targeted code changes
3. Complex multi-file features, large refactoring, full application building
4. Ask to learn → Agent to build → Edit to customize/enhance
5. Simple tasks → Ask/Edit; complex/multi-file → Agent; understanding concepts → Ask
6. Python, JavaScript, TypeScript, Java, Go, C++, SQL, and many others

---

## Summary

In this unit, you learned:
- ✅ The three core Copilot interaction modes (Ask, Edit, Agent)
- ✅ When to use each mode for different scenarios
- ✅ How to combine modes for optimal workflows
- ✅ Ask Mode for learning and problem-solving
- ✅ Edit Mode for precise code modifications
- ✅ Agent Mode for complex autonomous tasks
- ✅ How to apply these modes across multiple programming languages
- ✅ Real-world development scenarios using all modes

**Next:** [Module 3 - Copilot As Assistant / Conversational Development Workflows](../module3-copilot-assistant/README.md)

---

## Module 2 Complete! 🎉

You've mastered Copilot's core interaction modes:
- ✅ Ask Mode - Learn and explore
- ✅ Edit Mode - Modify and refactor
- ✅ Agent Mode - Build autonomously
- ✅ Multi-language support
- ✅ Workflow integration

Ready for advanced conversational development? Let's move to **Module 3**!
