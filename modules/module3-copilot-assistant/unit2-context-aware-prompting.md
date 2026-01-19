# Unit 2: Context-Aware Prompting

## Learning Objectives
After completing this unit, you will be able to:
- Understand the role of context in prompt design
- Identify and leverage different types of context
- Compare context-aware vs basic prompting approaches
- Apply zero-shot, one-shot, and few-shot learning techniques
- Write highly effective prompts that yield better results
- Use context to improve AI suggestions dramatically

---

## 1. Understanding Context in Prompt Design

### What is Context?

Context is the surrounding information that helps AI understand your intent and generate more accurate, relevant responses.

```
Without Context:
┌─────────────────┐
│ "Create button" │  → Generic button
└─────────────────┘

With Context:
┌─────────────────────────────────────┐
│ "Create a primary action button     │
│  for submitting forms in our React  │
│  app, styled with Tailwind CSS,     │
│  matching our design system"        │  → Specific, styled button
└─────────────────────────────────────┘
```

### Why Context Matters

**Example 1: Ambiguous Request**

**Without Context:**
```
You: "Create a function to process data"

Copilot: [Generates generic function]
def process_data(data):
    return data
```

**With Context:**
```
You: "Create a function to process user registration data:
     - Validate email format
     - Hash password with bcrypt
     - Check for existing users in PostgreSQL
     - Return user object or error message"

Copilot: [Generates specific, complete function]
def process_user_registration(email, password, db_session):
    # Email validation
    email_pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    if not re.match(email_pattern, email):
        return {'error': 'Invalid email format'}
    
    # Check existing user
    existing_user = db_session.query(User).filter_by(email=email).first()
    if existing_user:
        return {'error': 'User already exists'}
    
    # Hash password
    password_hash = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())
    
    # Create user
    user = User(email=email, password_hash=password_hash)
    db_session.add(user)
    db_session.commit()
    
    return {'user': user.to_dict()}
```

### The Context Pyramid

```
        ┌─────────────────┐
       /  Your Specific   /
      /   Requirements   /  (Most Important)
     /─────────────────/
    /   Code Style &   /
   /   Conventions    /
  /─────────────────/
 /  Libraries &     /
/   Tech Stack     /
/─────────────────/
    Project
   Structure
 & File Context
─────────────────
```

### Context Levels

#### **Level 1: No Context (Weak)**
```
"Write a function"
```

#### **Level 2: Basic Context (Better)**
```
"Write a function to validate passwords"
```

#### **Level 3: Detailed Context (Good)**
```
"Write a Python function to validate passwords:
 - Minimum 8 characters
 - At least one uppercase letter
 - At least one number"
```

#### **Level 4: Complete Context (Best)**
```
"""
Write a Python function to validate passwords for our web application.

Requirements:
- Minimum 8 characters, maximum 128
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- At least one special character (!@#$%^&*)
- No common passwords (check against list)

Return:
- True if valid
- Dict with error messages if invalid

Use type hints and add comprehensive docstring.
Follow PEP 8 style guide.
"""
```

---

## 2. Types of Context Used in Prompts

### Type 1: Technical Context

Information about the technology stack, languages, and tools.

**Example:**
```
❌ Without Technical Context:
"Create an API endpoint"

✅ With Technical Context:
"Create a REST API endpoint using:
 - Framework: Express.js (Node.js)
 - Database: MongoDB with Mongoose
 - Authentication: JWT tokens
 - Validation: Joi schema validation
 - Error handling: Async/await with try-catch"
```

### Type 2: Business Logic Context

Information about business rules and requirements.

**Example:**
```
❌ Without Business Logic:
"Calculate discount"

✅ With Business Logic:
"Calculate discount for e-commerce cart:
 - 10% off for orders over $100
 - 20% off for orders over $500
 - Additional 5% for loyalty members
 - Max discount: $100
 - Discount doesn't apply to sale items
 - Free shipping over $50"
```

### Type 3: Data Structure Context

Information about data formats and structures.

**Example:**
```
❌ Without Data Structure:
"Parse the data"

✅ With Data Structure:
"Parse user data from API response:

Input format:
{
  'users': [
    {'id': 1, 'name': 'John', 'email': 'john@example.com', 'age': 30},
    {'id': 2, 'name': 'Jane', 'email': 'jane@example.com', 'age': 25}
  ],
  'total': 2,
  'page': 1
}

Output format:
[
  {'userId': 1, 'fullName': 'John', 'contactEmail': 'john@example.com'},
  {'userId': 2, 'fullName': 'Jane', 'contactEmail': 'jane@example.com'}
]"
```

