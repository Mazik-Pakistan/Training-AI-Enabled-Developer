# Unit 1: Get Started with AI-Based Code Testing

## Learning Objectives
After completing this unit, you will be able to:
- Understand the critical role of testing in software development
- Use natural language to describe and generate test cases
- Generate comprehensive unit tests from existing code
- Identify and test edge cases and exceptions
- Verify requirements through systematic testing
- Debug effectively using test feedback

---

## 1. Why Testing Matters

### The Importance of Testing

Testing is not optional—it's essential for:

**Quality Assurance** ✓
- Ensures code works as expected
- Catches bugs before production
- Validates business requirements

**Confidence** ✓
- Safe refactoring
- Confident deployments
- Reduced stress

**Documentation** ✓
- Tests serve as living documentation
- Show how code should be used
- Demonstrate expected behavior

**Cost Savings** ✓
- Bugs found early cost less to fix
- Reduces production incidents
- Minimizes downtime

### The Cost of Not Testing

```
┌─────────────────────────────────────────────┐
│  Bug Discovery Cost                         │
├─────────────────────────────────────────────┤
│                                             │
│  Unit Test:        $1                       │
│  Integration Test: $10                      │
│  QA Testing:       $100                     │
│  Production Bug:   $1,000+                  │
│  Data Loss/Breach: $$$$$$$                  │
│                                             │
└─────────────────────────────────────────────┘
```

### Testing Pyramid

```
       /\
      /  \      E2E Tests (Few)
     /    \     - Full system tests
    /──────\    - Slowest, most expensive
   /        \
  /  Inte-   \  Integration Tests (Some)
 /   gration  \ - Module interactions
/──────────────\- Medium speed/cost
\              /
 \   Unit     / Unit Tests (Many)
  \  Tests   /  - Individual functions
   \        /    - Fast, cheap
    \──────/
     \    /
      \  /
       \/
```

### Types of Tests

**Unit Tests**
- Test individual functions/methods
- Fast execution
- High isolation
- Example: Testing a `calculateTax()` function

**Integration Tests**
- Test module interactions
- Database connections
- API integrations
- Example: Testing API endpoint with database

**End-to-End (E2E) Tests**
- Test complete workflows
- User scenarios
- Full stack
- Example: Complete user registration flow

---

## 2. Writing Test Cases Using Natural Language

### Natural Language Test Generation

With GitHub Copilot, you can describe tests in plain English and generate code.

### Pattern: Comment-Driven Test Creation

**Step 1: Describe the test**
```python
# Test that add function returns correct sum of two positive numbers
```

**Step 2: Copilot generates**
```python
# Test that add function returns correct sum of two positive numbers
def test_add_positive_numbers():
    result = add(2, 3)
    assert result == 5
```

### Comprehensive Test Description Pattern

```python
# Test: calculate_discount function
# Given: price of $100 and discount of 20%
# When: function is called
# Then: should return $80
def test_calculate_discount():
    # Copilot completes...
```

**Copilot generates:**
```python
def test_calculate_discount():
    price = 100
    discount = 20
    result = calculate_discount(price, discount)
    assert result == 80
```

### Test Suite Generation

**Your prompt:**
```python
# Generate comprehensive test suite for User class
# Test cases:
# 1. User creation with valid data
# 2. User creation with invalid email
# 3. Password hashing
# 4. User authentication success
# 5. User authentication failure
```

**Copilot generates:**
```python
import unittest
from user import User

class TestUser(unittest.TestCase):
    
    def test_user_creation_valid_data(self):
        """Test creating user with valid data."""
        user = User("john@example.com", "John Doe", "password123")
        self.assertEqual(user.email, "john@example.com")
        self.assertEqual(user.name, "John Doe")
        self.assertIsNotNone(user.password_hash)
    
    def test_user_creation_invalid_email(self):
        """Test that invalid email raises ValueError."""
        with self.assertRaises(ValueError):
            User("invalid-email", "John Doe", "password123")
    
    def test_password_hashing(self):
        """Test that password is hashed, not stored in plain text."""
        user = User("john@example.com", "John Doe", "password123")
        self.assertNotEqual(user.password_hash, "password123")
        self.assertTrue(len(user.password_hash) > 20)
    
    def test_user_authentication_success(self):
        """Test successful authentication with correct password."""
        user = User("john@example.com", "John Doe", "password123")
        self.assertTrue(user.authenticate("password123"))
    
    def test_user_authentication_failure(self):
        """Test failed authentication with wrong password."""
        user = User("john@example.com", "John Doe", "password123")
        self.assertFalse(user.authenticate("wrongpassword"))

if __name__ == '__main__':
    unittest.main()
```

---

## 3. Generating Unit Tests from Code

