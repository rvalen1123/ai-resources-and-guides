---
name: subagent-name
description: Brief description of what this subagent does (keep under 100 chars)
tools: file_read, file_write, search_files, search_code, terminal, git_log
---

# Subagent System Prompt

[Write a clear, concise system prompt that defines the subagent's role and behavior]

## Role
[What is this subagent's specialty?]

## Responsibilities
[What tasks should this subagent handle?]

## Guidelines
[How should this subagent approach its work?]

## Constraints
[What should this subagent avoid or be careful about?]

---

## Template Instructions

### YAML Frontmatter (Required)

**name:** kebab-case identifier for the subagent
- Examples: `security-reviewer`, `test-writer`, `api-designer`

**description:** One-line explanation (under 100 characters)
- Good: "Security-focused code reviewer who checks for vulnerabilities"
- Bad: "This subagent reviews code and looks at security issues and finds bugs"

**tools:** Space or comma-separated list of allowed tools
- Available tools:
  - `file_read` - Read files
  - `file_write` - Create/modify files  
  - `search_files` - Search by filename
  - `search_code` - Search file contents
  - `terminal` - Execute commands
  - `git_log` - View git history
- Omit the `tools` field to inherit all available tools (including MCP servers)
- Restrict tools for security: use minimal permissions needed

### System Prompt Guidelines

**Keep it concise:**
- Anthropic recommends under 400 characters total
- Longer prompts can reduce performance
- Be direct and specific

**Define clear scope:**
```markdown
# Good
You review code for security vulnerabilities using OWASP guidelines.
Focus on: SQL injection, XSS, CSRF, auth issues.

# Bad  
You are a really smart security expert who knows everything about 
security and can review any code in any language...
```

**Use actionable language:**
```markdown
# Good
1. Scan for SQL injection vulnerabilities
2. Check input validation
3. Verify authentication flows
4. Flag hardcoded secrets

# Bad
You should look at the code and try to find security issues if there are any.
```

**Include personality (optional):**
```markdown
# Adds clarity and memorability
You are paranoid about security and see vulnerabilities everywhere.
Your catchphrase: "That's not a bug, that's a feature... for attackers."

# But don't overdo it
You are the most amazing, incredible, super-duper security expert...
```

### Example Subagents

#### Minimal (Focused)
```yaml
---
name: quick-tester
description: Writes fast unit tests
tools: file_read, file_write
---

Write unit tests quickly. Focus on happy path and error cases. Use existing test patterns.
```

#### Standard (Balanced)
```yaml
---
name: api-designer
description: Designs RESTful APIs following best practices
tools: file_read, file_write, search_code
---

You design clean, RESTful APIs.

Guidelines:
- Use standard HTTP methods correctly
- Consistent error responses
- Proper status codes
- Clear endpoint naming
- Document with OpenAPI

Reference existing APIs for consistency.
```

#### Detailed (Comprehensive)
```yaml
---
name: database-optimizer
description: Optimizes database queries and schema design
tools: file_read, file_write, search_code, terminal
---

You are a database performance expert specializing in optimization.

## Expertise
- Query optimization and indexing strategies
- Schema design and normalization
- N+1 query detection
- Slow query analysis

## Approach
1. Analyze current queries and schema
2. Identify bottlenecks (missing indexes, poor joins)
3. Suggest specific optimizations with examples
4. Explain trade-offs clearly

## Guidelines
- Always measure before and after
- Consider read vs write patterns
- Balance normalization vs performance
- Recommend specific index types

Reference: Use EXPLAIN ANALYZE for query plans
```

### Testing Your Subagent

1. **Create the file**
   ```bash
   mkdir -p .claude/agents
   cp subagent-template.md .claude/agents/my-subagent.md
   # Edit my-subagent.md
   ```

2. **Test invocation**
   ```bash
   > Use the my-subagent to [task description]
   ```

3. **Evaluate performance**
   - Does it understand its role?
   - Does it follow guidelines?
   - Does it use tools appropriately?
   - Is output quality good?

4. **Iterate**
   - Refine the system prompt
   - Adjust tool permissions
   - Clarify constraints
   - Add examples if needed

### Common Patterns

**Research/Analysis Subagent**
```yaml
tools: file_read, search_files, search_code, git_log
# No write permissions - read-only analysis
```

**Implementation Subagent**
```yaml
tools: file_read, file_write, terminal
# Can create files and run tests
```

**DevOps Subagent**
```yaml
tools: file_read, terminal, git_log
# Focus on execution and history
```

**Full Access Subagent**
```yaml
# Omit tools field entirely
# Inherits all tools including MCP servers
```

### File Location Options

**Project-specific:**
```
your-project/.claude/agents/my-subagent.md
```

**User-global:**
```
~/.config/claude/agents/my-subagent.md
```

**Repository template:**
```
templates/subagents/my-subagent.md
# Copy to project when needed
```

### Best Practices from Anthropic

> "We recommend generating your initial sub agent with Claude and then iterating on it to make it personally yours. This approach gives you the best results - a solid foundation that you can customize to your specific needs."

**Workflow:**
1. Ask Claude to generate a subagent
2. Review and test it
3. Refine based on actual usage
4. Document what works
5. Share with team

**Keep it practical:**
- Start simple, add complexity as needed
- Test with real tasks
- Iterate based on performance
- Don't over-engineer

### Troubleshooting

**Subagent too verbose:**
- Shorten system prompt
- Remove unnecessary personality
- Focus on actionable items

**Subagent not following guidelines:**
- Make guidelines more explicit
- Add specific examples
- Clarify constraints

**Subagent asking for too much context:**
- Reference CLAUDE.md files
- Point to example files
- Include key patterns in prompt

**Tool permission errors:**
- Verify tools list is correct
- Check if tools are available
- Consider adding needed tools

### Advanced: Dynamic Subagents

You can also create subagents on-the-fly:

```bash
> Create a subagent specialized in React performance optimization,
> then use it to analyze our dashboard component

# Claude creates temporary subagent and uses it
```

This is useful for one-off tasks. Save successful patterns as permanent subagent files.

## Resources

- [Official Subagent Documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Subagent Best Practices Guide](../../guides/claude-code/subagent-best-practices.md)
- [Example Subagents](../../examples/claude-code/custom-agents/)
- [Custom Commands](../../examples/claude-code/custom-commands/)

---

**Remember:** Subagents are tools, not personalities. Keep them focused, practical, and effective.

*Remove these instructions when creating your actual subagent.*
