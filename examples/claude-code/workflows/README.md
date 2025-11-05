# Claude Code Workflow Examples

> **Proven patterns for common development workflows**

Ready-to-use workflow patterns that combine Claude Code's features for maximum productivity.

## Available Workflows

### 🔄 Test-Driven Development (TDD)
**Pattern:** Write tests first, implement to pass
```bash
> Write comprehensive tests for a user authentication system think hard
> Review the tests
> Implement the authentication system to pass these tests
> Run tests and fix any failures
```

**Benefits:**
- Better test coverage
- Clear requirements
- Fewer bugs
- Refactoring confidence

### 🐛 Debug Squad Pattern
**Pattern:** Multiple subagents attack problem from different angles
```bash
> Deploy 3 subagents to debug this performance issue:
> 1. Bug Hunter - Find the root cause
> 2. Log Analyst - Analyze error logs
> 3. Solution Architect - Propose fixes
```

**When to use:**
- Complex bugs with unclear cause
- Performance issues
- Intermittent problems
- System-wide issues

### 🔍 Code Exploration Workflow
**Pattern:** Parallel subagents explore large codebase
```bash
> Use 4 parallel subagents to explore this codebase:
> 1. Analyze backend architecture
> 2. Review frontend patterns
> 3. Check testing coverage
> 4. Examine database schema
> Then summarize findings
```

**Best for:**
- New codebases
- Legacy systems
- Pre-refactoring analysis
- Documentation generation

### 🏗️ Architecture Design Flow
**Pattern:** Progressive refinement with thinking levels
```bash
# Step 1: High-level design
> Design a microservices architecture for this e-commerce platform ultrathink

# Step 2: Detailed component design
> Design the user service in detail think hard

# Step 3: Implementation
> Implement the user service with tests

# Step 4: Review
> Use security-reviewer subagent to audit the implementation
```

**Phases:**
1. Architecture (ultrathink)
2. Component design (think hard)
3. Implementation (think)
4. Review (subagents)

### 🔒 Security Audit Workflow
**Pattern:** Progressive security review
```bash
# Step 1: Automated scan
> Use security-reviewer subagent to scan for common vulnerabilities

# Step 2: Deep dive
> Analyze authentication flow for security issues ultrathink

# Step 3: Specific checks
> Check for SQL injection vulnerabilities
> Verify CSRF protection
> Review input validation

# Step 4: Report
> Summarize findings and prioritize by severity
```

### ⚡ Performance Optimization Flow
**Pattern:** Measure, analyze, optimize, verify
```bash
# Step 1: Baseline
> Profile the application and identify bottlenecks think hard

# Step 2: Analysis
> Use performance-optimizer subagent to analyze the slow queries

# Step 3: Optimize
> Implement the suggested optimizations

# Step 4: Verify
> Write performance tests to prevent regression
```

### 🔄 Refactoring Workflow
**Pattern:** Safe, incremental refactoring
```bash
# Step 1: Understand
> Analyze this legacy code and explain its purpose think

# Step 2: Test coverage
> Use test-writer subagent to add tests for existing behavior

# Step 3: Refactor
> Refactor the code using modern patterns

# Step 4: Verify
> Run tests to ensure behavior unchanged
```

**Safety steps:**
1. Add tests before refactoring
2. Small, incremental changes
3. Run tests frequently
4. Keep original behavior

### 📝 Documentation Generation
**Pattern:** Comprehensive docs from code
```bash
# Step 1: Architecture docs
> Generate architecture documentation from the codebase ultrathink

# Step 2: API docs
> Document all API endpoints with examples

# Step 3: Code comments
> Add comprehensive comments to complex functions

# Step 4: README
> Update README with getting started guide
```

### 🚀 Feature Development End-to-End
**Pattern:** Complete feature from spec to deployment
```bash
# Step 1: Planning
> Break down this feature into implementation tasks think hard

# Step 2: TDD approach
> Write tests for the new feature
> Use test-writer subagent for comprehensive coverage

# Step 3: Implementation
> Implement feature to pass tests

# Step 4: Security review
> Use security-reviewer to audit new code

# Step 5: Documentation
> Update API docs and README

# Step 6: Integration
> Create PR with comprehensive description
```