### Type 4: Code Style Context

Information about coding standards and conventions.

**Example:**
```
❌ Without Style Context:
"Create a class"

✅ With Style Context:
"Create a Python class following our conventions:
 - Use dataclasses for simple data containers
 - Type hints for all parameters and returns
 - Google-style docstrings
 - Private methods start with underscore
 - Property decorators for getters/setters
 - Comprehensive error handling with custom exceptions"
```

### Type 5: Performance Context

Information about performance requirements.

**Example:**
```
❌ Without Performance Context:
"Search the list"

✅ With Performance Context:
"Implement search for list of 1 million+ records:
 - Target: <100ms response time
 - Use binary search (list is sorted by ID)
 - Implement caching for repeated searches
 - Index commonly searched fields
 - Paginate results (50 per page)
 - Memory efficient (don't load all records)"
```

### Type 6: Security Context

Information about security requirements.

**Example:**
```
❌ Without Security Context:
"Create login function"

✅ With Security Context:
"Create secure login function:
 - Hash passwords with bcrypt (12 rounds)
 - Implement rate limiting (5 attempts per 15 min)
 - Use constant-time comparison for passwords
 - Generate secure session tokens (32 bytes)
 - Set HTTP-only cookies
 - Log failed attempts with IP address
 - Implement account lockout after 5 failures
 - Validate input to prevent SQL injection"
```

### Type 7: Environment Context

Information about the execution environment.

**Example:**
```
❌ Without Environment Context:
"Connect to database"

✅ With Environment Context:
"Connect to PostgreSQL database:
 - Development: localhost:5432
 - Production: Use environment variables
 - Connection pooling: min 5, max 20
 - Timeout: 30 seconds
 - SSL required in production
 - Auto-reconnect on connection loss
 - Log queries in development only"
```

### Type 8: User Experience Context

Information about UX requirements.

**Example:**
```
❌ Without UX Context:
"Create a form"

✅ With UX Context:
"Create a user registration form:
 - Real-time validation as user types
 - Show green checkmark for valid fields
 - Inline error messages (red text below field)
 - Password strength indicator
 - Disable submit until all fields valid
 - Show loading spinner on submit
 - Success message after registration
 - Accessible (ARIA labels, keyboard navigation)
 - Mobile responsive (touch-friendly)"
```

---

## 3. Context-Aware Prompting vs Basic Prompting

### Direct Comparison

#### Example 1: Create a Function

**Basic Prompting:**
```python
# Create a function to sort items
```

**Result:**
```python
def sort_items(items):
    return sorted(items)
```

**Context-Aware Prompting:**
```python
# Create a function to sort product items for e-commerce display
# Input: List of product dicts with keys: name, price, rating, stock
# Sort by: 1) In stock items first, 2) By rating (high to low), 3) By price
# Return: Sorted list maintaining original dict structure
```

**Result:**
```python
def sort_products_for_display(products):
    """
    Sort products for optimal e-commerce display.
    
    Sorting priority:
    1. In-stock items before out-of-stock
    2. Higher rated items first
    3. Lower priced items first (within same rating)
    
    Args:
        products: List of dicts with keys: name, price, rating, stock
    
    Returns:
        Sorted list of product dictionaries
    """
    return sorted(
        products,
        key=lambda x: (
            x['stock'] == 0,  # In stock first (False < True)
            -x['rating'],      # Higher rating first
            x['price']         # Lower price first
        )
    )
```

#### Example 2: API Endpoint

**Basic Prompting:**
```javascript
// Create API endpoint to get users
```

**Result:**
```javascript
app.get('/users', (req, res) => {
  res.json(users);
});
```

**Context-Aware Prompting:**
```javascript
// Create Express.js API endpoint to get users with:
// - Pagination (page, limit query params, default 10 per page)
// - Filtering by status (query param: status=active/inactive)
// - Search by name (query param: search)
// - Authentication required (JWT middleware)
// - Error handling for database errors
// - Return format: {users: [...], total: N, page: N, totalPages: N}
```

