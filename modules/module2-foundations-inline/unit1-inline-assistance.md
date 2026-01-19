# Unit 1: Inline Code Assistance

## Learning Objectives
After completing this unit, you will be able to:
- Use AI code completion to write code faster
- Apply inline code actions (Explain, Fix, Move, Rewrite)
- Understand when and how to accept or reject suggestions
- Optimize your workflow with Copilot's inline features
- Handle multiple suggestion alternatives

---

## 1. AI Code Completion in GitHub Copilot

### What is AI Code Completion?

AI code completion is Copilot's ability to suggest code as you type. Unlike traditional autocomplete that only suggests keywords, Copilot predicts entire lines, blocks, or functions based on context.

### How It Works

```
Your Context          →    Copilot Analysis    →    Suggestions
━━━━━━━━━━━━━━━━━━━━     ━━━━━━━━━━━━━━━━━━━━     ━━━━━━━━━━━━━━━
• File content              • Pattern recognition     • Line completion
• Comments                  • Intent understanding    • Block completion
• Variable names            • Similar code patterns   • Function generation
• Import statements         • Best practices          • Multiple alternatives
• Cursor position           • Language syntax
```

### Types of Code Completion

#### **1. Single Line Completion**
Completes the current line you're writing.

**Example:**
```python
# You type:
numbers = [1, 2, 3, 4, 5]
sum_of_numbers = 

# Copilot suggests:
sum_of_numbers = sum(numbers)
```

#### **2. Multi-Line Completion**
Suggests multiple lines of code.

**Example:**
```python
# You type:
def validate_email(email):

# Copilot suggests:
def validate_email(email):
    import re
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None
```

#### **3. Function/Method Completion**
Generates entire functions based on name and context.

**Example:**
```python
# You type:
def calculate_compound_interest(principal, rate, time, n):
    """Calculate compound interest."""

# Copilot suggests:
def calculate_compound_interest(principal, rate, time, n):
    """Calculate compound interest."""
    amount = principal * (1 + rate / n) ** (n * time)
    interest = amount - principal
    return interest
```

#### **4. Class Completion**
Creates complete class structures.

**Example:**
```python
# You type:
class BankAccount:
    """A simple bank account class."""

# Copilot suggests:
class BankAccount:
    """A simple bank account class."""
    
    def __init__(self, account_number, balance=0):
        self.account_number = account_number
        self.balance = balance
    
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self.balance
```

### Accepting Suggestions

