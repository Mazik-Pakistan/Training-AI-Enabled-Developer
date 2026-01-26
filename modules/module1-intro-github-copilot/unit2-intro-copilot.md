# Unit 2: Introduction to GitHub Copilot

## Learning Objectives
After completing this unit, you will be able to:
- Explain what GitHub Copilot is and how it leverages AI
- Understand the technology behind Copilot (OpenAI Codex)
- Write effective prompts for better code suggestions
- Apply the 5 Responsible AI principles in development
- Recognize the capabilities and limitations of AI assistance

---

## 1. What GitHub Copilot Is and How It Works
<p align="center">
  <a href="https://www.youtube.com/watch?v=n0NlxUyA7FI">
    <img src="https://img.youtube.com/vi/n0NlxUyA7FI/maxresdefault.jpg" width="600" alt="Click to play video">
  </a><br>
  <em>▶ Click to play video</em>
</p>

### What is GitHub Copilot?
GitHub Copilot is an AI-powered code completion tool that acts as your "AI pair programmer." It suggests whole lines or entire functions as you type.

<img src="https://images.ctfassets.net/8aevphvgewt8/5IdZ8KizWhMOGixAmVSw0g/f81f5f263a88eabe5d3e102300d44a88/github-copilot-social-img.png">

**Key Features:**
- 💡 **Intelligent Code Completion**: Context-aware suggestions
- 💬 **Chat Interface**: Ask questions and get explanations
- 🔧 **Code Actions**: Fix, explain, and optimize code
- 🌍 **Multi-Language Support**: Works with dozens of languages
- 📝 **Comment-to-Code**: Generate code from natural language

### How GitHub Copilot Works

```
┌─────────────────────────────────────────┐
│  Your Code Editor (VS Code)             │
│                                         │
│  You type: # Calculate factorial        │
│                                         │
│  Copilot suggests:                      │
│  def factorial(n):                      │
│      if n == 0: return 1                │
│      return n * factorial(n-1)          │
└─────────────────────────────────────────┘
         │
         │ Sends context (code, comments)
         ▼
┌─────────────────────────────────────────┐
│  GitHub Copilot Service (Cloud)         │
│                                         │
│  Uses: OpenAI Codex Model               │
│  - Trained on billions of lines         │
│  - Understands programming patterns     │
│  - Generates contextual suggestions     │
└─────────────────────────────────────────┘
```

### The Technology Behind Copilot

**OpenAI Codex**
- Large language model trained on public code
- Understands natural language and code
- Generates code in multiple programming languages
- Continuously improved with user feedback

**How It Generates Suggestions:**
1. **Context Gathering**: Analyzes your current file, open files, and comments
2. **Pattern Recognition**: Identifies coding patterns and intent
3. **Code Generation**: Produces relevant suggestions
4. **Ranking**: Presents the most likely helpful suggestions first

### What Copilot Can Do

✅ **Code Generation**
- Write functions from comments
- Complete partially written code
- Generate boilerplate code

✅ **Code Understanding**
- Explain complex code
- Suggest improvements
- Identify potential bugs

✅ **Testing**
- Generate unit tests
- Create test cases
- Suggest edge cases

✅ **Documentation**
- Write docstrings
- Create README files
- Generate API documentation

### What Copilot Cannot Do

❌ **Replace Developers**
- Doesn't understand business requirements
- Can't make architectural decisions
- Requires human oversight and validation

❌ **Guarantee Correctness**
- Suggestions may contain bugs
- Code needs review and testing
- May not follow best practices

❌ **Replace Learning**
- Understanding fundamentals is crucial
- Critical thinking still required
- Knowledge of domain is essential

---

## 2. Effective Prompting for Better Development Experience

### The Art of Prompting

**Good prompts = Better suggestions**

Think of Copilot as a junior developer who needs clear instructions.

### Prompt Engineering Principles

#### 1. **Be Specific and Clear**

**❌ Poor Prompt:**
```python
# function
```

**✅ Good Prompt:**
```python
# Function to validate email address using regex
# Returns True if valid, False otherwise
```

#### 2. **Provide Context**

**❌ Poor Prompt:**
```python
# calculate
```

