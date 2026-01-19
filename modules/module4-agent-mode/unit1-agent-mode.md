# Unit 1: Get Started with Copilot Agent Mode

## Learning Objectives
After completing this unit, you will be able to:
- Understand what Copilot Agent Mode is and when to use it
- Activate and configure Agent Mode effectively
- Use custom instructions to guide agent behavior
- Create and manage prompt files for repeatable workflows
- Implement advanced agent strategies
- Leverage agents for complex, multi-step tasks
- Optimize agent performance and reliability

---

## 1. Introduction to Agent Mode

### What is Agent Mode?

Agent Mode transforms GitHub Copilot from an assistant into an autonomous developer that can:
- Plan multi-step solutions independently
- Execute complex workflows without constant guidance
- Make decisions based on project context
- Handle errors and iterate on solutions
- Complete entire features with minimal human intervention

```
Traditional Copilot:
You → Copilot → Code
(Interactive, step-by-step)

Agent Mode:
You → Agent → [Planning → Research → Implementation → Testing] → Complete Feature
(Autonomous, end-to-end)
```

### How Agent Mode Works

**Traditional Workflow:**
```
1. You: "Create user authentication"
2. Copilot: [Generates code]
3. You: "Add password hashing"
4. Copilot: [Adds hashing]
5. You: "Add validation"
6. Copilot: [Adds validation]
7. You: "Add tests"
8. Copilot: [Creates tests]
... many interactions ...
```

**Agent Mode Workflow:**
```
1. You: "Create complete user authentication system with 
        password hashing, validation, and tests"
2. Agent: [Plans approach]
        [Creates models]
        [Implements authentication]
        [Adds validation]
        [Writes tests]
        [Verifies everything works]
        [Reports completion]
```

### Key Differences

| Traditional Copilot | Agent Mode |
|---------------------|------------|
| Interactive, step-by-step | Autonomous, multi-step |
| Requires guidance | Makes decisions independently |
| Single-focus responses | Complete feature implementation |
| You manage workflow | Agent manages workflow |
| Quick suggestions | Comprehensive solutions |

### When to Use Agent Mode

**✅ Use Agent Mode for:**
- Complete feature implementation
- Large refactoring tasks
- Complex bug fixes requiring investigation
- Setting up new components/modules
- Implementing multiple related files
- Tasks requiring research and planning
- Repetitive patterns across files

**❌ Don't Use Agent Mode for:**
- Quick one-line changes
- Learning/exploring code (use Chat)
- Simple autocomplete (use Inline)
- When you need to understand each step
- Highly experimental work requiring judgment

### Real-World Examples

**Example 1: Feature Implementation**
```
Task: "Implement complete user profile editing feature"

Agent automatically:
✓ Creates profile model
✓ Builds edit form UI
✓ Implements validation
✓ Adds API endpoints
✓ Writes integration tests
✓ Updates documentation
✓ Verifies all components work together
```

**Example 2: Bug Fix**
```
Task: "Fix the memory leak in the image processing pipeline"

Agent automatically:
✓ Analyzes codebase for memory issues
✓ Identifies problematic code sections
✓ Researches best practices for fix
✓ Implements solution
✓ Adds memory usage monitoring
✓ Creates tests to prevent regression
✓ Verifies fix resolves issue
```

**Example 3: Refactoring**
```
Task: "Refactor authentication to use JWT instead of sessions"

Agent automatically:
✓ Analyzes current session implementation
✓ Plans migration strategy
✓ Installs JWT libraries
✓ Refactors auth middleware
✓ Updates login/logout endpoints
✓ Migrates tests
✓ Updates configuration
✓ Creates migration guide
```

---

## 2. Activating and Using Agent Mode

### How to Activate Agent Mode

**Method 1: Through Chat Interface**
```
1. Open Copilot Chat (Ctrl+Alt+I / Cmd+Shift+I)
2. Type: @workspace followed by your request
3. Add [Agent Mode] or @agent
4. Press Enter
```

**Method 2: Through Command Palette**
```
1. Press Ctrl+Shift+P (Cmd+Shift+P on Mac)
2. Type: "GitHub Copilot: Start Agent"
3. Enter your task description
4. Press Enter
```

**Method 3: Using Hashtag**
```
In Copilot Chat:
#github-pull-request_copilot-coding-agent Implement user profile feature
```

### Agent Mode Interface