**Result:**
```javascript
const authMiddleware = require('./middleware/auth');
const User = require('./models/User');

app.get('/users', authMiddleware, async (req, res) => {
  try {
    const page = parseInt(req.query.page) || 1;
    const limit = parseInt(req.query.limit) || 10;
    const status = req.query.status;
    const search = req.query.search;
    
    // Build query
    let query = {};
    
    if (status) {
      query.status = status;
    }
    
    if (search) {
      query.name = { $regex: search, $options: 'i' };
    }
    
    // Execute query with pagination
    const skip = (page - 1) * limit;
    const users = await User.find(query)
      .skip(skip)
      .limit(limit)
      .select('-password'); // Exclude password field
    
    const total = await User.countDocuments(query);
    const totalPages = Math.ceil(total / limit);
    
    res.json({
      users,
      total,
      page,
      totalPages
    });
  } catch (error) {
    console.error('Error fetching users:', error);
    res.status(500).json({ error: 'Failed to fetch users' });
  }
});
```

### Context Checklist

Before writing a prompt, ask:

- [ ] What language/framework am I using?
- [ ] What are the input and output formats?
- [ ] What are the business rules?
- [ ] Are there performance requirements?
- [ ] What security measures are needed?
- [ ] What error cases should be handled?
- [ ] What coding style should be followed?
- [ ] Are there existing patterns to follow?

---

## 4. Context-Aware Prompting with Zero-Shot, One-Shot, and Few-Shot Learning

### Understanding Shot Learning

**"Shot"** refers to the number of examples provided to the AI.

```
Zero-Shot:  No examples (description only)
One-Shot:   One example
Few-Shot:   Multiple examples (typically 2-5)
```

### Zero-Shot Learning

Provide clear description without examples.

**When to use:**
- Standard, well-known tasks
- Clear, unambiguous requirements
- Common patterns

**Example:**
```python
# Zero-shot: Create a function to validate email addresses
# Requirements:
# - Accept string as input
# - Return boolean (True if valid, False otherwise)
# - Use regex pattern for validation
# - Check for @ symbol and domain
```

**Copilot generates:**
```python
import re

def validate_email(email):
    """Validate email address format."""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))
```

### One-Shot Learning

Provide one example of desired output.

**When to use:**
- Custom formats
- Specific patterns
- Unique structure

**Example:**
```python
# Create validator functions following this pattern:
# Example:
def validate_username(username):
    """Validate username: 3-20 alphanumeric characters."""
    if not username or len(username) < 3 or len(username) > 20:
        return False, "Username must be 3-20 characters"
    if not username.isalnum():
        return False, "Username must be alphanumeric"
    return True, "Valid username"

# Now create similar validator for:
# Password: 8-128 characters, one uppercase, one lowercase, one number
```

**Copilot generates (following the pattern):**
```python
def validate_password(password):
    """Validate password: 8-128 chars, uppercase, lowercase, number."""
    if not password or len(password) < 8 or len(password) > 128:
        return False, "Password must be 8-128 characters"
    if not any(c.isupper() for c in password):
        return False, "Password must contain uppercase letter"
    if not any(c.islower() for c in password):
        return False, "Password must contain lowercase letter"
    if not any(c.isdigit() for c in password):
        return False, "Password must contain a number"
    return True, "Valid password"
```

### Few-Shot Learning

Provide multiple examples to establish pattern.

**When to use:**
- Complex patterns
- Subtle variations
- Domain-specific formats
- Consistent structure needed

**Example:**
```python
# Create API response formatters following these patterns:

# Example 1: Success with data
def format_user_response(user):
    return {
        'status': 'success',
        'data': user.to_dict(),
        'message': 'User retrieved successfully'
    }

# Example 2: Success with list
def format_users_list_response(users, total):
    return {
        'status': 'success',
        'data': {
            'users': [u.to_dict() for u in users],
            'total': total
        },
        'message': f'Retrieved {len(users)} users'
    }

# Example 3: Error response
def format_error_response(error_message, error_code=400):
    return {
        'status': 'error',
        'data': None,
        'message': error_message,
        'code': error_code
    }

# Now create similar formatters for:
# 1. Product response (single product)
# 2. Products list response (with pagination info)
# 3. Not found response
```

