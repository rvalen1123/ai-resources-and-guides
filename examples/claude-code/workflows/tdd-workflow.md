# Test-Driven Development (TDD) Workflow

> **Write tests first, implement to pass, refactor with confidence**

## Overview

Test-Driven Development with Claude Code combines extended thinking for test design with subagents for implementation and verification.

## The TDD Cycle

```
1. Think → Write Tests (Red)
2. Implement → Make Tests Pass (Green)  
3. Think → Refactor (Refactor)
4. Repeat
```

## Workflow Steps

### Step 1: Understand Requirements

```bash
> Analyze these requirements and identify test cases think hard

Requirements:
[Paste or describe requirements]

Expected output:
- Core functionality to test
- Edge cases to cover
- Error scenarios
- Integration points
```

**What Claude does:**
- Analyzes requirements comprehensively
- Identifies testable behaviors
- Suggests edge cases
- Recommends test structure

### Step 2: Write Comprehensive Tests

```bash
> Use the test-writer subagent to create comprehensive tests for [feature]

Include:
- Happy path scenarios
- Error cases
- Edge cases
- Boundary conditions
```

**Example:**
```bash
> Use test-writer to create tests for a user authentication system

Tests should cover:
- Successful login with valid credentials
- Failed login with invalid password
- Failed login with non-existent user
- Account lockout after multiple failures
- Session expiration
- Concurrent login attempts
```

### Step 3: Verify Tests Fail (Red)

```bash
> Run the tests to verify they fail for the right reasons

# Should see failures because implementation doesn't exist yet
```

**Important:** Tests should fail because the feature isn't implemented, not because tests are broken.

### Step 4: Implement Minimal Code (Green)

```bash
> Implement the [feature] to make the tests pass

Guidelines:
- Minimal code to pass tests
- Don't over-engineer
- Focus on making tests green
```

**Example:**
```bash
> Implement the user authentication function to pass the tests

Follow these patterns:
- Use bcrypt for password hashing
- Return clear error messages
- Log authentication attempts
- Follow existing auth patterns in ./src/auth/
```

### Step 5: Run Tests

```bash
> Run the test suite and fix any failures

# Iterate until all tests pass
```

### Step 6: Refactor (if needed)

```bash
> Now that tests pass, refactor the code for clarity and efficiency think

Focus on:
- Code clarity
- Removing duplication
- Improving performance
- Better error handling

Keep tests passing throughout refactoring
```

## Advanced TDD Patterns

### Pattern 1: Outside-In TDD

Start with high-level tests, work down to details.

```bash
# Step 1: High-level integration test
> Write integration test for the complete user registration flow

# Step 2: Identify needed components
> What components does this test require? think

# Step 3: Write unit tests for each component
> Write unit tests for email validation
> Write unit tests for password strength checker
> Write unit tests for user creation

# Step 4: Implement each component
> Implement email validation to pass tests
> Implement password checker to pass tests
> Implement user creation to pass tests

# Step 5: Integration test should now pass
> Run the integration test
```

### Pattern 2: Inside-Out TDD

Start with small units, build up to integration.

```bash
# Step 1: Core utility tests
> Write tests for email validation utility

# Step 2: Implement utility
> Implement email validator to pass tests

# Step 3: Component tests using utility
> Write tests for registration form that uses email validator

# Step 4: Implement component
> Implement registration form to pass tests

# Step 5: Integration tests
> Write integration test for complete registration flow

# Step 6: Wire it together
> Connect all components and verify integration tests pass
```

### Pattern 3: TDD with Subagents

Parallel test writing for complex features.

```bash
> Deploy 3 subagents for parallel TDD:
> 1. test-writer: Write unit tests for core logic
> 2. test-writer: Write integration tests for API
> 3. test-writer: Write E2E tests for user flows

# After tests are ready
> Review all tests for coverage and consistency

# Implement sequentially or in parallel
> Implement core logic to pass unit tests
> Implement API endpoints to pass integration tests
> Wire together for E2E tests
```

## Real-World Examples

### Example 1: API Endpoint Development

```bash
# Step 1: Define API contract
> Design the API contract for POST /api/users think

# Step 2: Write tests
> Use test-writer to create tests for POST /api/users endpoint

Tests should cover:
- 201 Created with valid input
- 400 Bad Request with invalid email
- 400 Bad Request with weak password
- 409 Conflict if user exists
- 500 Server Error if database fails

# Step 3: Run tests (should fail)
> Run the API tests

# Step 4: Implement endpoint
> Implement POST /api/users to pass all tests

Follow patterns in ./src/api/auth/route.ts

# Step 5: Verify
> Run tests again - all should pass

# Step 6: Refactor
> Review the implementation and refactor for clarity think
```

### Example 2: Business Logic Component

