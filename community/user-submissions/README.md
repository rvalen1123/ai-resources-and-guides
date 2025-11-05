# Community User Submissions

> **Share your Claude Code setup, patterns, and discoveries**

This is a community space for sharing real-world configurations, workflows, and best practices. Learn from others and contribute your own discoveries!

## How to Contribute

### What to Share

**Your Setup:**
- CLAUDE.md configurations that work well
- MCP server combinations
- Custom subagents
- **Claude Code Skills** - Your reusable workflow packages
- Workspace organization

**Discovered Patterns:**
- Unique workflows
- Productivity hacks
- Problem-solving approaches
- Tool combinations

**Real-World Examples:**
- Production configurations
- Team setups
- Project-specific adaptations
- Industry-specific patterns
- **Custom Skills** - Share your specialized skill packages

### Submission Guidelines

1. **Create a new markdown file** in this directory
   - Name: `username-topic.md` (e.g., `alice-saas-setup.md`)
   - Or create a subdirectory: `username/` for multiple submissions

2. **Include these sections:**
   ```markdown
   # [Your Title]
   
   **Author:** Your Name (@github-username)
   **Date:** YYYY-MM-DD
   **Tags:** [relevant, tags, here]
   
   ## Context
   [What problem does this solve? What's your use case?]
   
   ## Setup/Pattern
   [Your configuration, workflow, or pattern]
   
   ## Results
   [What improved? Metrics if available]
   
   ## Lessons Learned
   [What worked? What didn't?]
   ```

3. **Submit a PR** with:
   - Clear title describing your contribution
   - Brief description in PR body
   - Any relevant context or screenshots

### Submission Templates

Choose the template that fits your contribution:

#### Setup/Configuration Template
```markdown
# [Your Setup Name]

**Author:** Your Name (@username)
**Date:** 2024-XX-XX
**Tags:** setup, configuration, [tech-stack]
**Context:** [SaaS, Agency, Enterprise, Startup, etc.]

## Project Type
[Describe your project/company type]

## Tech Stack
- Primary language(s)
- Frameworks
- Databases
- Cloud providers
- Other tools

## CLAUDE.md Structure
```
[Your CLAUDE.md hierarchy]
```

## MCP Servers Used
```json
{
  "servers": {
    // Your MCP configuration
  }
}
```

## Custom Subagents
- [List your custom subagents]
- Why you created them
- How they help

## Workflow
[Typical daily workflow with Claude Code]

## Results
- Time saved: X hours/week
- Code quality improvements
- Team productivity gains
- Other metrics

## Tips & Tricks
[Specific tips that others might find useful]

## Challenges
[Problems you faced and how you solved them]
```

#### Workflow Pattern Template
```markdown
# [Workflow Name]

**Author:** Your Name (@username)
**Date:** 2024-XX-XX
**Tags:** workflow, pattern, [domain]
**Use Case:** [When to use this workflow]

## Problem
[What problem does this workflow solve?]

## Solution
[Your workflow step-by-step]

## Example
[Real example of using this workflow]

## Variations
[Alternative approaches or adaptations]

## Results
[Outcomes, before/after metrics]
```

#### Discovery/Tip Template
```markdown
# [Discovery/Tip Title]

**Author:** Your Name (@username)
**Date:** 2024-XX-XX
**Tags:** tip, discovery, [category]

## What I Discovered
[Your finding]

## Why It Matters
[Impact and usefulness]

## How to Use It
[Step-by-step or example]

## Caveats
[Limitations or considerations]
```

#### Claude Code Skill Template
```markdown
# [Skill Name] - SKILL.md

**Version:** 1.0.0
**Author:** Your Name (@username)
**Date:** 2024-XX-XX
**Tags:** skill, [category], [domain]

## Metadata
- **Category:** [development | testing | documentation | etc.]
- **Triggers:** [keywords that activate this skill]
- **Dependencies:** [required tools or other skills]
- **Compatibility:** [Claude Code IDE | API | Web | All]

## Overview
[What problem does this skill solve?]

## Instructions
[Step-by-step workflow for Claude to execute]

## Examples
[Real usage examples with inputs and outputs]

## Resources
[Included files: scripts, templates, references]

## Results & Metrics
[How this skill improved your workflow]

## Sharing Options
- **Upload Full Skill:** Create folder with SKILL.md and resources
- **Link to External:** Share GitHub/Gist link to your skill
- **Reference Official:** Link to published skill in Anthropic gallery
```

**Note on Skill Submissions:**
- For **complete skills**, create a folder: `username-skill-name/` with SKILL.md and resources
- For **external skills**, just link to your GitHub repo or published location
- Follow the [Skill Template](../../templates/claude-code/skill-template.md) for structure

## Example Submissions

Here are examples of great submissions (coming soon as community contributes):

### SaaS Startup Setup
*Example: Complete setup for a fast-moving startup*
- Lean CLAUDE.md focused on speed
- MCP servers for GitHub, Slack, database
- Custom subagents for rapid feature development
- TDD workflow with test-writer subagent

### Enterprise Integration Pattern
*Example: Large codebase management*
- Hierarchical CLAUDE.md structure
- Multiple specialized subagents
- Code review automation
- Documentation generation workflow

### Solo Developer Productivity
*Example: Maximizing individual efficiency*
- Minimal but effective CLAUDE.md
- Key MCP servers for solo work
- Workflow automation
- Time-saving patterns

### Agency Client Projects
*Example: Managing multiple projects*
- Template-based CLAUDE.md
- Reusable subagent library
- Quick project setup workflow
- Client-specific adaptations

## Community Highlights

*Notable submissions will be highlighted here*

### 🏆 Most Popular
[Links to most useful submissions]

### ⚡ Recently Added
[Links to recent submissions]

### 💡 Hidden Gems
[Underrated but valuable submissions]

## Discussion & Questions

- **Have questions about a submission?** Open an issue with `[Question]` tag
- **Want to discuss a pattern?** Start a discussion in Issues
- **Found a better approach?** Submit an improvement PR

## Contribution Tips

### Make It Useful
- ✅ **Specific** - Real examples, not generic advice
- ✅ **Tested** - Share what actually works
- ✅ **Context** - Explain your situation
- ✅ **Honest** - Include what didn't work

### Make It Discoverable
- ✅ **Good title** - Clear and descriptive
- ✅ **Tags** - Help others find it
- ✅ **Search terms** - Include relevant keywords
- ✅ **Cross-reference** - Link related submissions

### Make It Maintainable
- ✅ **Date it** - Include when you wrote it
- ✅ **Update** - Keep it current if things change
- ✅ **Version info** - Note Claude Code version if relevant
- ✅ **Contact** - How to reach you for questions

## Privacy & Security

**Please be careful not to share:**
- ❌ API keys or tokens
- ❌ Proprietary code
- ❌ Company secrets
- ❌ Personal information
- ❌ Database credentials

**Safe to share:**
- ✅ Configuration structures
- ✅ Workflow patterns
- ✅ Generic code examples
- ✅ Anonymized metrics
- ✅ Best practices

## License

By submitting to this directory, you agree to:
- Share under MIT License (same as repository)
- Allow others to learn from and adapt your submission
- Receive attribution for your contribution

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in their submissions
- Appreciated by the community! 🎉

---

## Questions?

- Check [Contributing Guidelines](../../README.md#contributing)
- Open an issue with `[Community]` tag
- Ask in discussions

**Let's learn from each other and make Claude Code more effective for everyone!**