```
┌──────────────────────────────────────────┐
│  🤖 Copilot Agent                        │
├──────────────────────────────────────────┤
│  Task: Implement user authentication     │
│                                          │
│  📋 Planning Phase                       │
│  ✓ Analyzed project structure           │
│  ✓ Identified required files            │
│  ✓ Determined dependencies              │
│                                          │
│  🔨 Implementation Phase                 │
│  ⏳ Creating user model...              │
│  ⏳ Implementing auth routes...          │
│  □ Adding validation...                  │
│  □ Writing tests...                      │
│                                          │
│  Progress: 40%                           │
└──────────────────────────────────────────┘
```

### Monitoring Agent Progress

**Agent provides real-time updates:**
```
🤖 Agent: Starting task analysis...
🤖 Agent: Found 3 files to modify
🤖 Agent: Creating models/user.py
✓ Agent: Created user model with validation
🤖 Agent: Implementing authentication logic
✓ Agent: Added login and register endpoints
🤖 Agent: Writing unit tests
✓ Agent: Created 8 test cases
🤖 Agent: Running tests to verify
✓ Agent: All tests passing
🤖 Agent: Task completed successfully!
```

### Providing Feedback to Agent

**During execution:**
```
You: "Use bcrypt for password hashing, not plain text"
Agent: "Updating to use bcrypt... Done!"

You: "Add rate limiting to prevent brute force"
Agent: "Adding rate limiting with 5 attempts per 15 minutes... Done!"
```

**If agent is stuck:**
```
You: "Focus on the login endpoint first"
Agent: "Understood. Completing login endpoint before proceeding."
```

### Agent Completion

**Successful Completion:**
```
✅ Task Completed: User Authentication System

Summary:
- Created 5 files
- Modified 2 existing files
- Added 157 lines of code
- Created 8 unit tests (all passing)
- Updated documentation

Files Changed:
✓ models/user.py (new)
✓ routes/auth.py (new)
✓ middleware/auth.py (new)
✓ tests/test_auth.py (new)
✓ config/settings.py (modified)
✓ requirements.txt (modified)

Next Steps:
- Review generated code
- Test manually in browser
- Deploy to staging environment
```

**Partial Completion:**
```
⚠️ Task Partially Completed

Completed:
✓ User model created
✓ Basic authentication implemented
✓ Tests written

Blocked On:
❌ Email service not configured
   → Need SMTP credentials in .env

Human Input Required:
Please add to .env:
  SMTP_HOST=smtp.example.com
  SMTP_PORT=587
  SMTP_USER=your-email@example.com
  SMTP_PASS=your-password

After adding credentials, I can complete:
- Email verification
- Password reset functionality
```

---

## 3. Using Custom Instructions and Prompt Files

### Custom Instructions

Custom instructions are persistent guidelines that shape how the agent behaves across all tasks.

### Creating Custom Instructions

**Access Settings:**
```
1. Open VS Code Settings
2. Search: "GitHub Copilot"
3. Find: "Copilot: Custom Instructions"
4. Add your instructions
```

**Example Custom Instructions:**

```markdown
# Development Standards

## Code Style
- Use TypeScript with strict mode
- Follow Airbnb style guide
- Maximum function length: 50 lines
- Prefer functional programming patterns
- Use async/await over promises

## Testing
- Write tests for all public functions
- Minimum 80% code coverage
- Use Jest for testing
- Include edge cases

## Security
- Never commit secrets or API keys
- Use environment variables for configuration
- Validate all user inputs
- Implement rate limiting on APIs
- Use parameterized queries (no SQL injection)

## Documentation
- Add JSDoc comments for all functions
- Include examples in documentation
- Update README for new features
- Document API endpoints with examples

## Error Handling
- Use try-catch for async operations
- Log errors with context
- Return meaningful error messages
- Never expose internal errors to users

## Performance
- Optimize database queries
- Implement caching where appropriate
- Lazy load resources
- Monitor for N+1 query problems
```

**Domain-Specific Instructions:**

```markdown
# E-Commerce Application Standards

## Data Models
- All prices stored in cents (integers)
- Use Decimal type for calculations
- Include audit fields: created_at, updated_at, created_by, updated_by
- Soft delete: use deleted_at instead of hard deletes

## Business Rules
- Orders cannot be modified after payment
- Inventory checks required before order placement
- Send email notification on order status changes
- Maintain order history for auditing

## API Responses
- Always include timestamp
- Use snake_case for JSON keys
- Include pagination metadata for lists
- Return 404 for not found, not 200 with empty object
```