**✅ Good Prompt:**
```python
# Calculate the compound interest
# principal: initial amount
# rate: annual interest rate (as decimal)
# time: time period in years
# n: number of times interest is compounded per year
```

#### 3. **Use Examples (Few-Shot Learning)**

```python
# Convert temperature from Celsius to Fahrenheit
# Example: celsius_to_fahrenheit(0) returns 32.0
# Example: celsius_to_fahrenheit(100) returns 212.0
def celsius_to_fahrenheit(celsius):
```

#### 4. **Break Down Complex Tasks**

```python
# Step 1: Read CSV file
# Step 2: Parse data into list of dictionaries
# Step 3: Filter records where age > 18
# Step 4: Sort by name alphabetically
# Step 5: Write to new CSV file
```

#### 5. **Use Descriptive Variable Names**

**❌ Poor:**
```python
def calc(a, b, c):
```

**✅ Good:**
```python
def calculate_loan_payment(principal, annual_rate, years):
```

### Prompt Patterns

#### Pattern 1: Function with Documentation
```python
def search_products(query: str, category: str = None, max_results: int = 10) -> list:
    """
    Search for products in the database.
    
    Args:
        query: Search term
        category: Optional category filter
        max_results: Maximum number of results to return
    
    Returns:
        List of product dictionaries matching the search criteria
    """
```

#### Pattern 2: Comment-Driven Development
```python
# Create a REST API endpoint for user registration
# - Accept POST request with username, email, password
# - Validate email format
# - Hash password using bcrypt
# - Check if user already exists
# - Save to database
# - Return JWT token
```

#### Pattern 3: Test-Driven Prompting
```python
# Test case: empty list should return 0
# Test case: [1, 2, 3] should return 6
# Test case: [-1, -2, -3] should return -6
def sum_list(numbers):
```

---

## 3. Principles of Responsible AI

### The 5 Responsible AI Principles

<img src="https://blogs.microsoft.com/wp-content/uploads/prod/sites/5/2022/06/2_Core_Principles.jpg">

#### 1. **Fairness** ⚖️
**Principle**: AI systems should treat all people fairly.

**In Practice:**
- Review AI-generated code for biases
- Ensure algorithms don't discriminate
- Test with diverse datasets
- Be aware of underrepresented groups

**Example:**
```python
# ❌ Biased approach
def calculate_loan_approval(income, age, gender):
    if gender == 'male':
        return income > 50000
    else:
        return income > 60000  # Unfair!

# ✅ Fair approach
def calculate_loan_approval(income, credit_score, debt_to_income_ratio):
    return (income > 50000 and 
            credit_score > 700 and 
            debt_to_income_ratio < 0.4)
```

#### 2. **Reliability & Safety** 🛡️
**Principle**: AI systems should perform reliably and safely.

**In Practice:**
- Always test AI-generated code
- Add error handling
- Validate inputs
- Include edge case handling

**Example:**
```python
# AI might suggest:
def divide(a, b):
    return a / b

# You should add:
def divide(a, b):
    """Safely divide two numbers."""
    if b == 0:
        raise ValueError("Cannot divide by zero")
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise TypeError("Arguments must be numbers")
    return a / b
```

#### 3. **Privacy & Security** 🔒
**Principle**: AI systems should be secure and respect privacy.

**In Practice:**
- Don't share sensitive data in prompts
- Review generated code for security issues
- Avoid hardcoding credentials
- Use secure coding practices

**Example:**
```python
# ❌ Don't do this:
# Connect to database at postgres://admin:password123@prod.db.com

# ✅ Do this:
# Connect to database using environment variables
import os
db_url = os.getenv('DATABASE_URL')
```

#### 4. **Inclusiveness** 🌍
**Principle**: AI systems should empower everyone and engage people.

**In Practice:**
- Write accessible code
- Use inclusive language in comments
- Consider internationalization
- Make UIs accessible

