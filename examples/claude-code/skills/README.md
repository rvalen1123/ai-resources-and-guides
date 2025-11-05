# Claude Code Skills

> **Reusable workflow packages for specialized tasks**

Claude Code Skills are modular, self-contained packages that bundle instructions, scripts, and resources to solve specific, repeatable tasks. Unlike custom agents or commands, Skills are dynamic workflow packages that Claude can automatically discover and invoke when needed.

## What Are Claude Code Skills?

**Skills = Instructions + Scripts + Resources + Metadata**

A Skill is a folder containing:
- `SKILL.md` - Core instructions and metadata
- Scripts and code files
- Templates and reference files
- Supporting resources

### Skills vs. Custom Agents vs. Commands

| Feature | Skills | Custom Agents | Custom Commands |
|---------|--------|---------------|-----------------|
| Structure | Folder with SKILL.md | Single markdown file | Single markdown file |
| Invocation | Automatic by Claude | Manual delegation | Manual trigger |
| Scope | Workflow + code + assets | Instructions only | Workflow steps |
| Portability | IDE + API + Web | IDE only | IDE only |
| Dynamic Loading | Yes | No | No |
| Versioning | Built-in | Manual | Manual |

### When to Use Skills

**Use Skills for:**
- ✅ Domain-specific, repeatable workflows
- ✅ Tasks requiring multiple files/assets
- ✅ Workflows shared across projects
- ✅ Team standardization
- ✅ Complex automation pipelines

**Use Custom Agents instead for:**
- ❌ One-off specialized tasks
- ❌ Simple instruction sets
- ❌ Project-specific helpers

**Use Custom Commands instead for:**
- ❌ Quick workflow shortcuts
- ❌ Sequential task execution
- ❌ Manual process automation

## Skill Structure

### Basic SKILL.md Format

```markdown
# Skill Name

**Version:** 1.0.0
**Author:** Your Name
**Description:** Brief description of what this skill does

## Metadata
- **Triggers:** Keywords that activate this skill
- **Dependencies:** Required tools, libraries, or other skills
- **Category:** [development, analysis, documentation, etc.]

## Instructions

[Detailed instructions for Claude on how to execute this skill]

## Examples

[Example usage scenarios]

## Resources

[List of included files and their purposes]
```

### Folder Structure

```
skill-name/
├── SKILL.md              # Core skill definition
├── scripts/              # Helper scripts
│   ├── helper.py
│   └── validator.js
├── templates/            # Code templates
│   └── template.txt
├── resources/            # Reference files
│   └── reference.md
└── tests/                # Test cases (optional)
    └── test.py
```

## Example Skills in This Repository

### Brand Guidelines Enforcer
**Purpose:** Ensure code and documentation follow company brand guidelines
**Location:** `brand-guidelines/`
**Triggers:** brand, style guide, corporate standards

### Code Reviewer
**Purpose:** Systematic code review with security, performance, and style checks
**Location:** `code-reviewer/`
**Triggers:** code review, PR review, security audit

### API Documentation Generator
**Purpose:** Generate comprehensive API documentation from code
**Location:** `api-docs-generator/`
**Triggers:** API docs, documentation, swagger, openapi

## Creating Your Own Skills

### Step 1: Plan Your Skill

**Questions to answer:**
- What specific problem does this solve?
- What files/resources are needed?
- When should Claude invoke this?
- What are the dependencies?

### Step 2: Use the Template

Start with the [Skill Template](../../../templates/claude-code/skill-template.md) and customize it for your needs.

### Step 3: Structure Your Skill

```bash
# Create skill directory
mkdir my-skill-name
cd my-skill-name

# Create core file
touch SKILL.md

# Add supporting resources
mkdir scripts templates resources
```

### Step 4: Test Your Skill

- Test in Claude Code IDE
- Verify automatic invocation
- Check resource loading
- Validate outputs

### Step 5: Share Your Skill

**In this Repository:**
- Add to `examples/claude-code/skills/`
- Include clear documentation
- Provide example usage

**Community Submissions:**
- Share in `community/user-submissions/`
- Follow submission guidelines
- Include metrics/results

**External:**
- Publish to GitHub
- Share in Claude community forums
- Add to skill registries

## Using Skills in Claude Code

### Automatic Invocation

Claude automatically detects and loads relevant skills based on your prompts:

```bash
# Claude detects "brand guidelines" trigger and loads the skill
> Review this code for brand guidelines compliance

# Claude detects "API documentation" trigger
> Generate API documentation for this service
```

### Manual Invocation

You can explicitly reference a skill:

```bash
> Use the code-reviewer skill to analyze this PR

> Apply the api-docs-generator skill to this codebase
```

### Skill Discovery

```bash
> What skills are available?
> Show me skills related to documentation
> List security-focused skills
```

## Community Skills