### Automatic Test Generation

Copilot can analyze your code and generate appropriate tests.

### Method 1: Using /tests Command

**Your code:**
```python
def calculate_bmi(weight_kg, height_m):
    """Calculate Body Mass Index."""
    if height_m <= 0:
        raise ValueError("Height must be positive")
    if weight_kg <= 0:
        raise ValueError("Weight must be positive")
    
    bmi = weight_kg / (height_m ** 2)
    return round(bmi, 2)
```

**Action:** Select code → Chat → `/tests`

**Copilot generates:**
```python
import unittest
from bmi_calculator import calculate_bmi

class TestCalculateBMI(unittest.TestCase):
    
    def test_normal_bmi(self):
        """Test BMI calculation with normal values."""
        result = calculate_bmi(70, 1.75)
        self.assertEqual(result, 22.86)
    
    def test_zero_height(self):
        """Test that zero height raises ValueError."""
        with self.assertRaises(ValueError) as context:
            calculate_bmi(70, 0)
        self.assertIn("Height must be positive", str(context.exception))
    
    def test_negative_height(self):
        """Test that negative height raises ValueError."""
        with self.assertRaises(ValueError):
            calculate_bmi(70, -1.75)
    
    def test_zero_weight(self):
        """Test that zero weight raises ValueError."""
        with self.assertRaises(ValueError) as context:
            calculate_bmi(0, 1.75)
        self.assertIn("Weight must be positive", str(context.exception))
    
    def test_negative_weight(self):
        """Test that negative weight raises ValueError."""
        with self.assertRaises(ValueError):
            calculate_bmi(-70, 1.75)
    
    def test_rounding(self):
        """Test that result is rounded to 2 decimal places."""
        result = calculate_bmi(70.123, 1.754)
        self.assertIsInstance(result, float)
        self.assertEqual(len(str(result).split('.')[1]), 2)
```

### Method 2: Test-First Pattern

```python
# Write test first describing expected behavior
def test_user_registration():
    # Given: valid user data
    user_data = {
        'username': 'testuser',
        'email': 'test@example.com',
        'password': 'SecurePass123'
    }
    
    # When: user registers
    result = register_user(user_data)
    
    # Then: user should be created successfully
    assert result['success'] == True
    assert 'user_id' in result
    assert result['username'] == 'testuser'

# Now ask Copilot to implement register_user function
```

---

## 4. Handling Edge (Exception) Cases

### What Are Edge Cases?

Edge cases are scenarios at the extremes of operating parameters:
- Minimum/maximum values
- Empty inputs
- Null/None values
- Boundary conditions
- Unexpected types

### Identifying Edge Cases with Copilot

**Your function:**
```python
def divide_list(numbers, divisor):
    """Divide all numbers in list by divisor."""
    return [n / divisor for n in numbers]
```

**Ask Copilot:**
```
What edge cases should I test for divide_list function?
```

**Copilot suggests:**
```
Edge cases to test:
1. Empty list
2. Divisor is zero
3. List contains zero
4. List contains negative numbers
5. List contains floats
6. List contains non-numeric values
7. Very large numbers
8. Very small numbers (near zero)
```

### Generating Edge Case Tests

**Prompt:**
```python
# Generate edge case tests for divide_list function
# Include: empty list, zero divisor, negative numbers, type errors
```

**Copilot generates:**
```python
import unittest
from math_utils import divide_list

class TestDivideListEdgeCases(unittest.TestCase):
    
    def test_empty_list(self):
        """Test with empty list."""
        result = divide_list([], 2)
        self.assertEqual(result, [])
    
    def test_zero_divisor(self):
        """Test that zero divisor raises ZeroDivisionError."""
        with self.assertRaises(ZeroDivisionError):
            divide_list([1, 2, 3], 0)
    
    def test_list_with_zero(self):
        """Test list containing zero."""
        result = divide_list([0, 2, 4], 2)
        self.assertEqual(result, [0.0, 1.0, 2.0])
    
    def test_negative_numbers(self):
        """Test with negative numbers."""
        result = divide_list([-10, -20, -30], 5)
        self.assertEqual(result, [-2.0, -4.0, -6.0])
    
    def test_mixed_positive_negative(self):
        """Test with mixed positive and negative numbers."""
        result = divide_list([10, -20, 30], 5)
        self.assertEqual(result, [2.0, -4.0, 6.0])
    
    def test_float_numbers(self):
        """Test with floating point numbers."""
        result = divide_list([1.5, 2.5, 3.5], 0.5)
        self.assertEqual(result, [3.0, 5.0, 7.0])
    
    def test_very_large_numbers(self):
        """Test with very large numbers."""
        result = divide_list([1e10, 2e10], 1e5)
        self.assertEqual(result, [1e5, 2e5])
    
    def test_very_small_numbers(self):
        """Test with very small numbers."""
        result = divide_list([0.0001, 0.0002], 0.00001)
        self.assertAlmostEqual(result[0], 10.0, places=5)
        self.assertAlmostEqual(result[1], 20.0, places=5)
    
    def test_non_numeric_value(self):
        """Test that non-numeric value raises TypeError."""
        with self.assertRaises(TypeError):
            divide_list([1, 'two', 3], 2)
```