**Example:**
```python
# ✅ Inclusive approach
def format_user_greeting(user_name: str, locale: str = 'en') -> str:
    """
    Generate a personalized greeting for any user.
    Supports multiple languages and accessibility features.
    
    Args:
        user_name: The user's preferred display name
        locale: Language/region code (e.g., 'en', 'es', 'fr')
    
    Returns:
        Localized greeting string
    """
    greetings = {
        'en': f'Hello, {user_name}!',
        'es': f'¡Hola, {user_name}!',
        'fr': f'Bonjour, {user_name}!',
        'ar': f'!{user_name} مرحبا',
    }
    return greetings.get(locale, greetings['en'])
```

#### 5. **Transparency** 📊
**Principle**: AI systems should be understandable.

**In Practice:**
- Document AI-generated code
- Explain complex algorithms
- Add comments for clarity
- Document decisions and assumptions

**Example:**
```python
def calculate_credit_score(payment_history, credit_utilization, age_of_credit):
    """
    Calculate credit score using standard industry formula.
    
    Formula based on:
    - Payment history: 35% weight
    - Credit utilization: 30% weight
    - Age of credit: 15% weight
    
    This is a simplified model. Real credit scores use more factors.
    
    Returns:
        Credit score (300-850 range)
    """
    # Weights based on industry standards
    score = (payment_history * 0.35 + 
             credit_utilization * 0.30 + 
             age_of_credit * 0.15) * 850
    
    return max(300, min(850, score))  # Clamp to valid range
```

### Best Practices for Responsible AI Use

**DO:**
- ✅ Review and understand all AI-generated code
- ✅ Test thoroughly before deploying
- ✅ Add your own comments and documentation
- ✅ Consider ethical implications
- ✅ Validate security and privacy aspects

**DON'T:**
- ❌ Blindly accept suggestions
- ❌ Share proprietary code in prompts
- ❌ Assume AI output is always correct
- ❌ Skip code reviews
- ❌ Ignore licensing concerns

---

## Hands-On Exercises

### Exercise 1: First Copilot Suggestion
1. Open VS Code with GitHub Copilot installed
2. Create a new Python file: `calculator.py`
3. Type this comment:
   ```python
   # Function to add two numbers
   ```
4. Press Enter and wait for Copilot suggestion
5. Accept the suggestion with Tab
6. Compare with your expected implementation

### Exercise 2: Improve Your Prompts
Try different prompts and observe the quality of suggestions:

**Version 1:**
```python
# sort function
```

**Version 2:**
```python
# Function to sort a list of numbers
```

**Version 3:**
```python
# Function to sort a list of numbers in ascending order
# Uses bubble sort algorithm
# Parameters: numbers (list of integers)
# Returns: sorted list
```

### Exercise 3: Context-Aware Suggestions
1. Create a file `user_validation.py`
2. Add this code:
   ```python
   import re
   
   def validate_email(email):
       # Check if email format is valid
   ```
3. Let Copilot suggest the implementation
4. Observe how it uses the `re` import

---

## Code Examples

### Example 1: Basic Code Generation

**Input (Comment):**
```python
# Function to check if a string is a palindrome
# Should ignore case and spaces
```

**Copilot Suggestion:**
```python
def is_palindrome(s):
    # Remove spaces and convert to lowercase
    s = s.replace(" ", "").lower()
    # Check if string equals its reverse
    return s == s[::-1]
```

### Example 2: Function with Tests

**Input:**
```python
# Function to calculate fibonacci number at position n
# Use memoization for efficiency
def fibonacci(n, memo={}):
```

**Copilot Suggestion:**
```python
def fibonacci(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo)
    return memo[n]

# Test cases
assert fibonacci(0) == 0
assert fibonacci(1) == 1
assert fibonacci(10) == 55
```

### Example 3: API Endpoint

**Input:**
```python
# Flask route to get user by ID
# Returns JSON with user data
# Returns 404 if user not found
```

**Copilot Suggestion:**
```python
@app.route('/api/users/<int:user_id>', methods=['GET'])
def get_user(user_id):
    user = User.query.get(user_id)
    if user is None:
        return jsonify({'error': 'User not found'}), 404
    return jsonify({
        'id': user.id,
        'name': user.name,
        'email': user.email
    })
```

---

## Real-World Scenario

### Scenario: Building a User Registration System

**Task**: Create a secure user registration function