**Copilot generates (following established patterns):**
```python
def format_product_response(product):
    return {
        'status': 'success',
        'data': product.to_dict(),
        'message': 'Product retrieved successfully'
    }

def format_products_list_response(products, total, page, per_page):
    return {
        'status': 'success',
        'data': {
            'products': [p.to_dict() for p in products],
            'total': total,
            'page': page,
            'per_page': per_page,
            'total_pages': (total + per_page - 1) // per_page
        },
        'message': f'Retrieved {len(products)} products'
    }

def format_not_found_response(resource_type, resource_id):
    return {
        'status': 'error',
        'data': None,
        'message': f'{resource_type} with ID {resource_id} not found',
        'code': 404
    }
```

### Comparison Table

| Approach | Examples | Best For | Accuracy |
|----------|----------|----------|----------|
| **Zero-Shot** | 0 | Standard tasks, clear requirements | Good |
| **One-Shot** | 1 | Custom formats, specific patterns | Better |
| **Few-Shot** | 2-5 | Complex patterns, consistency | Best |

### Advanced Few-Shot Pattern

**Domain-Specific Transformation:**

```python
# Data transformation patterns for our analytics system:

# Pattern 1: User event
raw_user_event = {
    'evt': 'login',
    'uid': '12345',
    'ts': '2024-01-15T10:30:00Z',
    'ip': '192.168.1.1'
}

transformed_user_event = {
    'event_type': 'user_login',
    'user_id': '12345',
    'timestamp': datetime.fromisoformat('2024-01-15T10:30:00'),
    'metadata': {'ip_address': '192.168.1.1'},
    'category': 'authentication'
}

# Pattern 2: Purchase event
raw_purchase_event = {
    'evt': 'purchase',
    'uid': '12345',
    'amt': '99.99',
    'cur': 'USD',
    'items': ['item1', 'item2']
}

transformed_purchase_event = {
    'event_type': 'user_purchase',
    'user_id': '12345',
    'timestamp': datetime.now(),
    'metadata': {
        'amount': Decimal('99.99'),
        'currency': 'USD',
        'item_ids': ['item1', 'item2'],
        'item_count': 2
    },
    'category': 'transaction'
}

# Pattern 3: Error event
raw_error_event = {
    'evt': 'error',
    'msg': 'Payment failed',
    'code': 'E001',
    'uid': '12345'
}

transformed_error_event = {
    'event_type': 'system_error',
    'user_id': '12345',
    'timestamp': datetime.now(),
    'metadata': {
        'error_message': 'Payment failed',
        'error_code': 'E001',
        'severity': 'high'
    },
    'category': 'error'
}

# Now create transformer for:
# Signup event: {'evt': 'signup', 'uid': '67890', 'email': 'user@example.com', 'ref': 'organic'}
```

---

## Hands-On Exercises

### Exercise 1: Context Levels

Rewrite this prompt with increasing context:

**Basic:**
```
"Create a sorting function"
```

**Your Turn - Add Context Progressively:**
1. Add technical context (language, algorithm)
2. Add data structure context (input/output format)
3. Add performance context (size, speed requirements)
4. Add business logic context (sorting rules)

### Exercise 2: Zero-Shot vs Few-Shot

**Task:** Create data validators

**Zero-Shot Approach:**
```python
# Create a function to validate phone numbers
# Support: US format (XXX) XXX-XXXX or XXX-XXX-XXXX
```

**Few-Shot Approach:**
```python
# Create validators following these patterns:

def validate_email(email):
    """Validate email format."""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    if not re.match(pattern, email):
        return False, "Invalid email format"
    return True, email

def validate_zip_code(zip_code):
    """Validate US zip code (5 digits or 5+4 format)."""
    pattern = r'^\d{5}(-\d{4})?$'
    if not re.match(pattern, zip_code):
        return False, "Invalid zip code format"
    return True, zip_code

# Now create validator for phone numbers: (XXX) XXX-XXXX or XXX-XXX-XXXX
```

Try both approaches and compare results.

### Exercise 3: Complete Context

Write a fully contextualized prompt for:

**Task:** "Create a user registration endpoint"

Include:
- Technical stack
- Validation rules
- Security requirements
- Error handling
- Response format
- Database operations

### Exercise 4: Pattern Replication

Given these examples:

