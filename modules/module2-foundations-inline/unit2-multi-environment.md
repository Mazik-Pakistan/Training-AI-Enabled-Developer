# Unit 2: Multi-Environment Support

## Learning Objectives
After completing this unit, you will be able to:
- Use GitHub Copilot across multiple programming languages
- Leverage GitHub Copilot Ask Mode effectively
- Switch between different Copilot interaction modes
- Understand language-specific Copilot features
- Apply consistent prompting across different languages

---

## 1. Work Across Multiple Programming Languages

### Copilot's Multi-Language Support

GitHub Copilot supports **dozens of programming languages**, making it versatile for polyglot developers.

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
                setLoading(false);
            })
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

## 3. Explore Different GitHub Copilot Interaction Modes

### Overview of Interaction Modes

GitHub Copilot offers five main interaction modes, each designed for different use cases:

**1. Inline Completion** (Automatic)
- Auto-suggestions appear as you type
- Press `Tab` to accept suggestions
- Best for writing code quickly

**2. Inline Chat** (`Ctrl+I`)
- Ask contextual questions about selected code
- Request quick edits and modifications
- Immediate inline responses

**3. Chat Panel** (`Ctrl+Alt+I`)
- Extended multi-turn conversations
- Perfect for learning and exploration
- Maintains conversation history

**4. Quick Chat** (`Ctrl+Shift+I`)
- Fast one-off questions
- No context switching needed
- Quick answers without panels

**5. Agent Mode**
- Multi-step autonomous task execution
- Complex implementations across multiple files
- Advanced feature for sophisticated workflows

### Mode Comparison Table

| Mode | Best For | Context Awareness | Output Type |
|------|----------|-------------------|-------------|
| **Inline Completion** | Writing code | Current file, open files | Code suggestions |
| **Inline Chat** | Quick questions | Selected code | Inline response |
| **Chat Panel** | Learning, debugging | Referenced files | Explanations, code |
| **Quick Chat** | One-off questions | Current file | Quick answers |
| **Agent Mode** | Complex tasks | Entire workspace | Multiple files |

### Choosing the Right Mode

#### **Use Inline Completion when:**
- Writing new code
- Completing partially written code
- Following established patterns
- Speed is priority

**Example:**
```python
# Just start typing and let Copilot complete
def calculate_
# Copilot completes immediately
```

#### **Use Inline Chat when:**
- You need to modify specific code
- Quick question about selection
- Want inline fix or explanation

**Example:**
1. Select code
2. Press `Ctrl+I`
3. Type: "Add error handling"
4. Get inline modification

#### **Use Chat Panel when:**
- Learning new concepts
- Complex multi-step guidance
- Need to maintain conversation history
- Exploring different approaches

**Example:**
```
You: How do I implement OAuth2 in Node.js?
[Detailed explanation follows]
You: Can you show me the token refresh logic?
[Builds on previous context]
You: What about storing tokens securely?
[Continues conversation]
```

#### **Use Quick Chat when:**
- Fast lookup needed
- Don't want to lose editor focus
- Terminal command help
- Quick syntax check

**Example:**
- `Ctrl+Shift+I`
- "What's the git command to undo last commit?"
- Get answer instantly
- Continue working

#### **Use Agent Mode when:**
- Implementing complex features
- Creating multiple related files
- Refactoring large codebases
- Need autonomous task completion

**Example:**
```
Prompt: "Create a RESTful API for a blog with posts, 
         comments, and authentication"

Agent creates:
- models.py
- routes.py
- auth.py
- tests/test_api.py
- requirements.txt
```

### Switching Between Modes

**Workflow Example:**

```
Task: Add user authentication to application

Step 1: Ask Mode (Chat Panel)
→ "What's the best way to implement authentication in Flask?"
→ Get overview and recommendations

Step 2: Inline Completion
→ Start implementing suggested approach
→ Let Copilot complete auth functions

Step 3: Inline Chat
→ Select generated code
→ "Add password hashing with bcrypt"

Step 4: Quick Chat
→ "How do I test authentication endpoints?"

Step 5: Inline Completion
→ Write test cases with Copilot assistance
```

---

## Hands-On Exercises

### Exercise 1: Multi-Language Challenge

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

### Exercise 2: Ask Mode Practice

Use Ask Mode to answer these questions:
1. "What are Python generators and when should I use them?"
2. "Explain the difference between var, let, and const in JavaScript"
3. "What is the purpose of Docker and how does it work?"
4. "How do I optimize SQL queries for large datasets?"

### Exercise 3: Mode Switching

Complete this task using different modes:

1. **Chat Panel**: Ask "How do I create a REST API in Flask?"
2. **Inline Completion**: Implement the basic structure
3. **Inline Chat**: Add error handling to one endpoint
4. **Quick Chat**: Ask "How to test Flask endpoints?"
5. **Inline Completion**: Write test cases

### Exercise 4: Cross-Language Project

Create a simple full-stack project:
- **Backend**: Python/Flask API
- **Frontend**: HTML/JavaScript
- **Database**: SQL schema

Use Copilot to generate all components.

---

## Real-World Scenario

### Scenario: Microservices Development

**Context**: Building microservices with different languages

**Service 1: User Service (Python/Flask)**
```python
# app.py
from flask import Flask, jsonify, request
from models import User, db

app = Flask(__name__)

# Use Copilot to generate CRUD endpoints
@app.route('/users', methods=['GET'])
def get_users():
    # Copilot suggests implementation
```