**Keyboard Shortcuts:**
- **Tab**: Accept entire suggestion
- **Ctrl+→** (or **Cmd+→**): Accept next word
- **Esc**: Reject suggestion
- **Alt+]**: See next alternative
- **Alt+[**: See previous alternative

### Working with Multiple Alternatives

Copilot often has multiple suggestions. Navigate through them to find the best one.

**Example:**
```python
# You type:
# Function to sort list of dictionaries by key

# Alternative 1:
def sort_by_key(data, key):
    return sorted(data, key=lambda x: x[key])

# Alternative 2 (press Alt+]):
def sort_by_key(data, key, reverse=False):
    return sorted(data, key=lambda x: x.get(key, ''), reverse=reverse)

# Alternative 3 (press Alt+] again):
def sort_by_key(data, key):
    """Sort list of dictionaries by specified key."""
    try:
        return sorted(data, key=lambda x: x[key])
    except KeyError:
        return data
```

### Best Practices for Code Completion

#### **DO:**
✅ **Write descriptive comments**
```python
# Calculate BMI (Body Mass Index) from weight in kg and height in meters
# Formula: weight / (height^2)
```

✅ **Use meaningful variable names**
```python
def calculate_total_price(item_price, quantity, tax_rate):
    # Copilot understands intent better
```

✅ **Provide examples in comments**
```python
# Convert Celsius to Fahrenheit
# Examples: 0°C = 32°F, 100°C = 212°F
```

✅ **Include type hints**
```python
def process_data(input_data: list[dict]) -> pd.DataFrame:
    # Type hints help Copilot understand data types
```

#### **DON'T:**
❌ **Use vague names**
```python
def calc(a, b):  # Copilot can't infer intent
```

❌ **Skip comments for complex logic**
```python
def f(x):  # What does this do?
    return x if x > 0 else -x
```

❌ **Blindly accept without review**
```python
# Always review for correctness and security
```

### Context Matters

Copilot uses various context sources:

**1. Current File**
```python
# If you have imports:
import pandas as pd
import numpy as np

# Copilot knows you're working with data
def load_data(filepath):
    # Suggests pandas-based solution
    return pd.read_csv(filepath)
```

**2. Open Files**
```python
# If you have utils.py open with custom functions
# Copilot may suggest using those functions
from utils import custom_validator

def process_user_input(data):
    # May suggest: return custom_validator(data)
```

**3. File Path and Name**
```python
# In file: authentication/login.py
# Copilot understands this is auth-related

def verify_credentials(username, password):
    # Suggests security-aware implementation
```

---

## 2. Inline Code Actions

Inline code actions are powerful tools to explain, fix, move, or rewrite code without leaving your editor.

### Accessing Inline Code Actions

**Method 1: Keyboard Shortcut**
- Select code
- Press `Ctrl+I` (Windows/Linux) or `Cmd+I` (Mac)
- Type your action

**Method 2: Context Menu**
- Right-click selected code
- Choose "Copilot" → Select action

**Method 3: Light Bulb Icon**
- Copilot shows suggestions automatically
- Click the light bulb icon
- Choose action

### Action 1: Explain

**Purpose**: Understand complex or unfamiliar code

**When to use:**
- Learning new codebase
- Understanding legacy code
- Reviewing pull requests
- Debugging

**Example:**

**Original Code:**
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

**You select code and ask: `/explain`**

**Copilot Response:**
```
This is an implementation of the Quicksort algorithm:

1. Base case: If array has 1 or fewer elements, return as-is
2. Choose middle element as pivot
3. Partition array into three parts:
   - left: elements less than pivot
   - middle: elements equal to pivot
   - right: elements greater than pivot
4. Recursively sort left and right partitions
5. Concatenate: sorted left + middle + sorted right

Time Complexity: O(n log n) average, O(n²) worst case
Space Complexity: O(n) due to list comprehensions
```

### Action 2: Fix

**Purpose**: Fix bugs, errors, or issues in code

**When to use:**
- Syntax errors
- Logic bugs
- Runtime errors
- Security vulnerabilities

**Example 1: Syntax Error**

**Original Code:**
```python
def calculate_average(numbers)
    total = sum(numbers)
    return total / len(numbers)
```

**You select code and type: `/fix`**

**Copilot Fixes:**
```python
def calculate_average(numbers):  # Added missing colon
    total = sum(numbers)
    return total / len(numbers)
```

**Example 2: Logic Bug**

**Original Code:**
```python
def is_even(number):
    return number % 2 == 1  # Wrong logic!
```

**You select code and type: `/fix`**

**Copilot Fixes:**
```python
def is_even(number):
    return number % 2 == 0  # Corrected: even numbers have remainder 0
```

**Example 3: Security Issue**

**Original Code:**
```python
def execute_query(user_input):
    query = f"SELECT * FROM users WHERE name = '{user_input}'"
    return db.execute(query)
```

**You select code and type: `/fix SQL injection vulnerability`**

**Copilot Fixes:**
```python
def execute_query(user_input):
    # Fixed: Using parameterized query to prevent SQL injection
    query = "SELECT * FROM users WHERE name = ?"
    return db.execute(query, (user_input,))
```

### Action 3: Move

**Purpose**: Refactor code by moving it to appropriate locations

**When to use:**
- Extracting functions
- Organizing code structure
- Improving modularity
- Following separation of concerns

**Example:**

**Original Code (in main.py):**
```python
def process_order(order_data):
    # Validate email
    import re
    email = order_data['email']
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    if not re.match(pattern, email):
        raise ValueError("Invalid email")
    
    # Calculate total
    subtotal = order_data['price'] * order_data['quantity']
    tax = subtotal * 0.08
    total = subtotal + tax
    
    # Process payment
    # ... more code
```

**You select email validation and type: `/move to utils`**

**Copilot Creates (utils.py):**
```python
import re

def validate_email(email):
    """Validate email address format."""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None
```

**Copilot Updates (main.py):**
```python
from utils import validate_email

def process_order(order_data):
    # Validate email
    email = order_data['email']
    if not validate_email(email):
        raise ValueError("Invalid email")
    
    # Calculate total
    subtotal = order_data['price'] * order_data['quantity']
    tax = subtotal * 0.08
    total = subtotal + tax
    
    # Process payment
    # ... more code
```

### Action 4: Rewrite

**Purpose**: Improve code quality, readability, or performance

**When to use:**
- Modernizing old code
- Improving readability
- Optimizing performance
- Following best practices
- Changing paradigms

**Example 1: Improve Readability**

**Original Code:**
```python
def p(n):
    r = []
    for i in range(2, n):
        if all(i % j != 0 for j in range(2, int(i**0.5) + 1)):
            r.append(i)
    return r
```

**You select code and type: `/rewrite for better readability`**

**Copilot Rewrites:**
```python
def find_prime_numbers(max_number):
    """
    Find all prime numbers up to max_number.
    
    Args:
        max_number: The upper limit for finding primes
    
    Returns:
        List of prime numbers
    """
    prime_numbers = []
    
    for number in range(2, max_number):
        is_prime = True
        
        # Check if number is divisible by any number up to its square root
        for divisor in range(2, int(number ** 0.5) + 1):
            if number % divisor == 0:
                is_prime = False
                break
        
        if is_prime:
            prime_numbers.append(number)
    
    return prime_numbers
```

**Example 2: Optimize Performance**

**Original Code:**
```python
def find_duplicates(lst):
    duplicates = []
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j] and lst[i] not in duplicates:
                duplicates.append(lst[i])
    return duplicates
```

**You select code and type: `/rewrite for better performance`**

**Copilot Rewrites:**
```python
def find_duplicates(lst):
    """
    Find duplicate elements in a list efficiently.
    Time complexity: O(n) vs O(n²) in original
    """
    from collections import Counter
    
    counts = Counter(lst)
    return [item for item, count in counts.items() if count > 1]
```

**Example 3: Change Paradigm**

**Original Code (Imperative):**
```python
def get_even_squares(numbers):
    result = []
    for num in numbers:
        if num % 2 == 0:
            result.append(num ** 2)
    return result
```

**You select code and type: `/rewrite using functional programming`**

**Copilot Rewrites:**
```python
def get_even_squares(numbers):
    """Get squares of even numbers using functional approach."""
    return list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, numbers)))

# Or more readable functional style:
def get_even_squares(numbers):
    """Get squares of even numbers using list comprehension."""
    return [num ** 2 for num in numbers if num % 2 == 0]
```

---

## Hands-On Exercises

### Exercise 1: Code Completion Practice

Create a new file `exercises.py` and practice accepting suggestions:

```python
# Exercise 1a: Complete this function
def fibonacci(n):
    # Let Copilot suggest implementation

# Exercise 1b: Complete this class
class Stack:
    # Let Copilot suggest methods

# Exercise 1c: Complete this with list comprehension
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_squares = # Let Copilot suggest
```

### Exercise 2: Multiple Alternatives

For each prompt, cycle through at least 3 alternatives:

```python
# Function to check if a string is a valid password
# Requirements: 8+ chars, 1 uppercase, 1 lowercase, 1 number
def is_valid_password(password):
    # Press Alt+] to see alternatives
```

### Exercise 3: Explain Complex Code

Copy this code and use `/explain`:

```python
def decorator_with_args(prefix):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(f"{prefix}: Calling {func.__name__}")
            result = func(*args, **kwargs)
            print(f"{prefix}: Done")
            return result
        return wrapper
    return decorator

@decorator_with_args("LOG")
def greet(name):
    return f"Hello, {name}!"
```

### Exercise 4: Fix Bugs

Find and fix bugs in this code using `/fix`:

```python
def calculate_discount(price, discount_percent):
    discount_amount = price * discount_percent
    final_price = price - discount_amount
    return final_price

# Test:
print(calculate_discount(100, 20))  # Should return 80, but returns?
```

### Exercise 5: Refactor Code

Use `/rewrite` to improve this code:

```python
def process(data):
    r = []
    for d in data:
        if d['status'] == 'active':
            if d['age'] >= 18:
                if d['verified']:
                    r.append(d['name'])
    return r
```

---

## Code Examples

### Example 1: Smart Context-Aware Completion

```python
# File: data_analysis.py
import pandas as pd
import numpy as np

# You type:
def load_and_clean_data(filepath):
    # Read CSV file

# Copilot suggests (knows you're using pandas from imports):
def load_and_clean_data(filepath):
    # Read CSV file
    df = pd.read_csv(filepath)
    
    # Remove missing values
    df = df.dropna()
    
    # Remove duplicates
    df = df.drop_duplicates()
    
    # Reset index
    df = df.reset_index(drop=True)
    
    return df
```

### Example 2: Complete Test Suite

```python
# File: test_calculator.py
import unittest

class TestCalculator(unittest.TestCase):
    # You type:
    def test_addition(self):

# Copilot suggests:
class TestCalculator(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)
    
    def test_subtraction(self):
        self.assertEqual(subtract(5, 3), 2)
        self.assertEqual(subtract(0, 5), -5)
    
    def test_multiplication(self):
        self.assertEqual(multiply(2, 3), 6)
        self.assertEqual(multiply(-2, 3), -6)
    
    def test_division(self):
        self.assertEqual(divide(6, 2), 3)
        with self.assertRaises(ZeroDivisionError):
            divide(5, 0)
```

### Example 3: Before and After Rewrite

**Before:**
```python
def get_user_data(user_id):
    conn = psycopg2.connect("host=localhost dbname=mydb user=admin password=secret")
    cur = conn.cursor()
    cur.execute("SELECT * FROM users WHERE id = " + str(user_id))
    result = cur.fetchone()
    cur.close()
    conn.close()
    return result
```

**After (using `/rewrite for security and best practices`):**
```python
def get_user_data(user_id):
    """
    Fetch user data by ID safely.
    
    Improvements:
    - Uses environment variables for credentials
    - Parameterized queries prevent SQL injection
    - Context manager ensures proper resource cleanup
    - Type hints for better code clarity
    """
    import os
    import psycopg2
    from typing import Optional, Tuple
    
    db_config = {
        'host': os.getenv('DB_HOST', 'localhost'),
        'dbname': os.getenv('DB_NAME'),
        'user': os.getenv('DB_USER'),
        'password': os.getenv('DB_PASSWORD')
    }
    
    with psycopg2.connect(**db_config) as conn:
        with conn.cursor() as cur:
            # Parameterized query prevents SQL injection
            cur.execute(
                "SELECT * FROM users WHERE id = %s",
                (user_id,)
            )
            return cur.fetchone()
```

---

## Real-World Scenario

### Scenario: Refactoring Legacy Code

**Context**: You've inherited a legacy Python project with poor code quality.

**Task**: Use Copilot's inline actions to improve the code.

**Step 1: Understand the Code**

```python
# Original legacy code
def proc(d):
    r = []
    for x in d:
        if x['t'] == 'A' and x['v'] > 100:
            r.append(x)
    return r
```

**Action**: Select code → `/explain`

**Copilot explains**: "This function filters a list of dictionaries, returning only items where 't' key equals 'A' and 'v' key is greater than 100."

**Step 2: Improve Readability**

**Action**: Select code → `/rewrite for better readability and add documentation`

```python
def filter_active_high_value_items(data):
    """
    Filter items that are active and have high value.
    
    Args:
        data: List of dictionaries with 'type' and 'value' keys
    
    Returns:
        List of items where type is 'A' and value > 100
    """
    filtered_items = []
    for item in data:
        if item['type'] == 'A' and item['value'] > 100:
            filtered_items.append(item)
    return filtered_items
```

**Step 3: Modernize**

**Action**: Select code → `/rewrite using list comprehension`

```python
def filter_active_high_value_items(data):
    """
    Filter items that are active and have high value.
    
    Args:
        data: List of dictionaries with 'type' and 'value' keys
    
    Returns:
        List of items where type is 'A' and value > 100
    """
    return [
        item for item in data
        if item.get('type') == 'A' and item.get('value', 0) > 100
    ]
```

**Step 4: Add Error Handling**

**Action**: Select code → `/fix add error handling and type hints`

```python
from typing import List, Dict, Any

def filter_active_high_value_items(data: List[Dict[str, Any]]) -> List[Dict[str, Any]]:
    """
    Filter items that are active and have high value.
    
    Args:
        data: List of dictionaries with 'type' and 'value' keys
    
    Returns:
        List of items where type is 'A' and value > 100
    
    Raises:
        TypeError: If data is not a list
        ValueError: If data is empty
    """
    if not isinstance(data, list):
        raise TypeError("Data must be a list")
    
    if not data:
        raise ValueError("Data cannot be empty")
    
    return [
        item for item in data
        if isinstance(item, dict) and
        item.get('type') == 'A' and
        isinstance(item.get('value'), (int, float)) and
        item.get('value', 0) > 100
    ]
```

---

## Knowledge Check

### Quick Quiz

1. What are the four main inline code actions?
2. How do you accept only the next word of a suggestion?
3. What's the difference between Tab and Ctrl+→?
4. When should you use `/explain` vs `/fix`?
5. How can you view alternative suggestions?

### Answers
1. Explain, Fix, Move, Rewrite
2. Press `Ctrl+→` (or `Cmd+→` on Mac)
3. Tab accepts the entire suggestion; Ctrl+→ accepts only the next word
4. Use `/explain` to understand code; use `/fix` to correct errors or issues
5. Press `Alt+]` for next alternative, `Alt+[` for previous

---

## Lab: Code Refactoring Challenge

### Objective
Practice all inline code actions on a real-world code sample.

### Instructions

**Part 1: Setup**
Create a file `legacy_code.py` with this content:
```python
def calc(a, b, c):
    if c == 1:
        return a + b
    elif c == 2:
        return a - b
    elif c == 3:
        return a * b
    elif c == 4:
        return a / b

def proc_data(d):
    r = []
    for i in d:
        if i % 2 == 0:
            r.append(i * i)
    return r

def get_usr(id):
    q = "SELECT * FROM users WHERE id = " + str(id)
    return db.execute(q)
```

**Part 2: Explain**
1. Use `/explain` on each function
2. Document what each function does

**Part 3: Fix Issues**
1. Use `/fix` on `get_usr` to fix SQL injection
2. Use `/fix` on `calc` to handle division by zero

**Part 4: Rewrite for Quality**
1. Use `/rewrite` on `calc` for better readability
2. Use `/rewrite` on `proc_data` using list comprehension
3. Add type hints and docstrings to all functions

**Part 5: Move and Organize**
1. Create `math_operations.py`
2. Move `calc` function to it
3. Create `data_processing.py`
4. Move `proc_data` to it
5. Create `database.py`
6. Move `get_usr` to it

**Expected Outcome:**
- ✅ All functions explained and documented
- ✅ Security issues fixed
- ✅ Code improved for readability
- ✅ Proper file organization
- ✅ Type hints and error handling added

### Deliverables
- `math_operations.py`
- `data_processing.py`
- `database.py`
- `REFACTORING_NOTES.md` (your observations)

---

## Additional Resources

### Documentation
- [GitHub Copilot Quickstart](https://docs.github.com/en/copilot/quickstart)
- [VS Code IntelliSense](https://code.visualstudio.com/docs/editor/intellisense)

### Videos
- [Copilot Tips and Tricks](https://www.youtube.com/watch?v=XXXXXXXXXXXX)

---

## Summary

In this unit, you learned:
- ✅ How AI code completion works
- ✅ Types of code completions (line, multi-line, function, class)
- ✅ How to work with multiple alternatives
- ✅ The four inline code actions (Explain, Fix, Move, Rewrite)
- ✅ Best practices for accepting suggestions
- ✅ Real-world refactoring techniques

**Next:** Unit 2 - Multi-Environment Support
