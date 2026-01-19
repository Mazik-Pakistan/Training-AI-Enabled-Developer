# Lab 2: GitHub Copilot Fundamentals

## Objective
Master GitHub Copilot's core features by building a practical application with AI assistance.

## Duration
90-120 minutes

## Prerequisites
- GitHub Copilot installed and activated
- Completed Module 1
- Basic Python or JavaScript knowledge

---

## Project: Task Manager CLI Application

You'll build a command-line task manager application using GitHub Copilot to assist with:
- Code generation
- Function implementation
- Error handling
- Testing
- Documentation

---

## Part 1: Project Setup (10 minutes)

### Step 1: Create Project Structure
```bash
mkdir task-manager
cd task-manager
git init
```

### Step 2: Create Initial Files
```bash
touch task_manager.py
touch test_task_manager.py
touch README.md
```

### Step 3: Open in VS Code
```bash
code .
```

---

## Part 2: Core Functionality with Copilot (30 minutes)

### Step 1: Define Task Class

Open `task_manager.py` and let Copilot help you:

**Your comment:**
```python
# Task class to represent a task with id, title, description, status, and created_at
# Include methods to mark as complete and convert to dictionary
```

**Wait for Copilot suggestion, then accept with Tab**

**Expected result:**
```python
from datetime import datetime

class Task:
    def __init__(self, id, title, description=""):
        self.id = id
        self.title = title
        self.description = description
        self.status = "pending"
        self.created_at = datetime.now()
    
    def mark_complete(self):
        """Mark task as completed."""
        self.status = "completed"
    
    def to_dict(self):
        """Convert task to dictionary."""
        return {
            'id': self.id,
            'title': self.title,
            'description': self.description,
            'status': self.status,
            'created_at': self.created_at.isoformat()
        }
```

### Step 2: TaskManager Class

**Your comment:**
```python
# TaskManager class to manage a list of tasks
# Methods: add_task, list_tasks, complete_task, delete_task, save_to_file, load_from_file
```

**Let Copilot generate the class**

### Step 3: CLI Interface

**Your comment:**
```python
# Command-line interface for task manager
# Commands: add, list, complete, delete, quit
# Use input() to get user commands
# Main loop to keep program running
```

**Let Copilot generate the CLI**

---

## Part 3: Using Copilot Chat (20 minutes)

### Exercise 1: Explain Code
1. Select the `TaskManager` class
2. Press `Ctrl+I` (inline chat)
3. Type: `/explain`
4. Read and understand Copilot's explanation

### Exercise 2: Fix Issues
1. Select the `save_to_file` method
2. Press `Ctrl+I`
3. Type: `/fix add error handling for file operations`
4. Review and accept suggestions

### Exercise 3: Add Features
1. Open Copilot Chat panel (`Ctrl+Alt+I`)
2. Ask: "How can I add task priority (high, medium, low) to the Task class?"
3. Implement the suggested changes
4. Ask: "How do I sort tasks by priority?"
5. Add sorting functionality

---

## Part 4: Testing with Copilot (25 minutes)

### Step 1: Generate Test Structure

Open `test_task_manager.py`:

**Your comment:**
```python
# Comprehensive test suite for Task and TaskManager classes
# Test task creation, completion, task manager operations
# Use unittest framework
```

**Let Copilot generate tests**

### Step 2: Add Specific Tests

**Use Copilot to generate:**
```python
# Test case: Creating task with valid data
# Test case: Marking task as complete
# Test case: Adding task to task manager
# Test case: Listing all tasks
# Test case: Completing a task by ID
# Test case: Deleting a task by ID
# Test case: Saving and loading tasks from file
```

### Step 3: Run Tests
```bash
python -m pytest test_task_manager.py -v
```

### Step 4: Fix Failing Tests
1. If any tests fail, select the failing test
2. Use `/fix` command in inline chat
3. Review and implement fix
4. Re-run tests

---

## Part 5: Multiple Alternatives (15 minutes)

### Exercise: Different Implementations

For the `list_tasks` method, explore alternatives:

**Try 1:** Basic implementation
```python
def list_tasks(self):
    # Let Copilot suggest
```