Looking for more skills? Check out:

### In This Repository
- Browse `examples/claude-code/skills/` for curated examples
- Visit `community/user-submissions/` for user-contributed skills

### External Resources
- [Anthropic Skills Gallery](https://www.anthropic.com/skills) - Official skill collection
- [Claude Community Forum](https://community.anthropic.com/) - User-shared skills
- [GitHub Topics](https://github.com/topics/claude-skills) - Open-source skills

## Skill Development Best Practices

### 1. Clear Naming
```markdown
# ✅ Good: api-docs-generator
# ❌ Bad: tool1, my-skill, helper
```

### 2. Specific Triggers
```markdown
# ✅ Good: "API documentation", "swagger", "openapi"
# ❌ Bad: "docs", "help", "generate"
```

### 3. Complete Instructions
```markdown
# ✅ Include:
- Step-by-step workflow
- Expected inputs/outputs
- Error handling
- Edge cases

# ❌ Avoid:
- Vague descriptions
- Missing context
- Assumed knowledge
```

### 4. Modular Resources
```markdown
# ✅ Organize:
scripts/       # Executable code
templates/     # Reusable templates
resources/     # Reference materials
tests/         # Validation tests

# ❌ Avoid:
- Everything in SKILL.md
- Unclear file purposes
- Missing documentation
```

### 5. Version Control
```markdown
# ✅ Track:
- Version number in SKILL.md
- Change log
- Breaking changes
- Migration guides

# ❌ Avoid:
- Unversioned changes
- Silent breaking updates
- No backward compatibility info
```

## Advanced Patterns

### Composite Skills

Create skills that invoke other skills:

```markdown
# full-stack-setup/SKILL.md

## Dependencies
- backend-scaffold
- frontend-scaffold
- database-setup

## Instructions
1. Invoke backend-scaffold skill
2. Invoke frontend-scaffold skill
3. Invoke database-setup skill
4. Configure integration
```

### Parameterized Skills

Accept parameters for customization:

```markdown
# test-generator/SKILL.md

## Parameters
- framework: [jest, mocha, pytest, junit]
- coverage: [unit, integration, e2e]
- style: [tdd, bdd]

## Instructions
1. Detect framework from project
2. Generate tests based on coverage level
3. Apply style conventions
```

### Contextual Skills

Adapt behavior based on project context:

```markdown
# code-formatter/SKILL.md

## Context Detection
- Language: Auto-detect from files
- Style Guide: Check for .prettierrc, .eslintrc
- Project Type: Identify framework

## Instructions
1. Detect project context
2. Apply appropriate formatting rules
3. Respect existing configurations
```

## Troubleshooting

### Skill Not Loading

**Check:**
- ✅ SKILL.md exists and is valid
- ✅ Metadata is properly formatted
- ✅ Triggers are specific enough
- ✅ Dependencies are available

### Skill Not Triggering

**Try:**
- 🔧 Use more specific keywords
- 🔧 Explicitly reference the skill
- 🔧 Check trigger keywords in SKILL.md
- 🔧 Verify skill is in correct location

### Resource Loading Issues

**Verify:**
- 📁 Files are in skill folder
- 📁 Paths are relative to SKILL.md
- 📁 File permissions are correct
- 📁 File formats are supported

## Contributing Skills

We welcome skill contributions! See:
- [Contributing Guidelines](../../../README.md#contributing)
- [Skill Template](../../../templates/claude-code/skill-template.md)
- [Community Submissions Guide](../../../community/user-submissions/README.md)

### Submission Checklist

Before submitting a skill:
- [ ] SKILL.md is complete and well-documented
- [ ] Instructions are clear and testable
- [ ] Resources are included and referenced
- [ ] Version is specified
- [ ] Dependencies are listed
- [ ] Examples demonstrate usage
- [ ] Tested in Claude Code IDE
- [ ] No sensitive data or credentials
- [ ] Follows naming conventions
- [ ] Includes license information

## Resources

### Official Documentation
- [Anthropic Skills Guide](https://www.anthropic.com/news/skills)
- [Claude Help Center - Skills](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)
- [Skills API Reference](https://docs.anthropic.com/en/docs/skills)

### Community Guides
- [Claude Skills Reference](../../../guides/claude-code/claude-skills-reference.md)
- [Inside Claude Code Skills](https://mikhail.io/2025/10/claude-code-skills/)
- [Skills vs Commands vs Agents](https://danielmiessler.com/blog/when-to-use-skills-vs-commands-vs-agents)

### Related Resources in This Repository
- [Custom Agents](../custom-agents/) - For instruction-only workflows
- [Custom Commands](../custom-commands/) - For sequential task automation
- [Proven Workflows](../workflows/) - For pattern-based development

---

*Skills transform Claude into a specialist for your specific needs. Create once, use everywhere.*