### Common Edge Cases by Data Type

**Strings:**
```python
# Test edge cases for string processing
def test_string_edge_cases():
    # Empty string
    assert process_string("") == expected_result
    
    # Single character
    assert process_string("a") == expected_result
    
    # Very long string
    assert process_string("a" * 10000) == expected_result
    
    # Special characters
    assert process_string("!@#$%^&*()") == expected_result
    
    # Unicode characters
    assert process_string("Hello 世界 🌍") == expected_result
    
    # Whitespace only
    assert process_string("   ") == expected_result
```

**Lists/Arrays:**
```python
# Test edge cases for list operations
def test_list_edge_cases():
    # Empty list
    assert process_list([]) == expected_result
    
    # Single element
    assert process_list([1]) == expected_result
    
    # All same elements
    assert process_list([5, 5, 5, 5]) == expected_result
    
    # Sorted list
    assert process_list([1, 2, 3, 4]) == expected_result
    
    # Reverse sorted
    assert process_list([4, 3, 2, 1]) == expected_result
```

---

## 5. Verifying Requirements Through Tests

### Requirements-Based Testing

Tests should verify that code meets business requirements.

### Example: E-commerce Discount System

**Requirements:**
```
1. 10% discount for orders over $100
2. 20% discount for orders over $500
3. Free shipping for orders over $50
4. Maximum discount is $100
5. Discounts don't apply to sale items
```

**Test-Driven Approach:**

```python
# Test requirement 1: 10% discount for orders over $100
def test_discount_10_percent_over_100():
    """Orders over $100 get 10% discount."""
    order = Order(items=[Item(price=120)])
    discount = calculate_discount(order)
    assert discount == 12.0  # 10% of 120

# Test requirement 2: 20% discount for orders over $500
def test_discount_20_percent_over_500():
    """Orders over $500 get 20% discount."""
    order = Order(items=[Item(price=600)])
    discount = calculate_discount(order)
    assert discount == 120.0  # 20% of 600

# Test requirement 3: Free shipping for orders over $50
def test_free_shipping_over_50():
    """Orders over $50 get free shipping."""
    order = Order(items=[Item(price=60)])
    shipping_cost = calculate_shipping(order)
    assert shipping_cost == 0

# Test requirement 4: Maximum discount is $100
def test_discount_cap_at_100():
    """Discount never exceeds $100."""
    order = Order(items=[Item(price=10000)])  # Would be $2000 discount
    discount = calculate_discount(order)
    assert discount == 100.0

# Test requirement 5: No discount on sale items
def test_no_discount_on_sale_items():
    """Sale items don't get additional discounts."""
    order = Order(items=[Item(price=600, on_sale=True)])
    discount = calculate_discount(order)
    assert discount == 0
```

### Acceptance Criteria Testing

**User Story:**
```
As a user
I want to reset my password
So that I can regain access to my account
```

**Acceptance Criteria:**
```
✓ User receives reset email within 5 minutes
✓ Reset link expires after 24 hours
✓ Old password stops working after reset
✓ New password must meet strength requirements
✓ User is logged in after successful reset
```

**Tests:**
```python
class TestPasswordReset(unittest.TestCase):
    
    def test_reset_email_sent(self):
        """User receives reset email."""
        user = User.objects.create(email="test@example.com")
        request_password_reset(user.email)
        self.assertEqual(len(mail.outbox), 1)
        self.assertIn("Password Reset", mail.outbox[0].subject)
    
    def test_reset_link_expires_after_24_hours(self):
        """Reset link expires after 24 hours."""
        token = create_reset_token(user)
        # Simulate 25 hours passing
        token.created_at = timezone.now() - timedelta(hours=25)
        token.save()
        is_valid = validate_reset_token(token.token)
        self.assertFalse(is_valid)
    
    def test_old_password_invalid_after_reset(self):
        """Old password doesn't work after reset."""
        user = User.objects.create(email="test@example.com")
        old_password = "OldPassword123"
        user.set_password(old_password)
        user.save()
        
        # Reset password
        reset_password(user, "NewPassword456")
        
        # Try old password
        can_login = user.authenticate(old_password)
        self.assertFalse(can_login)
    
    def test_new_password_strength_requirements(self):
        """New password must meet strength requirements."""
        weak_passwords = ["123", "password", "abc"]
        for weak_pass in weak_passwords:
            with self.assertRaises(ValidationError):
                reset_password(user, weak_pass)
    
    def test_user_logged_in_after_reset(self):
        """User is automatically logged in after reset."""
        response = reset_password_and_login(user, "NewPassword456")
        self.assertTrue(response.user.is_authenticated)
```