### 🔄 Migration Workflow
**Pattern:** Safe, tested migration
```bash
# Step 1: Analysis
> Analyze the current implementation ultrathink
> Identify migration risks and challenges

# Step 2: Strategy
> Design migration strategy with rollback plan think hard

# Step 3: Parallel implementation
> Implement new system alongside old

# Step 4: Testing
> Create comprehensive tests comparing old vs new behavior

# Step 5: Gradual rollout
> Implement feature flags for gradual migration

# Step 6: Verification
> Monitor and verify new system performance
```

## Workflow Combination Patterns

### Pattern: Think + Subagent
```bash
> ultrathink a solution approach
# Get comprehensive plan
> Use [specialized-subagent] to implement the plan
```

### Pattern: Parallel + Sequential
```bash
# Parallel: Independent exploration
> Use 3 subagents to analyze different modules in parallel

# Sequential: Dependent implementation  
> Based on analysis, implement Module A
> Then implement Module B that depends on A
> Finally integrate both modules
```

### Pattern: Iterative Refinement
```bash
# Iteration 1: Quick prototype
> Create a basic implementation think

# Iteration 2: Enhance
> Add error handling and validation think hard

# Iteration 3: Polish
> Optimize performance and add tests

# Iteration 4: Production-ready
> Use security-reviewer and add monitoring ultrathink
```

## Custom Workflow Creation

### Define Your Workflow

1. **Identify the pattern** you use repeatedly
2. **Break it into steps** with clear transitions
3. **Choose appropriate thinking levels** per step
4. **Select subagents** for specialized tasks
5. **Document** the workflow

### Create a Custom Command

Save to `.claude/commands/your-workflow.md`:

```markdown
---
name: your-workflow
description: Description of what this workflow does
---

# Your Workflow Name

[Step-by-step instructions]

Usage: `/your-workflow [arguments]`
```

### Example: API Development Workflow

`.claude/commands/api-dev.md`:
```markdown
---
name: api-dev
description: Complete API endpoint development workflow
---

# API Development Workflow

Implements a new API endpoint with tests, docs, and security review.

## Steps

1. Design API contract think hard
   - Endpoint path and method
   - Request/response schemas
   - Error responses
   - Rate limiting

2. Write tests first (TDD)
   - Use test-writer subagent
   - Happy path tests
   - Error case tests
   - Edge cases

3. Implement endpoint
   - Follow existing patterns
   - Input validation
   - Error handling
   - Logging

4. Security review
   - Use security-reviewer subagent
   - Check authentication
   - Verify authorization
   - Input sanitization

5. Documentation
   - Add OpenAPI spec
   - Update API docs
   - Add usage examples

Usage: `/api-dev "endpoint description"`
```

## Workflow Tips

### Efficiency
- ✅ Use thinking levels appropriately (don't always ultrathink)
- ✅ Parallel subagents for independent tasks
- ✅ Sequential for dependent tasks
- ✅ Clear handoffs between steps

### Quality
- ✅ Include verification steps
- ✅ Test throughout the process
- ✅ Security review for production code
- ✅ Documentation as you go

### Cost Management
- ⚠️ Monitor token usage with multiple subagents
- ⚠️ Reserve ultrathink for truly complex steps
- ⚠️ Terminate subagents when no longer needed
- ⚠️ Use casual subagents for simple tasks

## Real-World Workflow Examples

### Startup MVP Development
```bash
> ultrathink the MVP architecture with scalability in mind
> Break into user stories
> For each story:
>   - Use test-writer for tests
>   - Implement feature
>   - Use security-reviewer
>   - Update docs
> Integration testing
> Deployment planning
```

### Enterprise Integration
```bash
> Analyze existing system architecture ultrathink
> Identify integration points think hard
> Design integration layer with error handling
> Use 2 subagents:
>   - One for legacy system interaction
>   - One for new system development
> Comprehensive testing including failure scenarios
> Gradual rollout strategy
```

### Open Source Contribution
```bash
> Read project CONTRIBUTING.md and understand conventions
> Explore relevant code sections think
> Implement feature following project patterns
> Write tests matching existing test style
> Update documentation
> Create PR with detailed description
```

## Related Resources

- [Subagent Best Practices](../../../guides/claude-code/subagent-best-practices.md)
- [Thinking Levels Guide](../../../guides/claude-code/thinking-levels-guide.md)
- [Custom Commands](../custom-commands/)
- [Custom Subagents](../custom-agents/)

---

*Workflows are patterns, not rigid rules. Adapt them to your needs and context.*