**Try 2:** Press `Alt+]` for next suggestion
- Compare different approaches
- Note differences in:
  - Return types
  - Formatting
  - Error handling

**Try 3:** Press `Alt+]` again
- Evaluate which is best for your needs

### Task: Choose Best Implementation
1. Review all alternatives
2. Consider:
   - Readability
   - Functionality
   - Error handling
   - Performance
3. Select and accept the best one

---

## Part 6: Code Actions (20 minutes)

### Exercise 1: Explain Complex Code

Select this code and use `/explain`:
```python
tasks = sorted([t for t in self.tasks if t.status == 'pending'], 
               key=lambda x: x.created_at)
```

### Exercise 2: Rewrite for Clarity

Select the same code and use `/rewrite for better readability`

Compare results.

### Exercise 3: Add Error Handling

Select the entire `TaskManager` class:
1. Use `/fix add comprehensive error handling`
2. Review suggestions
3. Accept useful additions

### Exercise 4: Move to Separate Module

1. Select the `Task` class
2. Type: `/move to separate file task.py`
3. Let Copilot create the new file and update imports

---

## Part 7: Documentation with Copilot (15 minutes)

### Step 1: Add Docstrings

For each function without a docstring:
1. Place cursor after function definition
2. Type `"""`
3. Let Copilot generate docstring
4. Review and adjust as needed

### Step 2: Generate README

In `README.md`:

**Your prompt:**
```markdown
# Task Manager CLI

<!-- Use Copilot to generate:
- Project description
- Features list
- Installation instructions
- Usage examples
- Contributing guidelines
-->
```

**Let Copilot complete the documentation**

### Step 3: Add Code Comments

Use Copilot Chat:
- "Add comments explaining the complex parts of the code"
- Review and accept meaningful comments

---

## Part 8: Enhancements (15 minutes)

### Add Features with Copilot

**Feature 1: Search Tasks**
```python
# Method to search tasks by keyword in title or description
# Should be case-insensitive
# Return list of matching tasks
def search_tasks(self, keyword):
```

**Feature 2: Filter by Status**
```python
# Method to filter tasks by status (pending, completed)
# Return filtered list of tasks
def filter_by_status(self, status):
```

**Feature 3: Task Statistics**
```python
# Method to get task statistics
# Return dictionary with total, completed, pending counts
def get_statistics(self):
```

---

## Deliverables

Your completed project should have:

✅ Working task manager CLI
✅ Complete Task and TaskManager classes
✅ Comprehensive test suite (80%+ coverage)
✅ Error handling throughout
✅ Full documentation
✅ Additional features (search, filter, stats)

---

## Testing Your Application

### Manual Testing
```bash
# Run the application
python task_manager.py

# Try these commands:
add
list
complete 1
delete 2
quit
```

### Automated Testing
```bash
# Run test suite
python -m pytest test_task_manager.py -v

# With coverage
python -m pytest --cov=task_manager test_task_manager.py
```

---

## Bonus Challenges

### Challenge 1: Add Due Dates
Use Copilot to add due date functionality:
- Add due_date field to Task
- Add method to check overdue tasks
- Sort by due date

### Challenge 2: Color Output
Add colored terminal output:
```python
# Add colored output for task status
# Green for completed, yellow for pending, red for overdue
```

### Challenge 3: Export to CSV
Add CSV export functionality:
```python
# Method to export tasks to CSV file
# Include all task fields
```

---

## Reflection Questions

1. How did Copilot help speed up development?
2. Were there any incorrect suggestions? How did you identify them?
3. Which Copilot feature was most useful?
4. When did you prefer writing code yourself vs using Copilot?
5. How can you improve your prompts for better suggestions?

---

## Self-Assessment

Rate your understanding (1-5):

- [ ] Using inline code completion
- [ ] Navigating multiple suggestions
- [ ] Using chat interface effectively
- [ ] Applying code actions (explain, fix, rewrite)
- [ ] Generating tests with Copilot
- [ ] Reviewing and validating AI suggestions

---

## Next Steps

- Refactor the code using Copilot's suggestions
- Add more features (tags, categories, reminders)
- Create a web interface for the task manager
- Deploy as a Python package

**Continue to:** [Lab 3 - Conversational Development](lab3-conversational-development.md)