**Step 1: Write Intent**
```python
# Create user registration function that:
# - Validates email format
# - Checks password strength (min 8 chars, 1 uppercase, 1 number)
# - Hashes password securely
# - Checks if user already exists
# - Saves to database
# - Returns success or error message
```

**Step 2: Copilot Generates**
```python
import re
import hashlib
from database import db, User

def register_user(email, password, username):
    # Validate email format
    email_pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    if not re.match(email_pattern, email):
        return {'success': False, 'error': 'Invalid email format'}
    
    # Check password strength
    if len(password) < 8:
        return {'success': False, 'error': 'Password must be at least 8 characters'}
    if not re.search(r'[A-Z]', password):
        return {'success': False, 'error': 'Password must contain uppercase letter'}
    if not re.search(r'\d', password):
        return {'success': False, 'error': 'Password must contain a number'}
    
    # Check if user exists
    existing_user = User.query.filter_by(email=email).first()
    if existing_user:
        return {'success': False, 'error': 'User already exists'}
    
    # Hash password
    password_hash = hashlib.sha256(password.encode()).hexdigest()
    
    # Create user
    new_user = User(email=email, username=username, password_hash=password_hash)
    db.session.add(new_user)
    db.session.commit()
    
    return {'success': True, 'message': 'User registered successfully'}
```

**Step 3: Review for Responsible AI**
- ✅ Security: Password hashing
- ✅ Privacy: Not logging sensitive data
- ⚠️ Improvement needed: Use bcrypt instead of SHA256
- ⚠️ Add rate limiting to prevent abuse

---

## Lab: Build a Feature with Copilot

### Objective
Create a complete feature using GitHub Copilot while applying responsible AI principles.

### Instructions

**Part 1: Setup**
1. Create a new file: `task_manager.py`
2. Enable GitHub Copilot
3. Prepare to document your process

**Part 2: Feature Development**
Use Copilot to create a task management system with these features:
```python
# Task Manager Application
# Features:
# 1. Add task with title, description, priority (high/medium/low)
# 2. List all tasks
# 3. Mark task as complete
# 4. Delete task
# 5. Filter tasks by priority
# 6. Search tasks by keyword
```

**Part 3: Apply Responsible AI**
For each generated function:
1. Review for fairness (no biases)
2. Add error handling (reliability)
3. Check security (input validation)
4. Add documentation (transparency)
5. Test with diverse inputs (inclusiveness)

**Part 4: Testing**
Use Copilot to generate unit tests:
```python
# Generate comprehensive unit tests for task manager
# Include edge cases and error scenarios
```

**Part 5: Documentation**
Use Copilot to generate:
1. Docstrings for all functions
2. README.md with usage examples
3. Comments explaining complex logic

### Expected Outcome
- ✅ Working task manager application
- ✅ Comprehensive test suite
- ✅ Well-documented code
- ✅ Responsible AI principles applied
- ✅ Understanding of Copilot's capabilities and limitations

### Deliverables
- `task_manager.py` - Main application
- `test_task_manager.py` - Unit tests
- `README.md` - Documentation
- `REFLECTION.md` - Your experience using Copilot

---

## Additional Resources

### Documentation
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Copilot Getting Started](https://docs.github.com/en/copilot/getting-started-with-github-copilot)
- [Microsoft Responsible AI Principles](https://www.microsoft.com/en-us/ai/responsible-ai)

### Interactive Learning
- [Microsoft Learn: Introduction to GitHub Copilot](https://learn.microsoft.com/en-us/training/modules/introduction-to-github-copilot/)

### Videos
- [GitHub Copilot: Your AI Pair Programmer](https://www.youtube.com/watch?v=yCUVJUjKcYU)
- [Responsible AI in Practice](https://www.youtube.com/watch?v=dnC8-uUZXSc)

---

## Summary

In this unit, you learned:
- ✅ What GitHub Copilot is and how it works using OpenAI Codex
- ✅ How to write effective prompts for better suggestions
- ✅ The 5 Responsible AI principles and how to apply them
- ✅ Best practices for using AI assistance safely and ethically
- ✅ Hands-on experience generating code with Copilot

**Next:** [Unit 3 - GitHub Copilot Primer & Environment Setup](unit3-setup.md)
