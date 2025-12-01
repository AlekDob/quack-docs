# Prompt Engineering

Master the art of writing effective prompts that generate quality code and precise responses.

## Why Prompt Engineering Matters

The quality of Claude's response is **directly proportional** to the quality of your prompt. A well-written prompt:

- Reduces iterations and development time
- Produces code that respects your architecture
- Prevents bugs and security vulnerabilities
- Communicates expectations and constraints clearly

## The Four Fundamental Elements

Every excellent prompt includes these four key elements:

### 1. Clear Intent

What are you trying to achieve? The primary objective.

**Bad**: "Add authentication"
**Good**: "Add JWT-based authentication to the Express API"

### 2. Specific Context

Technical information, business context, constraints, quality expectations.

**Bad**: "Use a database"
**Good**: "Use PostgreSQL 14 with node-postgres (pg) v8.x"

### 3. Desired Outcome

Explicit success criteria - how do you know it's "complete"?

**Bad**: "Make it work"
**Good**: "Protected routes return 401 if token is missing or invalid"

### 4. Quality Indicators

Definition of "good" - standards, best practices, performance.

**Bad**: "Make it secure"
**Good**: "Hash passwords with bcrypt (minimum 10 rounds), never log passwords"

## Prompt Template

Here's how a perfect prompt looks with all 4 elements:

```
[CLEAR INTENT] - What you want to achieve

Context:
  - [Technical info: framework, libraries, versions]
  - [Existing patterns: files to follow as example]
  - [Constraints: what it should NOT do, limitations]

Requirements:
  - [Functional requirement #1]
  - [Functional requirement #2]
  - [Functional requirement #3]

Success criteria:
  - [Success criterion #1 - measurable]
  - [Success criterion #2 - verifiable]
  - [Success criterion #3 - testable]

Quality expectations:
  - [Code standards: patterns, typing]
  - [Security: validation, sanitization]
  - [Testing: coverage, edge cases]
  - [Performance: metrics, limits]
```

## Example: Vague vs Effective

### Vague Prompt

```
Add user authentication
```

**What's missing?**
- What type of authentication? (JWT, session, OAuth?)
- Where should it be integrated?
- What are the security requirements?
- How do you define "complete"?

### Effective Prompt

```
Add JWT authentication to our Express API:

Context:
  - Using Express 4.x with TypeScript
  - Existing user model in @models/User.ts
  - Protect routes in @routes/api.ts

Requirements:
  - JWT tokens with 24h expiration
  - Login endpoint (POST /auth/login)
  - Middleware to verify tokens (@middleware/auth.ts)
  - Password hashing with bcrypt (minimum 10 rounds)

Success criteria:
  - Protected routes return 401 if no valid token
  - Login returns JWT with valid credentials
  - Tests pass for both success and failure cases

Quality expectations:
  - Follow our error handling pattern (@utils/errors.ts)
  - Add TypeScript types for all functions
  - Include input validation
  - No passwords in logs
```

## Conversational vs Structured Prompts

### When to Use Conversational Prompts

- Initial exploration of a problem
- Brainstorming solutions
- Debugging unclear issues
- Simple and direct requests

**Example:**
```
I noticed the getUserData function in @api.ts is slow when
there are more than 1000 users. Can you analyze the problem
and suggest optimizations? We use Postgres 14.
```

### When to Use Structured Prompts

- Complex features with multiple requirements
- Integrations touching multiple files
- Tasks with specific constraints
- When absolute precision is needed

**Example:**
```
Implement user profile editing

Business Context:
- Users must be able to update their information
- Part of account settings page
- Must prevent duplicate emails

Technical Requirements:
- Add endpoint PUT /api/users/:id/profile
- Update User model to include: bio, avatar_url, location
- Validate email uniqueness before update
- Use existing auth middleware (@middleware/auth.ts)

Success Criteria:
- User can update bio, avatar, location
- Email validation prevents duplicates
- Returns 409 Conflict if email exists
- Requires authentication (401 if not logged in)
```

## How to Choose?

```
Is it a complex feature (>3 requirements)?
  |-- YES -> Use Structured Prompt
  |-- NO -> Conversational Prompt is sufficient

Are there critical constraints (security, performance)?
  |-- YES -> Use Structured Prompt
  |-- NO -> Conversational Prompt is fine

Are you exploring a problem (analysis)?
  |-- YES -> Use Conversational Prompt
  |-- NO -> Evaluate complexity

Will the prompt be shared with the team?
  |-- YES -> Use Structured Prompt (clearer)
  |-- NO -> Choose based on preference
```

## The Importance of Precision

**Key insight:** Precision is NOT verbosity - it's being **specific at critical points**.

### Where to Be Precise (Critical)

1. **Technical Requirements**
   - Bad: "Add database support"
   - Good: "Add PostgreSQL support using node-postgres (pg) v8.x"

2. **Business Logic**
   - Bad: "Calculate the discount"
   - Good: "Apply 10% discount if cart total > 100, 5% if > 50, otherwise 0%"

3. **Integration Points**
   - Bad: "Connect to the API"
   - Good: "Connect to the existing REST API (@services/api.ts) using fetchWithAuth wrapper"

4. **Performance Requirements**
   - Bad: "Make it fast"
   - Good: "Response time < 200ms for queries on tables up to 100k rows"

### Where Claude Can Infer (Low Precision)

- Code formatting (indentation, spacing)
- Import organization
- Basic TypeScript types (if evident from context)
- Naming conventions (if consistent in project)

**Previous**: [The Side Panel](../02-core-concepts/side-panel)

**Next**: [Prompting Patterns](../04-best-practices/prompting-patterns)
