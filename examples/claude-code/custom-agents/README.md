# Custom Claude Code Subagents

> **Based on:** [Official Anthropic Sub Agents Documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents) and best practices from the Claude Code community.

Ready-to-use, lightweight subagent templates for specialized coding tasks. Each subagent is designed to stay under the 400-character limit while providing focused expertise.

## Available Subagents

### 🔒 [Security Reviewer](security-reviewer.md)
**Focus:** Security vulnerabilities, OWASP compliance  
**Tools:** file_read, search_files, search_code  
**Use case:** Code security audits, vulnerability detection

### 🧪 [Test Writer](test-writer.md)
**Focus:** Test-driven development, comprehensive testing  
**Tools:** file_read, file_write, terminal  
**Use case:** Writing unit tests, TDD workflows

### 📚 [Legacy Expert](legacy-expert.md)
**Focus:** Legacy code analysis, git history investigation  
**Tools:** file_read, search_files, search_code, git_log  
**Use case:** Understanding old codebases, code archaeology

### ⚡ [Performance Optimizer](performance-optimizer.md)
**Focus:** Performance optimization, bottleneck identification  
**Tools:** file_read, file_write, terminal, search_code  
**Use case:** Performance audits, optimization strategies

## How to Use

### Copy to Your Project
```bash
mkdir -p .claude/agents
cp security-reviewer.md .claude/agents/
# Claude will auto-detect and use when appropriate
```

### Invoke Explicitly
```bash
> Use the security-reviewer subagent to audit this auth code
> Deploy the test-writer to create tests for the user service
> Have the legacy-expert analyze this payment system
```

## Design Principles

These subagents follow the **official Claude Code patterns**:
- **Lightweight** - Stay under 400 characters total
- **Focused** - Single area of expertise
- **Practical** - Clear, actionable system prompts
- **Tool-specific** - Appropriate tool permissions

## Creating Custom Subagents

### Official Recommendation
**Start with Claude-generated agents:** Anthropic recommends "generating your initial sub agent with Claude and then iterating on it to make it personally yours. This approach gives you the best results - a solid foundation that you can customize to your specific needs."

Keep it simple:
1. **Short description** - What does it do?
2. **Minimal tools** - Only what's needed
3. **Concise prompt** - 1-2 sentences max
4. **Test the length** - Watch for the 400-character warning

See our [Subagent Template](../../../templates/claude-code/subagent-template.md) for a starting point.

---

*These subagents are designed to be practical, not personalities. They get the job done efficiently.*