```python
# Example 1
def calculate_order_total(items, tax_rate):
    subtotal = sum(item['price'] * item['quantity'] for item in items)
    tax = subtotal * tax_rate
    return {'subtotal': subtotal, 'tax': tax, 'total': subtotal + tax}

# Example 2
def calculate_shipping_cost(weight, distance, priority):
    base_cost = weight * 0.5
    distance_cost = distance * 0.1
    priority_multiplier = 2.0 if priority else 1.0
    return {
        'base_cost': base_cost,
        'distance_cost': distance_cost,
        'total': (base_cost + distance_cost) * priority_multiplier
    }
```

Create a similar function for:
- `calculate_discount(items, loyalty_level, coupon_code)`

---

## Real-World Scenario

### Scenario: Building a Feature with Context-Aware Prompting

**Task:** Implement password reset functionality

**Approach 1: Basic Prompting (Poor Results)**
```
"Create password reset function"
```

**Approach 2: Context-Aware Prompting (Excellent Results)**

```python
"""
Create a secure password reset system for our Flask application.

Technical Stack:
- Framework: Flask with SQLAlchemy
- Database: PostgreSQL
- Email: SendGrid API
- Token: itsdangerous.URLSafeTimedSerializer

Requirements:
1. Generate secure reset token (expires in 1 hour)
2. Send email with reset link
3. Validate token on reset page
4. Update password with bcrypt hashing
5. Invalidate old sessions
6. Log password change with IP address

Security:
- Rate limit: 3 requests per hour per email
- Constant-time token comparison
- Expire token after use
- Check password against common passwords list

Error Handling:
- Invalid email: Return success (security - don't reveal if email exists)
- Expired token: Clear error message with resend option
- Database errors: Log and show generic error

Response Format:
Success: {'status': 'success', 'message': 'Reset email sent'}
Error: {'status': 'error', 'message': 'error description'}

Example flow:
1. POST /api/password-reset/request {'email': 'user@example.com'}
2. User receives email with token
3. POST /api/password-reset/confirm {'token': 'xxx', 'new_password': 'yyy'}
4. Password updated, user can login
"""
```

The context-aware version provides:
- Complete, secure implementation
- Proper error handling
- Security best practices
- Clear structure
- Documentation

---

## Knowledge Check

### Quick Quiz

1. What is context in prompt engineering?
2. Name three types of context
3. What's the difference between zero-shot and few-shot learning?
4. When should you use one-shot learning?
5. Why does context improve AI responses?

### Answers
1. Surrounding information that helps AI understand intent
2. Technical, Business Logic, Data Structure, Code Style, Performance, Security, etc.
3. Zero-shot provides no examples; few-shot provides 2-5 examples
4. When you have a specific pattern or format to follow
5. Context reduces ambiguity and provides clear requirements

---

## Lab: Master Context-Aware Prompting

### Objective
Practice writing context-rich prompts for better AI assistance.

### Challenges

**Challenge 1: Basic → Context-Rich**
Transform these basic prompts:
1. "Create a function to search"
2. "Make an API endpoint"
3. "Add validation"

**Challenge 2: Zero, One, Few-Shot**
For each task, create:
- Zero-shot prompt
- One-shot prompt with example
- Few-shot prompt with 3 examples

Task: Create logging functions

**Challenge 3: Real Feature**
Write a complete context-aware prompt for:
- Shopping cart system
- Include: Add item, remove item, update quantity, calculate total, apply discounts

**Challenge 4: Pattern Library**
Create a few-shot pattern library for:
- Database models
- API endpoints
- Test cases
- Error handlers

### Deliverables
- Collection of prompts (basic vs context-aware)
- Comparison of AI outputs
- Pattern library (reusable examples)
- Reflection on quality improvements

---

## Summary

In this unit, you learned:
- ✅ The critical role of context in prompting
- ✅ Eight types of context to include
- ✅ Context-aware vs basic prompting comparison
- ✅ Zero-shot, one-shot, and few-shot learning
- ✅ How to write comprehensive, effective prompts
- ✅ Techniques for consistent, high-quality AI output

**Next:** Module 4 - Copilot Agent Mode

---

## Module 3 Complete! 🎉

You've mastered conversational development:
- ✅ Chat interface and slash commands
- ✅ Context anchors for precise conversations
- ✅ Model selection strategies
- ✅ Context-aware prompting techniques
- ✅ Advanced prompt engineering

**Ready for autonomous AI assistance? Let's explore Agent Mode!**
