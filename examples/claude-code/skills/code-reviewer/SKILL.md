# Code Reviewer

**Version:** 1.0.0  
**Author:** AI Resources Community  
**Description:** Comprehensive code review with security, performance, style, and best practice checks  
**Created:** 2025-11-05  
**Updated:** 2025-11-05

## Metadata

- **Category:** development | security | quality-assurance
- **Triggers:** code review, PR review, pull request review, security audit, code quality
- **Dependencies:** None (uses Claude's native capabilities)
- **Compatibility:** Claude Code IDE | API | Web | All
- **Estimated Duration:** Medium (5-30 min depending on code size)

## Overview

### Purpose
This skill performs systematic, multi-dimensional code reviews covering security vulnerabilities, performance bottlenecks, code style, maintainability, and best practices. It provides actionable feedback with severity levels and specific suggestions.

### Use Cases
- Pre-merge pull request reviews
- Security audits before deployment
- Code quality checks for legacy code
- Onboarding review standards for teams
- Self-review before committing

### When to Use This Skill
✅ **Use when:**
- Reviewing pull requests or code changes
- Conducting security audits
- Establishing code quality baselines
- Teaching best practices to team members
- Preparing code for production deployment

❌ **Don't use when:**
- Making quick syntax fixes (use linter instead)
- Reviewing auto-generated code (unless for security)
- Initial prototyping phase (premature optimization)

## Instructions

### Prerequisites

**Required:**
- Code to review (files, diff, or PR)
- Understanding of project context

**Optional:**
- Project coding standards document
- Security requirements
- Performance benchmarks

### Workflow Steps

#### 1. Context Gathering
**Objective:** Understand the code's purpose and environment

**Actions:**
- Review the code changes or full codebase
- Identify programming language(s) and framework(s)
- Determine the type of application (web, API, CLI, etc.)
- Note any existing patterns or conventions
- Check for related tests

**Output:** Context summary including language, framework, and purpose

**Validation:** Confirm understanding with user if unclear

#### 2. Security Analysis
**Objective:** Identify security vulnerabilities and risks

**Actions:**
- Check for SQL injection vulnerabilities
- Verify input validation and sanitization
- Review authentication and authorization logic
- Identify exposed secrets or credentials
- Check for XSS, CSRF, and other OWASP Top 10 issues
- Verify secure data handling (encryption, hashing)
- Review dependency security (known CVEs)
- Check error handling (no sensitive info leakage)

**Output:** List of security issues with severity (Critical, High, Medium, Low)

**Validation:** Each issue includes code location and remediation steps

#### 3. Performance Analysis
**Objective:** Identify performance bottlenecks and inefficiencies

**Actions:**
- Check algorithm complexity (O(n²) or worse)
- Identify N+1 query problems
- Review database indexing needs
- Check for unnecessary loops or computations
- Identify memory leaks or excessive allocations
- Review caching opportunities
- Check for blocking operations in async code
- Identify resource cleanup issues

**Output:** List of performance concerns with impact assessment

**Validation:** Include before/after complexity or estimated improvement

#### 4. Code Style and Maintainability
**Objective:** Ensure code is clean, readable, and maintainable

**Actions:**
- Check naming conventions (variables, functions, classes)
- Review function/method length and complexity
- Verify code organization and structure
- Check for code duplication (DRY principle)
- Review comment quality (not too few, not too many)
- Verify consistent formatting
- Check for magic numbers and strings
- Review error messages for clarity

**Output:** List of style and maintainability issues

**Validation:** Suggestions improve readability and future modifications

#### 5. Best Practices Check
**Objective:** Ensure adherence to language and framework best practices

**Actions:**
- Verify SOLID principles application
- Check design pattern usage appropriateness
- Review error handling completeness
- Verify logging adequacy
- Check test coverage and quality
- Review API design (if applicable)
- Verify configuration management
- Check documentation completeness

**Output:** List of best practice violations or opportunities

**Validation:** Recommendations are specific and actionable

#### 6. Report Generation
**Objective:** Compile findings into actionable review

**Actions:**
- Categorize all findings by type and severity
- Prioritize issues (must-fix vs. nice-to-have)
- Provide specific code suggestions or examples
- Include positive observations (what's done well)
- Create summary with metrics
- Generate action items

**Output:** Comprehensive review report

**Validation:** Report is clear, actionable, and constructive

### Error Handling

**Common Issues:**

**Issue:** Code context is insufficient
- **Cause:** Only partial code provided without surrounding context
- **Solution:** Request additional files or context; make assumptions explicit

**Issue:** Language-specific knowledge gap
- **Cause:** Uncommon language or framework
- **Solution:** Focus on universal principles; note specific uncertainty areas

**Issue:** Conflicting standards
- **Cause:** Code uses different conventions than typical standards
- **Solution:** Identify project's existing patterns; suggest consistency

### Quality Checks

**Before completion, verify:**
- [ ] All review categories covered (security, performance, style, best practices)
- [ ] Each issue includes severity level
- [ ] Specific code locations referenced
- [ ] Actionable remediation steps provided
- [ ] Positive feedback included (balanced review)
- [ ] Summary includes metrics (# issues by category/severity)

## Examples

### Example 1: API Endpoint Review

**Context:** Reviewing a new REST API endpoint for user registration

**Input:**
```python
@app.route('/register', methods=['POST'])
def register():
    username = request.form['username']
    password = request.form['password']
    
    user = User(username=username, password=password)
    db.session.add(user)
    db.session.commit()
    
    return jsonify({'message': 'User created'})
```

**Process:**
```bash
> Review this registration endpoint for security and best practices
```

**Output:**
```markdown
## Security Issues (Critical)
1. **No password hashing** (Line 6)
   - Severity: CRITICAL
   - Issue: Password stored in plaintext
   - Fix: Use bcrypt/scrypt to hash password before storage
   
2. **No input validation** (Lines 4-5)
   - Severity: HIGH
   - Issue: Accepting raw input without validation
   - Fix: Validate username format, password strength
   
3. **SQL injection risk** (Lines 7-8)
   - Severity: HIGH
   - Issue: Using ORM but no input sanitization
   - Fix: Add input validation and sanitization

## Best Practices (High Priority)
1. **No error handling** (All)
   - Missing try-except blocks
   - No handling for duplicate usernames
   - Fix: Add proper exception handling

2. **No authentication token returned** (Line 10)
   - User created but no way to authenticate
   - Fix: Generate and return JWT or session token

## Positive Observations
✓ Using ORM instead of raw SQL
✓ Using POST method for data submission
```

**Result:** Identified 5 critical security and best practice issues with specific remediation steps

### Example 2: Performance Review

**Context:** Reviewing data processing function with performance concerns

**Input:**
```javascript
function processUsers(users) {
  const results = [];
  for (let user of users) {
    const posts = db.query('SELECT * FROM posts WHERE user_id = ?', user.id);
    const comments = db.query('SELECT * FROM comments WHERE user_id = ?', user.id);
    results.push({
      user: user,
      posts: posts,
      comments: comments
    });
  }
  return results;
}
```

**Process:**
```bash
> Analyze this function for performance issues
```

**Output:**
```markdown
## Performance Issues

1. **N+1 Query Problem** (Lines 4-5) - CRITICAL
   - Severity: CRITICAL
   - Impact: 2N+1 database queries for N users
   - Example: 1000 users = 2001 queries = ~20-30 seconds
   - Fix: Use JOIN or batch queries
   
   ```javascript
   // Better approach:
   function processUsers(users) {
     const userIds = users.map(u => u.id);
     const posts = db.query(
       'SELECT * FROM posts WHERE user_id IN (?)',
       userIds
     );
     const comments = db.query(
       'SELECT * FROM comments WHERE user_id IN (?)',
       userIds
     );
     
     // Group by user_id and combine
     return users.map(user => ({
       user,
       posts: posts.filter(p => p.user_id === user.id),
       comments: comments.filter(c => c.user_id === user.id)
     }));
   }
   ```
   
2. **No pagination** (All)
   - Severity: HIGH
   - Risk: Memory exhaustion with large datasets
   - Fix: Add offset/limit parameters

3. **Blocking synchronous queries** (Lines 4-5)
   - Severity: MEDIUM
   - Issue: No async/await usage
   - Fix: Use async queries for better throughput
```

**Result:** Identified N+1 query problem reducing complexity from O(n²) to O(n)

## Configuration

### Customization Options

**Parameter:** `review_depth`
- **Description:** How thorough the review should be
- **Default:** `comprehensive`
- **Options:** `quick | standard | comprehensive | security-focused`
- **Example:** "Do a quick review focusing on critical issues only"

**Parameter:** `include_positive`
- **Description:** Whether to include positive observations
- **Default:** `true`
- **Options:** `true | false`
- **Example:** "Review this code but skip positive feedback"

**Parameter:** `severity_threshold`
- **Description:** Minimum severity level to report
- **Default:** `low`
- **Options:** `critical | high | medium | low`
- **Example:** "Only show critical and high severity issues"

### Environment Variables

```bash
# Optional: Customize review standards
CODE_REVIEW_STYLE_GUIDE="./docs/style-guide.md"
CODE_REVIEW_SECURITY_RULES="./security-policy.md"
```

## Resources

### Included Files

This is a lightweight skill using Claude's native capabilities - no additional files required.

### External Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Security vulnerabilities
- [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) - Code quality principles
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) - Algorithm complexity

## Advanced Usage

### Combining with Other Skills

This skill works well with:
- **Test Writer** - Review first, then generate tests for identified issues
- **Security Auditor** - Deep dive into security findings
- **Performance Optimizer** - Implement performance recommendations

### Integration Patterns

**Pattern 1: Pre-Commit Hook**
```bash
# Review changes before committing
> Review my uncommitted changes using code-reviewer skill
```

**Pattern 2: PR Review Automation**
```bash
# In CI/CD pipeline
> Review PR #123 focusing on security and performance
```

**Pattern 3: Team Standards Enforcement**
```bash
# With custom style guide
> Review using our style guide at docs/standards.md
```

### Performance Optimization

**Tips for faster execution:**
- Review smaller chunks for faster feedback
- Use `quick` mode for initial pass
- Focus on changed files only in PRs
- Set severity threshold to reduce noise

## Testing

### Test Cases

**Test 1: Security Vulnerability Detection**
- **Setup:** Code with SQL injection vulnerability
- **Execute:** Run code-reviewer skill
- **Expected:** Identifies SQL injection as CRITICAL
- **Verify:** Includes specific remediation steps

**Test 2: Performance Issue Detection**
- **Setup:** Code with N+1 query problem
- **Execute:** Run code-reviewer skill
- **Expected:** Identifies N+1 issue with complexity analysis
- **Verify:** Provides optimized code example

**Test 3: Balanced Feedback**
- **Setup:** Mix of good and bad code
- **Execute:** Run code-reviewer skill
- **Expected:** Lists both issues and positive observations
- **Verify:** Report is constructive, not just critical

## Changelog

### Version 1.0.0 (2025-11-05)
- Initial release
- Comprehensive review covering security, performance, style, best practices
- Multi-language support
- Configurable review depth and severity thresholds

## Contributing

**Improvements welcome!**

If you enhance this skill:
1. Add language-specific checks
2. Enhance framework-specific patterns
3. Add more example reviews
4. Update severity guidelines

## License

MIT License - Free to use and modify

## Support

**Questions or Issues?**
- Open an issue with tag `skill:code-reviewer`
- Include code sample and unexpected behavior
- Specify Claude Code version

## Related Skills

- [Security Reviewer](../../custom-agents/security-reviewer.md) - Deep security analysis
- [Performance Optimizer](../../custom-agents/performance-optimizer.md) - Performance improvements
- [Test Writer](../../custom-agents/test-writer.md) - Generate tests for reviewed code

---

**Credits:** Inspired by industry standard code review practices and OWASP security guidelines.

*This skill is part of the [AI Resources and Guides](https://github.com/rvalen1123/ai-resources-and-guides) repository.*
