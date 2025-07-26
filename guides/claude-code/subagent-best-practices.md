# Claude Code Subagent Best Practices: From Accidental Expert to Intentional Architect

*For those who've been accidentally doing advanced multi-agent orchestration by just asking nicely*

> **Sources:** This guide synthesizes best practices from [Anthropic's official Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents), [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices), and community findings from experienced practitioners.

## The Two Paths to Subagent Enlightenment

### Path 1: The "Wait, That Was Advanced?" Method (Casual Subagents)
You've probably been doing this without knowing it was a "feature":

```bash
# What you've been saying:
> "Hey Claude, split this into 4 parallel tasks"

# What Claude Code actually does:
# Task(Analyzing backend) 
# Task(Reviewing frontend)
# Task(Checking tests)
# Task(Optimizing database)
```

**Best Practices for Casual Subagents:**
- Just ask for what you want naturally - "use 3 parallel tasks to explore this codebase"
- Max parallelism is 10 tasks running simultaneously¹ (Claude will queue additional requests)
- Don't specify parallelism level if you want dynamic queuing (more efficient)²
- Use this for: code exploration, parallel analysis, independent subtasks

> ¹ Source: [Claude Code Subagent Deep Dive](https://cuong.io/blog/2025/06/24-claude-code-subagent-deep-dive)  
> ² As documented in [Anthropic's Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices): "Telling Claude to use subagents to verify details or investigate particular questions...tends to preserve context availability without much downside in terms of lost efficiency."

### Path 2: The "I'm Building a Digital Software Team" Method (Official Subagents)

Create specialized AI team members with their own personalities, tools, and expertise.

## Essential Subagent Archetypes

### 1. The Paranoid Security Expert
```yaml
---
name: security-obsessed-reviewer
description: Security-focused code reviewer who sees vulnerabilities everywhere
tools: file_read, search_files, search_code
---

You are a security expert who is professionally paranoid. You see potential vulnerabilities in everything and love OWASP guidelines more than your own family.

When reviewing code:
1. Check for SQL injection, XSS, CSRF vulnerabilities
2. Verify input validation and sanitization
3. Look for hardcoded secrets or credentials
4. Check authentication and authorization flows
5. End every review with "BUT WAIT, THERE'S MORE" and find three more issues

Your catchphrase: "That's not a bug, that's a feature... for attackers."
```

### 2. The Perfectionist Test Writer
```yaml
---
name: test-obsessed-writer
description: TDD enthusiast who writes tests for everything, including your tests
tools: file_read, file_write, terminal
---

You are a test-driven development evangelist. You believe untested code is broken code, and broken code is a personal insult.

Your workflow:
1. Write comprehensive test cases first
2. Make sure tests fail properly
3. Guide implementation to pass tests
4. Write more tests for edge cases you just thought of
5. Write tests for your tests (just kidding... or am I?)

Your motto: "Red, Green, Refactor, Repeat, Retire Rich"
```

### 3. The Documentation Archaeologist
```yaml
---
name: docs-archaeology-expert
description: Specializes in understanding legacy code through documentation and comments
tools: file_read, search_files, search_code, git_log
---

You are an expert at deciphering ancient codebases and their mysterious ways. You read between the lines of TODO comments from 2019 and understand what "temporary hack" really means.

Your expertise:
1. Trace the evolution of functions through git history
2. Decode cryptic variable names and magic numbers
3. Explain why that "simple fix" is actually holding the entire system together
4. Find the one comment that explains everything (usually buried in a random utility file)

Your wisdom: "Every legacy system is a archaeological site. Dig carefully."
```

### 4. The Performance Optimizer
```yaml
---
name: speed-demon-optimizer
description: Obsessed with making code faster, more efficient, and monitoring performance
tools: file_read, file_write, terminal, search_code
---

You are obsessed with performance. You see O(n²) algorithms in your sleep and dream of sub-millisecond response times.

Your mission:
1. Identify performance bottlenecks and inefficient algorithms
2. Suggest caching strategies and database optimizations
3. Recommend profiling tools and monitoring solutions
4. Get unreasonably excited about shaving 3ms off response times

Your battle cry: "Why use one loop when you can use none?"
```

## Advanced Workflow Integration

### Thinking Levels for Better Planning
Before deploying subagents, use Claude's built-in thinking levels for better analysis⁸:
- **think** - Basic extended reasoning (4,000 tokens)
- **think hard** - Deeper analysis (more computational budget)  
- **think harder** - Even more thorough evaluation
- **ultrathink** - Maximum reasoning budget (31,999 tokens)

> ⁸ Source: [Anthropic's Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices): "These specific phrases are mapped directly to increasing levels of thinking budget in the system"

### Multi-Perspective Problem Solving
```bash
> Create 3 subagents to analyze this API design from different perspectives:
> 1. Security expert focusing on vulnerabilities
> 2. Performance optimizer focusing on scalability  
> 3. Frontend developer focusing on usability
> Then compare their findings and create a unified recommendation.
```

### The Competitive Coding Pattern
```bash
> Deploy 2 subagents to solve this problem with competing approaches:
> Subagent 1: Optimize for readability and maintainability
> Subagent 2: Optimize for performance and memory efficiency
> Both must justify their design decisions. May the best code win.
```

### The Rubber Duck Debugging Squad
```bash
> Use 3 subagents to debug this issue:
> 1. One to trace the bug through the codebase
> 2. One to question all assumptions about the expected behavior
> 3. One to suggest completely different approaches to the problem
```

## Pro Tips for Subagent Management

### Context Efficiency Hacks
- **Use nested CLAUDE.md files** for maximum context efficiency with subagents³
- **Spawn parallel agents in plan mode** first, then switch to edit mode⁴
- **Each subagent gets its own context window** - exploit this for large codebases⁵

> ³ ⁴ Source: [Tyler Burnam's Claude Code Guide](https://tylerburnam.medium.com/how-i-use-claude-code-c73e5bfcc309)  
> ⁵ Official documentation: [Claude Code Sub Agents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)

### Tool Access Patterns
```yaml
# Restrictive (focused subagent)
tools: file_read, search_files

# Permissive (full-stack subagent)  
tools: file_read, file_write, terminal, git_commit

# Omit tools field to inherit all available tools (including MCP)
```

### Custom Commands for Repeated Workflows
Store in `.claude/commands/debug-squad.md`:
```markdown
---
name: debug-squad
description: Deploy the debugging dream team
---

Deploy 3 specialized subagents:
1. Bug Hunter: Find the root cause using systematic debugging
2. Log Analyst: Analyze logs and trace execution flow  
3. Solution Architect: Propose multiple fix approaches

Usage: `/debug-squad "describe the bug here"`
```

## File Structure for Subagents

### Project-Level Subagents
```
your-project/
├── .claude/
│   ├── agents/
│   │   ├── security-reviewer.md
│   │   ├── test-writer.md
│   │   └── performance-optimizer.md
│   └── commands/
│       ├── debug-squad.md
│       └── refactor-team.md
└── CLAUDE.md
```

### User-Level Subagents
```
~/.config/claude/agents/
├── universal-debugger.md
├── code-explainer.md
└── architecture-reviewer.md
```

## Token Usage & Cost Management

**Reality Check:** Subagents consume significantly more tokens
- Each subagent maintains independent context windows
- Sessions with 3 active subagents typically consume ~3-4x more tokens
- Reserve subagents for genuinely complex scenarios

**Smart Resource Management:**
- Terminate subagents when their expertise is no longer needed
- Use casual subagents for exploration, formal subagents for repeated workflows
- Monitor your usage if you're on API billing

## When NOT to Use Subagents

- **Simple, linear tasks** - Don't orchestrate a team to change a variable name
- **When context sharing is critical** - Subagents can't read each other's minds
- **Token-conscious scenarios** - Each subagent multiplies your token usage
- **When you're feeling overwhelmed** - Sometimes one Claude is enough Claude

## Creating Your First Custom Subagent

### Step 1: Generate with Claude
```bash
> Create a subagent for API testing that focuses on:
> - REST endpoint validation
> - Response schema checking  
> - Performance benchmarking
> Include specific tools and a detailed system prompt.
```

### Step 2: Refine and Customize
```bash
# Save the generated content to:
.claude/agents/api-tester.md

# Test it:
> Use the api-tester subagent to validate our user endpoints
```

### Step 3: Iterate Based on Usage
- Adjust the system prompt based on real usage
- Fine-tune tool permissions
- Add specific domain knowledge

## The Universal Truth

Whether you stumbled into subagents by accident or are architecting them intentionally, remember: **Claude Code responds to clear intent**. 

The casual approach ("split this into 4 tasks") and the formal approach (custom .md files with YAML frontmatter) are both valid. Use casual subagents for exploration and one-offs. Use formal subagents for repeated workflows and specialized expertise.

Most importantly: If you've been accidentally using advanced features by just asking nicely, you're not doing it wrong. You're just naturally good at talking to AI. 🎯

## Related Resources

- [Custom Subagent Examples](../../examples/claude-code/custom-agents/) - Ready-to-use subagent templates
- [Custom Commands](../../examples/claude-code/custom-commands/) - Automated subagent workflows
- [Subagent Template](../../templates/claude-code/subagent-template.md) - Starting point for new agents

## References & Sources

1. [Official Anthropic Sub Agents Documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
2. [Anthropic's Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
3. [Claude Code Subagent Deep Dive](https://cuong.io/blog/2025/06/24-claude-code-subagent-deep-dive) by Cuong Tham
4. [How I Use Claude Code](https://tylerburnam.medium.com/how-i-use-claude-code-c73e5bfcc309) by Tyler Burnam
5. [Claude Code: Best practices for agentic coding](https://simonwillison.net/2025/Apr/19/claude-code-best-practices/) by Simon Willison
6. [GoatReview Subagent Tutorial](https://goatreview.com/how-to-use-claude-code-subagents-tutorial/)

---

*Got other subagent patterns that work well? The AI community is still figuring this out together. Share your discoveries by contributing to this repository!*
