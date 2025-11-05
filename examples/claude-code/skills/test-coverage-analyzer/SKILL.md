# Test Coverage Analyzer

**Version:** 1.0.0  
**Author:** AI Resources Community  
**Description:** Analyze test coverage, identify gaps, and generate missing tests for comprehensive code quality  
**Created:** 2025-11-05  
**Updated:** 2025-11-05

## Metadata

- **Category:** testing | quality-assurance | development
- **Triggers:** test coverage, coverage analysis, missing tests, test gaps, coverage report, test quality
- **Dependencies:** None (uses Claude's native capabilities)
- **Compatibility:** Claude Code IDE | API | Web | All
- **Estimated Duration:** Medium (10-30 min depending on codebase size)

## Overview

### Purpose
This skill analyzes existing test coverage, identifies untested code paths, assesses test quality, and generates specific recommendations or test implementations to achieve comprehensive coverage. Helps teams improve code quality and catch bugs before production.

### Use Cases
- Auditing test coverage before releases
- Identifying critical untested code paths
- Improving test suite quality
- Meeting coverage requirements (80%, 90%, etc.)
- Code review with testing focus
- Technical debt reduction

### When to Use This Skill
✅ **Use when:**
- Assessing test coverage for a project
- Preparing for production deployment
- Code has tests but coverage is unclear
- Implementing TDD and need baseline
- Reviewing pull requests with new code

❌ **Don't use when:**
- No code exists yet (use test-first development)
- Simple scripts with no business logic
- Prototype/POC phase (premature testing)

## Instructions

### Prerequisites

**Required:**
- Source code files to analyze
- Existing test files (if any)

**Optional:**
- Coverage reports (from jest, pytest, coverage.py, etc.)
- Test framework configuration
- Critical code paths list

### Workflow Steps

#### 1. Test Discovery
**Objective:** Identify all existing tests and test framework

**Actions:**
- Locate test files (test_*.py, *.spec.js, *_test.go, etc.)
- Identify test framework (Jest, Pytest, JUnit, etc.)
- Count total tests and test files
- Check test organization structure
- Identify test types (unit, integration, E2E)
- Note test naming conventions

**Output:** Test inventory with framework and organization details

**Validation:** All test files are catalogued

#### 2. Source Code Analysis
**Objective:** Understand code structure and critical paths

**Actions:**
- Identify all source files
- Map functions/methods/classes
- Identify critical business logic
- Note error handling paths
- Identify edge cases
- Map dependencies and interactions
- Calculate cyclomatic complexity (high = needs more tests)

**Output:** Complete code structure map with complexity metrics

**Validation:** All testable code units identified

#### 3. Coverage Mapping
**Objective:** Map tests to source code

**Actions:**
- Match test files to source files
- Identify which functions have tests
- Calculate line coverage percentage
- Calculate branch coverage percentage
- Identify completely untested files
- Note partially tested functions
- Map test scenarios to code paths

**Output:** Coverage matrix showing tested vs. untested code

**Validation:** Clear visualization of coverage gaps

#### 4. Gap Analysis
**Objective:** Identify specific untested scenarios

**Actions:**
- List untested functions/methods
- Identify untested branches (if/else, switch)
- Find untested error paths
- Note missing edge case tests
- Identify integration gaps
- Find untested critical paths
- Calculate coverage percentage by priority

**Output:** Prioritized list of coverage gaps

**Validation:** Each gap includes specific code location and scenario

#### 5. Test Quality Assessment
**Objective:** Evaluate existing test effectiveness

**Actions:**
- Check for assertion quality (specific vs. generic)
- Verify test isolation (no shared state)
- Review test data (realistic vs. trivial)
- Check error scenario coverage
- Evaluate test maintainability
- Verify test performance (fast vs. slow)
- Check for flaky tests indicators

**Output:** Test quality report with improvement suggestions

**Validation:** Actionable recommendations for each issue

#### 6. Recommendation Generation
**Objective:** Provide specific testing improvements

**Actions:**
- Prioritize gaps by criticality (high/medium/low)
- Generate test case descriptions
- Create test code examples for critical gaps
- Suggest test refactoring for quality issues
- Recommend coverage targets
- Provide implementation plan

**Output:** Detailed testing improvement plan

**Validation:** Recommendations are specific and achievable

### Error Handling

**Common Issues:**

**Issue:** No coverage data available
- **Cause:** Coverage tool not configured
- **Solution:** Analyze code statically; recommend coverage tool setup

**Issue:** Tests in non-standard locations
- **Cause:** Custom project structure
- **Solution:** Request test file locations; adapt analysis

**Issue:** Mixed testing frameworks
- **Cause:** Legacy or migrated codebase
- **Solution:** Analyze per framework; note inconsistencies

### Quality Checks

**Before completion, verify:**
- [ ] All source files analyzed
- [ ] All test files identified
- [ ] Coverage percentages calculated
- [ ] Gaps prioritized by criticality
- [ ] Specific test recommendations provided
- [ ] Test quality assessed
- [ ] Implementation examples included

## Examples

### Example 1: Python Function Coverage Analysis

**Context:** Analyzing a Python user authentication module

**Input:**
```python
# auth.py
def authenticate_user(username, password):
    if not username or not password:
        raise ValueError("Username and password required")
    
    user = database.get_user(username)
    if not user:
        return None
    
    if not verify_password(password, user.password_hash):
        log_failed_attempt(username)
        return None
    
    if user.is_locked:
        raise AccountLockedException(f"Account {username} is locked")
    
    return user

# test_auth.py
def test_authenticate_valid_user():
    user = authenticate_user("john", "password123")
    assert user is not None
    assert user.username == "john"
```

**Process:**
```bash
> Analyze test coverage for auth.py and identify missing tests
```

**Output:**
```markdown
## Coverage Analysis: auth.py

### Current Coverage
- **Line Coverage:** 50% (7/14 lines)
- **Branch Coverage:** 20% (1/5 branches)
- **Function Coverage:** 100% (1/1 function)

### Tested Scenarios ✓
1. ✅ Valid user authentication (happy path)

### Missing Test Coverage (HIGH PRIORITY)

#### 1. Empty Username/Password Validation ⚠️
**Priority:** HIGH
**Code:** Lines 3-4
**Scenario:** `ValueError` when username or password is empty

**Missing Test:**
```python
def test_authenticate_empty_username():
    with pytest.raises(ValueError, match="Username and password required"):
        authenticate_user("", "password123")

def test_authenticate_empty_password():
    with pytest.raises(ValueError, match="Username and password required"):
        authenticate_user("john", "")

def test_authenticate_both_empty():
    with pytest.raises(ValueError, match="Username and password required"):
        authenticate_user("", "")
```

#### 2. User Not Found Path ⚠️
**Priority:** HIGH
**Code:** Lines 6-8
**Scenario:** Returns `None` when user doesn't exist

**Missing Test:**
```python
def test_authenticate_user_not_found():
    user = authenticate_user("nonexistent", "password123")
    assert user is None
```

#### 3. Invalid Password Path ⚠️
**Priority:** HIGH
**Code:** Lines 10-12
**Scenario:** Returns `None` and logs failed attempt

**Missing Test:**
```python
def test_authenticate_invalid_password(mock_log):
    user = authenticate_user("john", "wrongpassword")
    assert user is None
    mock_log.assert_called_once_with("john")
```

#### 4. Locked Account Exception ⚠️
**Priority:** CRITICAL
**Code:** Lines 14-15
**Scenario:** `AccountLockedException` for locked accounts

**Missing Test:**
```python
def test_authenticate_locked_account():
    # Setup: Create locked user
    locked_user = create_user("locked_user", locked=True)
    
    with pytest.raises(AccountLockedException, match="Account locked_user is locked"):
        authenticate_user("locked_user", "correct_password")
```

### Test Quality Issues

#### Issue 1: No Negative Test Cases
**Current:** Only happy path tested
**Impact:** Bugs in error handling won't be caught
**Recommendation:** Add all error path tests above

#### Issue 2: Missing Mock Verification
**Current:** Database and logging calls not mocked/verified
**Impact:** Tests depend on real database, can't verify logging
**Recommendation:** 
```python
@patch('auth.database.get_user')
@patch('auth.log_failed_attempt')
def test_authenticate_invalid_password(mock_log, mock_get_user):
    mock_get_user.return_value = User(username="john", ...)
    # ... test code ...
```

#### Issue 3: No Edge Cases
**Missing:**
- SQL injection attempts in username
- Very long passwords
- Special characters in username
- Null values vs empty strings

### Coverage Target

**Recommended:** 90% line coverage, 80% branch coverage

**Implementation Plan:**
1. Add 4 critical missing tests (Day 1) - reaches 85% coverage
2. Add edge case tests (Day 2) - reaches 90% coverage
3. Refactor with proper mocking (Day 3) - improves quality
4. Add integration tests (Day 4) - complete coverage

**Estimated Effort:** 4-6 hours
```

**Result:** Identified 4 critical untested scenarios with specific test implementations

### Example 2: JavaScript Component Coverage Analysis

**Context:** React component with partial test coverage

**Input:**
```javascript
// UserProfile.jsx
function UserProfile({ userId, onUpdate }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetchUser(userId)
      .then(data => {
        setUser(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err.message);
        setLoading(false);
      });
  }, [userId]);

  if (loading) return <Spinner />;
  if (error) return <ErrorMessage message={error} />;
  if (!user) return <NotFound />;

  return (
    <div>
      <h1>{user.name}</h1>
      <button onClick={() => onUpdate(user)}>Edit</button>
    </div>
  );
}

// UserProfile.test.jsx
test('renders user name', async () => {
  mockFetch({ name: 'John Doe' });
  render(<UserProfile userId={1} />);
  expect(await screen.findByText('John Doe')).toBeInTheDocument();
});
```

**Process:**
```bash
> Analyze test coverage for UserProfile component
```

**Output:**
```markdown
## Coverage Analysis: UserProfile.jsx

### Current Coverage
- **Line Coverage:** 45% (9/20 lines)
- **Branch Coverage:** 25% (1/4 branches)
- **Component States:** 25% (1/4 states tested)

### Tested Scenarios ✓
1. ✅ Successful user fetch and render

### Missing Test Coverage

#### 1. Loading State ⚠️ CRITICAL
**Priority:** HIGH
**Code:** Line 17
**Scenario:** Spinner displayed while fetching

**Missing Test:**
```javascript
test('shows loading spinner initially', () => {
  mockFetchPending();
  render(<UserProfile userId={1} />);
  expect(screen.getByTestId('spinner')).toBeInTheDocument();
});
```

#### 2. Error State ⚠️ CRITICAL
**Priority:** HIGH
**Code:** Line 18
**Scenario:** Error message displayed on fetch failure

**Missing Test:**
```javascript
test('shows error message on fetch failure', async () => {
  mockFetchError(new Error('Network error'));
  render(<UserProfile userId={1} />);
  
  const errorMsg = await screen.findByText(/Network error/i);
  expect(errorMsg).toBeInTheDocument();
});
```

#### 3. User Not Found State ⚠️
**Priority:** MEDIUM
**Code:** Line 19
**Scenario:** NotFound component for null user

**Missing Test:**
```javascript
test('shows not found when user is null', async () => {
  mockFetch(null);
  render(<UserProfile userId={999} />);
  
  expect(await screen.findByText(/not found/i)).toBeInTheDocument();
});
```

#### 4. Edit Button Click ⚠️
**Priority:** HIGH
**Code:** Line 24
**Scenario:** onUpdate callback called with user data

**Missing Test:**
```javascript
test('calls onUpdate when edit button clicked', async () => {
  const mockOnUpdate = jest.fn();
  const userData = { id: 1, name: 'John Doe' };
  mockFetch(userData);
  
  render(<UserProfile userId={1} onUpdate={mockOnUpdate} />);
  
  const editButton = await screen.findByText('Edit');
  fireEvent.click(editButton);
  
  expect(mockOnUpdate).toHaveBeenCalledWith(userData);
});
```

#### 5. userId Change Effect ⚠️
**Priority:** MEDIUM
**Code:** Line 7 (useEffect dependency)
**Scenario:** Refetch when userId prop changes

**Missing Test:**
```javascript
test('refetches user when userId changes', async () => {
  const { rerender } = render(<UserProfile userId={1} />);
  expect(await screen.findByText('John Doe')).toBeInTheDocument();
  
  mockFetch({ name: 'Jane Smith' });
  rerender(<UserProfile userId={2} />);
  
  expect(await screen.findByText('Jane Smith')).toBeInTheDocument();
});
```

### Test Quality Assessment

#### Strength ✓
- Uses modern testing patterns (findBy for async)
- Tests user-visible behavior

#### Issues to Address

1. **No Loading State Testing**
   - Risk: Loading UX bugs undetected
   - Fix: Add loading state test

2. **No Error Handling Tests**
   - Risk: Poor error UX unnoticed
   - Fix: Add error state and edge case tests

3. **Incomplete Interaction Testing**
   - Risk: Button handlers can break silently
   - Fix: Test all interactive elements

4. **Missing Accessibility Tests**
   - Risk: A11y regressions
   - Recommendation: Add `toHaveAccessibleName` checks

### Coverage Goal

**Target:** 85% line coverage, 100% critical path coverage

**Implementation Order:**
1. ⚠️ CRITICAL: Add loading and error state tests (30 min)
2. ⚠️ HIGH: Add button interaction test (15 min)
3. 📊 MEDIUM: Add userId change test (20 min)
4. 📊 MEDIUM: Add not found test (10 min)
5. ✨ NICE: Add accessibility tests (30 min)

**Total Effort:** ~2 hours to reach 85% coverage

### Automation Recommendation

Add to CI/CD:
```json
// jest.config.js
{
  "coverageThreshold": {
    "global": {
      "branches": 80,
      "functions": 80,
      "lines": 85,
      "statements": 85
    }
  }
}
```
```

**Result:** Identified 5 missing test scenarios, prioritized by criticality, with time estimates

## Configuration

### Customization Options

**Parameter:** `coverage_target`
- **Description:** Desired coverage percentage
- **Default:** `80`
- **Options:** Any number 0-100
- **Example:** "Analyze coverage and aim for 90%"

**Parameter:** `priority_focus`
- **Description:** What to prioritize in analysis
- **Default:** `all`
- **Options:** `critical-paths | error-handling | edge-cases | all`
- **Example:** "Focus on critical business logic paths"

**Parameter:** `include_tests`
- **Description:** Whether to generate test code examples
- **Default:** `true`
- **Options:** `true | false`
- **Example:** "Just show coverage gaps, don't generate tests"

**Parameter:** `test_framework`
- **Description:** Preferred test framework for generated tests
- **Default:** `auto-detect`
- **Options:** `jest | pytest | junit | mocha | rspec | auto-detect`
- **Example:** "Generate tests using pytest"

## Resources

### External Resources

- [Code Coverage Best Practices](https://martinfowler.com/bliki/TestCoverage.html)
- [Jest Coverage Reports](https://jestjs.io/docs/cli#--coverageboolean)
- [Pytest Coverage](https://pytest-cov.readthedocs.io/)
- [Istanbul (JS Coverage)](https://istanbul.js.org/)

## Advanced Usage

### Combining with Other Skills

This skill works well with:
- **Test Writer** - Implement the recommended tests
- **Code Reviewer** - Include coverage analysis in reviews
- **CI/CD Pipeline** - Automate coverage checks

### Integration Patterns

**Pattern 1: Pre-Release Coverage Audit**
```bash
> Analyze test coverage for all files in src/ directory
> Identify gaps above 80% criticality threshold
```

**Pattern 2: PR Coverage Requirements**
```bash
> Check test coverage for changed files in this PR
> Generate missing tests for uncovered lines
```

**Pattern 3: Technical Debt Planning**
```bash
> Create coverage improvement roadmap for legacy/ directory
> Prioritize by file criticality and current coverage
```

## Testing

### Test Cases

**Test 1: Gap Identification**
- **Setup:** Code file with 60% coverage
- **Execute:** Run coverage analyzer
- **Expected:** Identifies specific untested lines/branches
- **Verify:** Each gap includes code location

**Test 2: Test Generation**
- **Setup:** Untested error handling code
- **Execute:** Request test generation
- **Expected:** Syntactically correct test code
- **Verify:** Tests can be added and run

**Test 3: Quality Assessment**
- **Setup:** Tests with weak assertions
- **Execute:** Analyze test quality
- **Expected:** Identifies assertion weaknesses
- **Verify:** Includes improvement suggestions

## Changelog

### Version 1.0.0 (2025-11-05)
- Initial release
- Line and branch coverage analysis
- Gap identification with priority
- Test quality assessment
- Test code generation for gaps
- Multiple framework support

## Contributing

Enhancements welcome:
1. Add mutation testing analysis
2. Support more test frameworks
3. Add visual coverage reports
4. Enhance quality assessment criteria

## License

MIT License - Free to use and modify

## Support

**Questions or Issues?**
- Open an issue with tag `skill:test-coverage-analyzer`
- Include test framework and language
- Share coverage report if available

## Related Skills

- [Test Writer](../../custom-agents/test-writer.md) - Generate complete test suites
- [Code Reviewer](../code-reviewer/) - Includes test coverage checks

---

**Credits:** Based on industry testing best practices and coverage analysis patterns.

*This skill is part of the [AI Resources and Guides](https://github.com/rvalen1123/ai-resources-and-guides) repository.*
