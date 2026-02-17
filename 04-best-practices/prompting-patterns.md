Proven patterns for common scenarios you'll encounter frequently.

## Building Contextual Chains

For complex tasks, **break the prompt into contextual chains** instead of a monolithic mega-prompt.

### The Analysis - Implementation - Extension Pattern

**Why it works:**
- Allows Claude to reason step-by-step
- You can correct direction after each step
- Builds shared understanding progressively

**Step 1 - Analysis**
```
Analyze the current error handling pattern in @utils/errors.ts
and @routes/*.ts. How are errors currently handled?
```

*Wait for response. Claude explains the current pattern.*

**Step 2 - Implementation**
```
Now add centralized error handling middleware that:
- Catches all errors from routes
- Logs with Winston (existing logger @utils/logger.ts)
- Returns consistent JSON format
- Uses the same pattern you identified
```

*Wait for implementation. Verify it's correct.*

**Step 3 - Extension**
```
Great! Now add custom error classes for:
- ValidationError (400)
- NotFoundError (404)
- UnauthorizedError (401)
Save them in @utils/errors.ts and update routes to use them
```

---

## Pattern 1: Feature Request

**When to use:** Adding new functionality.

### Template

```
[BUSINESS CONTEXT]
Why this feature? Who benefits?

[TECHNICAL REQUIREMENTS]
What to build? Technologies?

[INTEGRATION POINTS]
Where does it fit? Existing files?

[SUCCESS CRITERIA]
How do you know it's done?

[QUALITY EXPECTATIONS]
Tests? Performance? Security?
```

### Real Example

```
Add product search functionality

Business Context:
- Users need to find products quickly
- Search by name, category, tags
- Part of main navigation

Technical Requirements:
- Add endpoint GET /api/products/search
- Accept query params: q (search term), category, tags[]
- Use PostgreSQL full-text search (existing setup)
- Return max 50 results, sorted by relevance

Integration Points:
- Add route in @routes/products.ts
- Use existing Product model (@models/Product.ts)
- Connect to SearchBar component (@components/SearchBar.tsx)

Success Criteria:
- Search returns relevant results in < 500ms
- Handles typos (fuzzy matching)
- Empty query returns 400 Bad Request
- Results include: id, name, category, price, image_url

Quality Expectations:
- Add tests for search accuracy
- Sanitize input (prevent SQL injection)
- Cache frequent searches (Redis)
- Log slow queries (> 1s) for monitoring
```

---

## Pattern 2: Debugging

**When to use:** Fixing bugs or performance issues.

### Template

```
[SYMPTOM]
What's broken? Error message?

[EXPECTED BEHAVIOR]
What should happen?

[CONTEXT]
When does it occur? Environment?

[WHAT YOU TRIED]
Steps already attempted?

[RELEVANT FILES]
@files that might be involved
```

### Real Example

```
Debug memory leak in API server

Symptom:
- Memory usage grows from 200MB to 2GB in 6 hours
- Eventually crashes with 'Out of Memory'
- Happens only in production, not in dev

Expected Behavior:
- Memory should stabilize around 300-400MB

Context:
- Started after deploy v2.3.0 (added caching)
- Happens only in production (staging OK)
- Normal traffic ~500 requests/min
- Spike to 2000/min when timeout occurs

What I Tried:
- Checked event listener leaks (none found)
- Reviewed recent changes (caching logic suspicious)
- Heap snapshot shows Map() object growing

Relevant Files:
@services/cache.ts @middleware/response-cache.ts @routes/api.ts

Please:
1. Analyze cache implementation for leaks
2. Suggest fix with appropriate cleanup
3. Add memory monitoring
```

---

## Pattern 3: Refactoring

**When to use:** Improving existing code.

### Template

```
[CURRENT STATE]
What needs refactoring? Why?

[DESIRED STATE]
What should it become?

[CONSTRAINTS]
What must NOT change? (API, behavior)

[SCOPE]
Which files/functions?
```

### Real Example

```
Refactor authentication logic

Current State:
- Auth code scattered across multiple route files
- JWT validation logic duplicated
- Hard to test, hard to maintain
- See @routes/users.ts @routes/orders.ts @routes/admin.ts

Desired State:
- Auth centralized in @middleware/auth.ts
- Single JWT verify function
- Reusable middleware for protected routes
- Easy to add role-based access control later

Constraints:
- MUST NOT change API endpoints or response format
- MUST maintain backward compatibility
- Existing tests must still pass

Scope:
- Extract auth logic from all route files
- Create authenticate middleware
- Create requireRole middleware (for future use)
- Update routes to use new middleware

Quality:
- Add unit tests for middleware
- Document usage in code comments
- Follow existing error handling pattern
```

---

## Common Pitfalls to Avoid

### 1. Ambiguity

**Bad**: "Improve the API"
**Good**: "Add pagination to GET /api/users with limit and offset params"

### 2. Information Overload

**Bad**: Including entire codebase history
**Good**: Reference only relevant files with @notation

### 3. Missing Constraints

**Bad**: "Add file upload"
**Good**: "Add file upload: max 5MB, only images (jpg, png, webp), store in S3"

### 4. Vague Success Criteria

**Bad**: "Make sure it works"
**Good**: "Tests pass, response time < 200ms, handles 1000 concurrent uploads"

---

## Context-Aware Prompting

### When to Reference Files Explicitly

Use @references when:

1. **Files not obvious from context**
   ```
   Explain the authentication flow @middleware/auth.ts @services/jwt.ts
   ```

2. **Need to see current implementation**
   ```
   Refactor to use async/await @utils/database.ts
   ```

3. **Multi-file coordination**
   ```
   Synchronize these two implementations @client/api.ts @server/routes.ts
   ```

4. **Pattern to replicate**
   ```
   Create a similar validator for Product @validators/UserValidator.ts
   ```

### When NOT to Reference Files

- File already mentioned in current conversation
- General project patterns (Claude infers from other files)
- Standard files (README, package.json)

---

## Summary

**Key takeaways:**

1. **Use the 4 elements**: Intent, Context, Outcome, Quality
2. **Choose your style**: Conversational for exploration, Structured for implementation
3. **Be precise where it matters**: Technical requirements, business logic, integration points
4. **Chain complex tasks**: Analysis - Implementation - Extension
5. **Use patterns**: Feature Request, Debugging, Refactoring
6. **Avoid pitfalls**: Ambiguity, overload, missing constraints

**Previous**: [Prompt Engineering](../03-advanced-techniques/prompt-engineering)