---

## 6. Debugging with Test Feedback

### Using Test Failures to Find Bugs

Test failures provide valuable debugging information.

**Example: Failing Test**

```python
def test_calculate_total():
    items = [
        {'price': 10.00, 'quantity': 2},
        {'price': 5.50, 'quantity': 3}
    ]
    total = calculate_total(items)
    assert total == 36.50  # FAILS: Expected 36.50, got 36.5
```

**Debugging with Copilot:**

**You ask:**
```
Why is this test failing?
```

**Copilot explains:**
```
The test is failing due to floating-point precision.
36.50 and 36.5 are mathematically equal but not identical in assertion.

Fix 1: Use assertAlmostEqual
self.assertAlmostEqual(total, 36.50, places=2)

Fix 2: Format the result
total = round(calculate_total(items), 2)
assert total == 36.50
```

### Test-Driven Debugging

```python
# Bug: Function returns incorrect results for negative numbers
def absolute_value(n):
    return n if n > 0 else -n  # BUG: should be >= 0

# Write test to expose the bug
def test_absolute_value_zero():
    """Test absolute value of zero."""
    result = absolute_value(0)
    assert result == 0  # FAILS: Expected 0, got -0

# Use Copilot to fix
# Select function → /fix based on test failure
```

### Regression Testing

**Scenario:** Bug found in production

**Step 1: Write test that reproduces the bug**
```python
def test_bug_division_by_zero():
    """
    Bug #123: Division by zero when calculating average of empty list
    Reported: 2026-01-15
    """
    result = calculate_average([])
    # This should not crash
    assert result == 0 or result is None
```

**Step 2: Fix the code**
```python
def calculate_average(numbers):
    """Calculate average of numbers."""
    if not numbers:  # FIX: Handle empty list
        return 0
    return sum(numbers) / len(numbers)
```

**Step 3: Verify fix**
```bash
$ pytest test_bug_fixes.py::test_bug_division_by_zero
PASSED
```

---

## Hands-On Exercises

### Exercise 1: Generate Test Suite
Create tests for this function:
```python
def is_valid_password(password):
    """Check if password meets requirements."""
    if len(password) < 8:
        return False
    if not any(c.isupper() for c in password):
        return False
    if not any(c.isdigit() for c in password):
        return False
    return True

# Use Copilot to generate comprehensive tests
```

### Exercise 2: Edge Case Testing
Identify and test edge cases:
```python
def find_max(numbers):
    """Find maximum number in list."""
    # Generate edge case tests with Copilot
```

### Exercise 3: Requirements Testing
Implement and test these requirements:
```
Shopping Cart Requirements:
1. Items can be added with quantity
2. Item quantity can be updated
3. Items can be removed
4. Total price is calculated correctly
5. Cart cannot exceed 100 items
```

---

## Lab: Comprehensive Testing Project

### Objective
Create a fully tested module using GitHub Copilot.

### Project: Banking System

**Requirements:**
1. Account creation with initial balance
2. Deposit money (positive amounts only)
3. Withdraw money (sufficient balance required)
4. Transfer between accounts
5. Transaction history
6. Monthly interest calculation

### Instructions

**Part 1: Write Tests First (TDD)**
Use Copilot to generate test suite based on requirements

**Part 2: Implement Features**
Use tests to guide implementation

**Part 3: Edge Cases**
Add tests for all edge cases

**Part 4: Integration Tests**
Test multiple operations together

**Deliverables:**
- `bank_account.py` (implementation)
- `test_bank_account.py` (unit tests)
- `test_integration.py` (integration tests)
- Test coverage report (aim for 90%+)

---

## Summary

In this unit, you learned:
- ✅ Why testing is crucial for software quality
- ✅ How to generate tests using natural language
- ✅ Creating unit tests from existing code
- ✅ Identifying and testing edge cases
- ✅ Verifying business requirements through tests
- ✅ Using test feedback for effective debugging

**Next:** Course Completion and Final Project

---

## Module 5 Complete! 🎉

You now have comprehensive skills in:
- GitHub platform fundamentals
- GitHub Copilot features and capabilities
- Inline code assistance and multi-language support
- Conversational development workflows
- Agent mode for complex tasks
- AI-assisted testing strategies

**Ready for the final challenge? Complete the course capstone project!**