### Prompt Files

Prompt files are reusable templates for common tasks.

### Creating Prompt Files

**Structure:**
```
project-root/
├── .github/
│   └── copilot/
│       └── prompts/
│           ├── new-feature.md
│           ├── bug-fix.md
│           ├── refactor.md
│           └── documentation.md
```

**Example: new-feature.md**

```markdown
# New Feature Implementation

## Context
Project: [PROJECT_NAME]
Feature: [FEATURE_NAME]
Related Files: [RELATED_FILES]

## Requirements
[DETAILED_REQUIREMENTS]

## Implementation Checklist
- [ ] Create/update data models
- [ ] Implement business logic
- [ ] Add input validation
- [ ] Create API endpoints (if applicable)
- [ ] Write unit tests (min 80% coverage)
- [ ] Write integration tests
- [ ] Add error handling
- [ ] Update documentation
- [ ] Add logging for debugging
- [ ] Performance optimization

## Code Standards
- Follow existing project patterns
- Use TypeScript strict mode
- Add comprehensive comments
- Include examples in docstrings

## Testing Requirements
- Unit tests for all functions
- Integration tests for workflows
- Edge case testing
- Error scenario testing

## Security Considerations
- Input validation and sanitization
- Authentication/authorization checks
- Rate limiting (if applicable)
- Audit logging

## Deliverables
- Implementation code
- Test suite
- Documentation update
- Migration scripts (if database changes)
```

**Example: bug-fix.md**

```markdown
# Bug Fix Template

## Bug Description
Issue: [ISSUE_NUMBER]
Description: [BUG_DESCRIPTION]
Reproduction Steps: [STEPS]
Expected Behavior: [EXPECTED]
Actual Behavior: [ACTUAL]

## Investigation Checklist
- [ ] Review error logs
- [ ] Analyze stack trace
- [ ] Check recent changes (git blame)
- [ ] Reproduce bug locally
- [ ] Identify root cause
- [ ] Verify no related issues

## Fix Implementation
- [ ] Implement fix
- [ ] Add validation to prevent issue
- [ ] Update error handling
- [ ] Add logging for debugging
- [ ] Verify fix works

## Testing
- [ ] Write test reproducing bug
- [ ] Verify test fails before fix
- [ ] Verify test passes after fix
- [ ] Test edge cases
- [ ] Regression testing

## Documentation
- [ ] Update inline comments
- [ ] Add to CHANGELOG
- [ ] Update known issues list (if applicable)
- [ ] Document solution for future reference
```

### Using Prompt Files with Agent

**Method 1: Reference in Chat**
```
@agent Implement new feature following .github/copilot/prompts/new-feature.md

Feature: User Profile Editing
Requirements:
- Users can update name, email, bio
- Email changes require verification
- Profile picture upload (max 5MB)
```

**Method 2: Inline Template**
```
@agent Fix bug #123 following bug-fix template

Bug: Users can submit empty forms
Root Cause: Missing client-side validation
Fix: Add validation before form submission
```

### Variable Substitution in Prompts

**Template with Variables:**
```markdown
# API Endpoint Template

Create REST API endpoint:
- Path: /api/{{RESOURCE}}/{{ACTION}}
- Method: {{HTTP_METHOD}}
- Authentication: {{AUTH_TYPE}}
- Rate Limit: {{RATE_LIMIT}}

Request Body:
{{REQUEST_SCHEMA}}

Response:
{{RESPONSE_SCHEMA}}

Validation:
{{VALIDATION_RULES}}
```

**Usage:**
```
@agent Create endpoint using api-endpoint.md

Variables:
- RESOURCE: users
- ACTION: profile
- HTTP_METHOD: PUT
- AUTH_TYPE: JWT
- RATE_LIMIT: 10 per minute
- REQUEST_SCHEMA: {name: string, bio: string}
- RESPONSE_SCHEMA: {user: User, message: string}
- VALIDATION_RULES: name (3-50 chars), bio (max 500 chars)
```

---

## 4. Agent Strategies for Complex Tasks

### Strategy 1: Divide and Conquer

**For Large Features:**
```
Task: "Build complete e-commerce checkout system"

Phase 1: @agent Create shopping cart model and basic operations
Phase 2: @agent Implement payment processing integration
Phase 3: @agent Add order confirmation and email notifications
Phase 4: @agent Write comprehensive test suite
Phase 5: @agent Add error handling and edge cases
```