```bash
# Feature: Shopping cart discount calculator

# Step 1: Test design
> Design test cases for discount calculation think hard

Rules:
- 10% off orders over $100
- 15% off orders over $200
- Additional 5% for members
- Discounts don't stack above 20%
- Free shipping over $50

# Step 2: Write tests
> Write comprehensive tests for discount calculator

Include all rules and edge cases:
- $50 order, non-member: no discount
- $150 order, non-member: 10% off
- $250 order, member: 15% + 5% = 20% off
- $1000 order, member: 20% max
- Boundary cases: $99.99 vs $100.00

# Step 3: Implement
> Implement discount calculator to pass all tests

# Step 4: Refactor
> Refactor discount logic for maintainability think

Make discount rules configurable if possible
```

### Example 3: Refactoring with Test Safety Net

```bash
# You have legacy code that needs refactoring

# Step 1: Add tests for existing behavior
> Use test-writer to create tests that verify current behavior of [legacy function]

Important: Tests should pass with current implementation

# Step 2: Verify tests pass
> Run tests - all should pass with existing code

# Step 3: Refactor
> Refactor [legacy function] using modern patterns think hard

Keep the same external behavior - tests must still pass

# Step 4: Verify tests still pass
> Run tests - should still pass after refactoring

# Step 5: Add tests for edge cases
> Now add tests for edge cases we discovered during refactoring

# Step 6: Update implementation
> Update implementation to handle new edge cases
```

## Common Patterns

### Testing Pyramid

```bash
# Many unit tests (fast, isolated)
> Write unit tests for utility functions
> Write unit tests for components

# Fewer integration tests (slower, test interactions)
> Write integration tests for API layer
> Write integration tests for service layer

# Few E2E tests (slowest, test complete flows)
> Write E2E tests for critical user journeys
```

### Test Organization

```
src/
├── components/
│   ├── UserCard.tsx
│   └── UserCard.test.tsx        # Unit tests
├── api/
│   ├── users/
│   │   ├── route.ts
│   │   └── route.test.ts        # Integration tests
└── e2e/
    └── registration.test.ts      # E2E tests
```

### Test Naming Convention

```typescript
// Pattern: describe what, test specific behavior
describe('UserAuthentication', () => {
  describe('login', () => {
    it('should return token with valid credentials', () => {})
    it('should reject invalid password', () => {})
    it('should lock account after 5 failures', () => {})
  })
})
```

## Tips for Effective TDD

### Do's ✅

1. **Write minimal tests first**
   - Start with simplest test case
   - Add complexity gradually

2. **Keep tests simple**
   - One assertion per test (when possible)
   - Clear test names
   - Obvious what's being tested

3. **Test behavior, not implementation**
```typescript
// Good - tests behavior
it('should calculate total price with tax', () => {
  expect(calculateTotal(100)).toBe(108)
})

// Bad - tests implementation
it('should multiply price by 1.08', () => {
  expect(calculator.multiplier).toBe(1.08)
})
4. **Use thinking levels appropriately**
   - `think hard` for test case design
   - `think` for implementation
   - `ultrathink` for complex business logic

5. **Let tests guide design**
   - Hard to test = probably bad design
   - TDD helps create better APIs

### Don'ts ❌

1. **Don't skip failing tests**
   - Always verify tests fail first
   - Ensures tests are actually testing something

2. **Don't write all tests upfront**
   - Write one test, implement, refactor
   - Repeat cycle

3. **Don't test implementation details**
   - Test public interface
   - Allow internal refactoring

4. **Don't ignore test pain**
   - Difficult tests signal design problems
   - Refactor design, not tests

5. **Don't skip refactoring**
   - Refactor is part of the cycle
   - Technical debt accumulates otherwise

## Measuring Success

### Good Signs ✅

- Tests are easy to write
- Tests are easy to read
- Tests run fast
- Tests catch real bugs
- Confident refactoring
- High code coverage (>80%)

### Warning Signs ⚠️

- Tests are complex
- Tests break frequently with refactoring
- Tests are slow
- Low test coverage
- Fear of refactoring

## Troubleshooting

### Problem: Tests are too slow

```bash
> Analyze test performance and suggest optimizations think hard

Look for:
- Database operations (use mocks or in-memory DB)
- External API calls (mock them)
- Complex setup (simplify or share fixtures)
- Running too many E2E tests (convert to integration tests)
```

### Problem: Tests are brittle

```bash
> Review tests and identify brittleness causes think

Common issues:
- Testing implementation details
- Tight coupling
- Unclear dependencies
- Over-mocking

> Refactor tests to be more resilient
```

### Problem: Don't know what to test

```bash
> Analyze [feature] and suggest test cases ultrathink

Include:
- Core functionality
- Error conditions
- Edge cases
- Integration points
- Performance constraints
```

## Resources

### Related Guides
- [Thinking Levels Guide](../../../guides/claude-code/thinking-levels-guide.md)
- [Subagent Best Practices](../../../guides/claude-code/subagent-best-practices.md)
- [Custom Subagents](../custom-agents/)

### Test-Writer Subagent
See [test-writer.md](../custom-agents/test-writer.md) for specialized test-writing subagent.

---

*TDD with Claude Code: Let tests drive your design, let Claude drive your tests.*