**Service 2: Order Service (Node.js/Express)**
```javascript
// app.js
const express = require('express');
const app = express();

// Use Copilot to generate order management
app.get('/orders', async (req, res) => {
    // Copilot suggests implementation
});
```

**Service 3: Gateway (Go)**
```go
// main.go
package main

import "net/http"

// Use Copilot to generate API gateway
func main() {
    // Copilot suggests routing logic
}
```

**Database (PostgreSQL)**
```sql
-- schema.sql
-- Use Copilot to generate schema
CREATE TABLE users (
    -- Copilot completes
);
```

---

## Lab: Polyglot Development Project

### Objective
Build a complete application using multiple programming languages with Copilot.

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

**Part 1: Backend (Python)**

*Prompt:* "Create a Flask API for task management with user authentication"

```python
# app.py - Main Flask application
# Prompt: "Create Flask app with SQLAlchemy for task management"
from flask import Flask, jsonify, request
from flask_sqlalchemy import SQLAlchemy
from flask_jwt_extended import JWTManager

app = Flask(__name__)
# Copilot suggests configuration and setup

# models.py - Database models
# Prompt: "Create SQLAlchemy models for User and Task with relationships"
class User(db.Model):
    # Copilot suggests proper field definitions
    pass

class Task(db.Model):
    # Copilot suggests relationship to User
    pass

# auth.py - Authentication logic
# Prompt: "Implement JWT authentication with password hashing using bcrypt"
def register_user(username, email, password):
    # Copilot suggests hashing and database storage
    pass

# routes.py - API endpoints
# Prompt: "Create REST API endpoints for CRUD operations on tasks"
@app.route('/api/tasks', methods=['GET'])
def get_tasks():
    # Copilot suggests query and JSON response
    pass
```

**Part 2: Frontend (JavaScript)**

*Prompt:* "Create a single-page application for task management"

```javascript
// index.html - Main page
// Prompt: "Create responsive HTML page with login form and task list"
<div id="app">
    <!-- Copilot suggests structure -->
</div>

// style.css - Styling
// Prompt: "Add modern CSS styling with flexbox for task management app"
:root {
    /* Copilot suggests color scheme */
}

// app.js - Frontend logic
// Prompt: "Create JavaScript app with form handlers and state management"
class TaskApp {
    constructor() {
        // Copilot suggests initialization
    }
    
    async addTask(title) {
        // Copilot suggests API integration
    }
}

// api.js - API client
// Prompt: "Create API client class with methods for all CRUD operations"
class APIClient {
    async getTasks() {
        // Copilot suggests fetch implementation
    }
}
```

**Part 3: Database (SQL)**

*Prompt:* "Create database schema for task management system"

```sql
-- schema.sql - Database schema
-- Prompt: "Create normalized database schema with users and tasks tables"
CREATE TABLE users (
    -- Copilot suggests proper fields and constraints
);

CREATE TABLE tasks (
    -- Copilot suggests relationship to users table
);

-- seed.sql - Sample data
-- Prompt: "Generate sample data for testing"
INSERT INTO users (...) VALUES (...);
INSERT INTO tasks (...) VALUES (...);
```

**Part 4: Documentation**

Use Ask Mode (Chat Panel) for these questions:
- "How should I structure a multi-language full-stack application?"
- "What are best practices for API endpoint documentation?"
- "How do I set up a development environment for this stack?"

Create files:
- `README.md` - Setup and usage instructions
- `API.md` - API endpoint documentation
- `ARCHITECTURE.md` - System architecture explanation

### Deliverables
- Complete working application
- All files properly organized
- README.md with setup instructions
- REFLECTION.md on multi-language development

---

## Additional Resources

### Documentation
- [GitHub Copilot Language Support](https://docs.github.com/en/copilot/getting-started-with-github-copilot)
- [Multi-Language Projects](https://docs.github.com/en/copilot/using-github-copilot/getting-started-with-github-copilot)

### Community
- [Copilot Discussions](https://github.com/orgs/community/discussions/categories/copilot)

---

## Knowledge Check

### Quick Quiz

1. Name 5 programming languages Copilot supports
2. What's the difference between Ask Mode and Inline Completion?
3. Which mode is best for learning new concepts?
4. How does Copilot adapt to different languages?
5. When should you use Agent Mode?

### Answers
1. Python, JavaScript, TypeScript, Java, Go (and many others)
2. Ask Mode provides explanations and guidance; Inline Completion generates code
3. Chat Panel mode
4. By understanding language-specific syntax, idioms, and patterns
5. For complex, multi-step tasks requiring multiple files

---

## Summary

In this unit, you learned:
- ✅ How to use Copilot across multiple programming languages
- ✅ Language-specific features and adaptations
- ✅ How to use Ask Mode effectively
- ✅ Different interaction modes and when to use them
- ✅ How to switch between modes for optimal workflow
- ✅ Cross-language development techniques

**Next:** [Module 3 - Copilot As Assistant / Conversational Development Workflows](../module3-copilot-assistant/README.md)

---

## Module 2 Complete! 🎉

You've mastered Copilot's foundational features:
- ✅ Inline code assistance
- ✅ Code actions (Explain, Fix, Move, Rewrite)
- ✅ Multi-language support
- ✅ Different interaction modes

Ready for advanced features? Let's move to **Module 3**!