**Benefits:**
- More control over each phase
- Easier to review incremental changes
- Can adjust strategy between phases
- Reduced risk of errors

### Strategy 2: Iterative Refinement

**Initial Implementation:**
```
@agent Create basic user authentication with email/password
```

**Refinement 1:**
```
@agent Add password strength validation and account verification
```

**Refinement 2:**
```
@agent Add rate limiting and account lockout after failed attempts
```

**Refinement 3:**
```
@agent Add two-factor authentication support
```

### Strategy 3: Test-Driven Development

**Step 1: Define Tests**
```
@agent Write comprehensive test suite for user registration:
- Valid registration
- Duplicate email rejection
- Password strength validation
- Email format validation
- Required fields validation
```

**Step 2: Implement Features**
```
@agent Implement user registration to pass all tests
```

**Benefits:**
- Clear requirements from tests
- Guaranteed test coverage
- Prevents regression
- Documents expected behavior

### Strategy 4: Progressive Enhancement

**Base Implementation:**
```
@agent Create basic blog post CRUD operations
```

**Enhancement 1:**
```
@agent Add markdown support for post content
```

**Enhancement 2:**
```
@agent Add image uploads with automatic optimization
```

**Enhancement 3:**
```
@agent Add tags and categories with search
```

**Enhancement 4:**
```
@agent Add comments with moderation
```

### Strategy 5: Parallel Development

**For Independent Features:**
```
Terminal 1: @agent Implement user profile management
Terminal 2: @agent Implement notification system
Terminal 3: @agent Implement analytics dashboard
```

**Benefits:**
- Faster development
- Independent testing
- Reduced conflicts

### Strategy 6: Template-Based Development

**Create Reusable Patterns:**
```
@agent Create CRUD controller following this pattern:

[Provide example controller]

Now create similar controllers for:
- Products
- Categories  
- Orders
- Reviews
```

---

## Hands-On Exercises

### Exercise 1: First Agent Task

**Simple Task:**
```
@agent Create a TODO list manager:
- Add tasks with title and description
- Mark tasks as complete
- Delete tasks
- List all tasks
- Filter by completion status
```

**Observe:**
- How agent plans the task
- Files agent creates
- Implementation approach
- Testing strategy

### Exercise 2: Custom Instructions

**Create custom instructions for:**
```markdown
# My Development Preferences

Code Style:
- [Your preferences]

Testing:
- [Your requirements]

Documentation:
- [Your standards]

Security:
- [Your rules]
```

**Then ask agent to:**
```
@agent Create user authentication system
```

**Verify agent follows your instructions.**

### Exercise 3: Prompt File Creation

**Create prompt file:** `.github/copilot/prompts/api-endpoint.md`

**Use it:**
```
@agent Create API endpoint following api-endpoint.md template
for managing blog posts
```

### Exercise 4: Complex Multi-Phase Task

**Phase 1:**
```
@agent Set up Express.js project structure with TypeScript
```

**Phase 2:**
```
@agent Add PostgreSQL database with Prisma ORM
```

**Phase 3:**
```
@agent Implement user authentication with JWT
```

**Phase 4:**
```
@agent Add comprehensive test suite
```

---

## Real-World Scenarios

### Scenario 1: Greenfield Project Setup

**Task:**
```
@agent Initialize a new React + Node.js project:

Frontend:
- React 18 with TypeScript
- Vite for build
- React Router for navigation
- Tailwind CSS for styling
- Axios for API calls

Backend:
- Express with TypeScript
- PostgreSQL with Prisma
- JWT authentication
- Input validation with Joi
- API documentation with Swagger

Setup:
- Project structure
- Configuration files
- Development scripts
- Basic authentication
- Example CRUD operations
- Test framework
```

### Scenario 2: Legacy Code Refactoring

**Task:**
```
@agent Refactor legacy authentication system:

Current State:
- Uses plain passwords (no hashing)
- Session-based (in-memory)
- No rate limiting
- No input validation
- No tests

Target State:
- Bcrypt password hashing
- JWT token-based
- Redis session storage
- Rate limiting (express-rate-limit)
- Comprehensive validation
- Full test coverage
- Backward compatibility during migration
```

### Scenario 3: Feature Addition to Existing Project

**Task:**
```
@agent Add real-time notifications to existing app:

Requirements:
- WebSocket connection with Socket.io
- Notification model in existing database
- User preferences for notifications
- Mark as read functionality
- Notification center UI component
- Push notifications for browser
- Email fallback for offline users
- Integrate with existing auth system
- Don't break existing features
```

---

## Best Practices

### 1. Clear Task Description

**❌ Vague:**
```
@agent Fix the bug
```

**✅ Clear:**
```
@agent Fix bug where users can submit forms with empty required fields.
Add client-side validation, server-side validation, and appropriate error messages.
```

### 2. Provide Context

**❌ No Context:**
```
@agent Add authentication
```

**✅ With Context:**
```
@agent Add JWT authentication to existing Express API.
Current setup: Node.js, Express, PostgreSQL, Prisma.
Requirements: Login, register, token refresh, password reset.
Follow existing code style and patterns.
```

### 3. Set Expectations

**Include:**
- What should be created
- What should be modified
- What should be preserved
- Testing requirements
- Documentation needs

### 4. Monitor and Guide

**Don't:**
- Start agent and walk away
- Ignore agent questions
- Assume agent knows everything

**Do:**
- Watch progress
- Answer questions promptly
- Provide feedback
- Verify outputs

### 5. Review Agent Output

**Always:**
- ✓ Review generated code
- ✓ Run tests
- ✓ Test manually
- ✓ Check for security issues
- ✓ Verify documentation
- ✓ Ensure code style consistency

---

## Knowledge Check

### Quick Quiz

1. What is the main difference between Chat and Agent Mode?
2. When should you use Agent Mode?
3. What are custom instructions?
4. What are prompt files used for?
5. What's the best strategy for very large tasks?

### Answers
1. Chat is interactive/step-by-step; Agent is autonomous/multi-step
2. For complete features, large refactoring, complex multi-file tasks
3. Persistent guidelines that shape agent behavior across all tasks
4. Reusable templates for common tasks and workflows
5. Divide and conquer - break into smaller phases

---

## Lab: Build Complete Feature with Agent

### Objective
Use Agent Mode to build a complete feature from scratch.

### Project: Blog API with Comments

**Requirements:**
```
@agent Create a complete blog API with comments:

Backend (Node.js + Express + TypeScript):
- Post model: title, content, author, published_at
- Comment model: content, author, post_id, parent_id (for nested comments)
- CRUD operations for posts
- CRUD operations for comments
- Nested comments support (1 level deep)
- Authentication with JWT
- Input validation
- Rate limiting
- Pagination for lists

Features:
- Create/edit/delete posts (authenticated authors only)
- Publish/unpublish posts
- Add comments to posts (authenticated users)
- Reply to comments
- Delete own comments
- Get all posts (published only for non-authors)
- Get single post with comments tree

Testing:
- Unit tests for models
- Integration tests for API endpoints
- Test authentication/authorization
- Edge case testing

Documentation:
- API documentation with examples
- Setup instructions
- Environment variables guide

Deliverables:
- Complete, working API
- Test suite (80%+ coverage)
- README with setup and usage
- Example .env file
```

### Evaluation Criteria

**Code Quality:**
- [ ] Clean, readable code
- [ ] Proper error handling
- [ ] Security best practices
- [ ] Performance considerations

**Testing:**
- [ ] All tests pass
- [ ] Good coverage (80%+)
- [ ] Edge cases covered

**Documentation:**
- [ ] Clear setup instructions
- [ ] API documentation
- [ ] Code comments where needed

**Functionality:**
- [ ] All requirements implemented
- [ ] Works as expected
- [ ] No critical bugs

---

## Summary

In this unit, you learned:
- ✅ What Agent Mode is and when to use it
- ✅ How to activate and monitor agents
- ✅ Custom instructions for consistent behavior
- ✅ Prompt files for reusable workflows
- ✅ Strategies for complex tasks
- ✅ Best practices for agent effectiveness

**🎉 Module 4 Complete!**

You now have all the skills to leverage AI at every level:
- Inline completion for quick coding
- Chat for learning and problem-solving
- Agent Mode for autonomous feature development

**Next:** Module 5 - Testing with GitHub Copilot

---

## Additional Resources

### Documentation
- [GitHub Copilot Agent Mode](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-agent-mode)
- [Custom Instructions Guide](https://docs.github.com/en/copilot/customizing-copilot)

### Tips
- Start with clear, detailed task descriptions
- Break complex tasks into phases
- Monitor agent progress actively
- Always review generated code
- Build reusable prompt templates
- Learn from agent's approaches

**You're now an AI-Enabled Developer! 🚀**
