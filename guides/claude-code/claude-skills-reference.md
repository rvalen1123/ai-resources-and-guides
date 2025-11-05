# Claude Skills Reference Guide

> **Complete reference for Claude's built-in capabilities and skills**

*Your comprehensive guide to understanding what Claude can do natively*

## What Are Claude Skills?

Claude Skills are the built-in capabilities that Claude possesses without needing external tools or MCP servers. Understanding these skills helps you:
- Know what Claude can do out-of-the-box
- Avoid unnecessary tool/MCP integration for tasks Claude handles natively
- Structure prompts to leverage Claude's strengths
- Combine skills for powerful workflows

## Core Language & Reasoning Skills

### 🧠 Advanced Reasoning

**Extended Thinking**
- **Think modes** - `think`, `think hard`, `think harder`, `ultrathink`
- **Token budgets** - 4K, 10K, 31K+ tokens for reasoning
- **Use cases** - Complex problem-solving, architecture design, debugging

```bash
# Examples
> Analyze this distributed system architecture ultrathink
> Debug this race condition think hard
> Optimize this algorithm think
```

**Logical Analysis**
- Deductive reasoning
- Pattern recognition
- Problem decomposition
- Root cause analysis
- Trade-off evaluation

### 📝 Natural Language Processing

**Understanding**
- Context comprehension across long conversations
- Intent detection
- Nuance and ambiguity handling
- Multiple language support

**Generation**
- Technical writing
- Documentation
- Explanations and tutorials
- Code comments
- Error messages

**Transformation**
- Summarization
- Simplification/complexification
- Tone adjustment
- Format conversion
- Translation

## Programming & Development Skills

### 💻 Code Understanding

**Multi-Language Proficiency**
- Python, JavaScript/TypeScript, Java, C++, C#, Go, Rust, Ruby, PHP
- SQL, HTML/CSS, Shell scripting
- Emerging languages (Zig, Swift, Kotlin, Dart)

**Code Analysis**
- Reading and comprehending code
- Identifying patterns and anti-patterns
- Understanding architecture and design
- Tracing execution flow
- Spotting bugs and vulnerabilities

**Documentation Reading**
- Understanding API documentation
- Parsing README files
- Interpreting specifications
- Learning from examples

### 🛠️ Code Generation

**Writing New Code**
- Functions, classes, modules
- Tests (unit, integration, E2E)
- Configuration files
- Scripts and utilities
- Boilerplate and scaffolding

**Code Modification**
- Refactoring
- Optimization
- Bug fixes
- Feature additions
- Code migration

**Code Patterns**
- Design patterns implementation
- Architecture patterns
- Best practices application
- Framework-specific patterns

### 🔍 Debugging & Problem Solving

**Error Analysis**
- Stack trace interpretation
- Error message decoding
- Exception handling
- Log analysis

**Debugging Strategies**
- Hypothesis generation
- Test case creation
- Isolation techniques
- Systematic elimination

**Performance Analysis**
- Identifying bottlenecks
- Algorithm complexity analysis
- Memory usage optimization
- Profiling interpretation

## Software Engineering Skills

### 📐 Architecture & Design

**System Design**
- High-level architecture planning
- Component design
- API design
- Database schema design
- Scalability planning

**Design Patterns**
- Creational (Singleton, Factory, Builder)
- Structural (Adapter, Decorator, Facade)
- Behavioral (Observer, Strategy, Command)

**Best Practices**
- SOLID principles
- DRY, KISS, YAGNI
- Clean code principles
- Code organization

### 🧪 Testing

**Test Design**
- Unit test creation
- Integration test planning
- E2E test scenarios
- Test data generation
- Edge case identification

**TDD Support**
- Red-Green-Refactor workflow
- Test-first development
- Behavior-driven development
- Specification by example

**Quality Assurance**
- Code coverage analysis
- Test effectiveness evaluation
- Testing strategy recommendations

### 🔒 Security

**Vulnerability Detection**
- SQL injection
- XSS (Cross-site scripting)
- CSRF protection
- Authentication/authorization issues
- Input validation
- Secrets in code

**Security Best Practices**
- OWASP Top 10 awareness
- Secure coding patterns
- Encryption recommendations
- Access control design

**Code Review**
- Security-focused reviews
- Vulnerability assessment
- Risk evaluation

## Data & Analysis Skills

### 📊 Data Processing

**Data Transformation**
- Parsing (JSON, XML, CSV, etc.)
- Format conversion
- Data cleaning
- Normalization
- Aggregation

**Data Analysis**
- Pattern identification
- Statistical analysis
- Trend detection
- Anomaly detection

**Query Languages**
- SQL query writing and optimization
- NoSQL query patterns
- GraphQL schema and queries

### 🗄️ Database Knowledge

**Schema Design**
- Table design
- Relationships (1:1, 1:N, N:M)
- Indexing strategies
- Normalization/denormalization

**Database Operations**
- CRUD operations
- Transactions
- Migrations
- Query optimization

**Database Types**
- Relational (PostgreSQL, MySQL, SQLite)
- NoSQL (MongoDB, Redis, Cassandra)
- Graph databases
- Time-series databases

## DevOps & Infrastructure Skills

### 🚀 Deployment & Operations

**CI/CD**
- Pipeline configuration
- GitHub Actions workflows
- GitLab CI/CD
- Jenkins, CircleCI, Travis CI

**Infrastructure as Code**
- Docker containerization
- Kubernetes manifests
- Terraform configurations
- CloudFormation templates

**Cloud Platforms**
- AWS services knowledge
- Azure services
- Google Cloud Platform
- Serverless patterns

### 🔧 Configuration

**Config Files**
- JSON, YAML, TOML, INI
- Environment variables
- Feature flags
- Build configurations

**Package Management**
- npm/yarn (Node.js)
- pip/poetry (Python)
- Maven/Gradle (Java)
- Cargo (Rust)
- Go modules

## Workflow & Productivity Skills

### 📋 Project Management

**Planning**
- Task breakdown
- Estimation
- Dependency mapping
- Risk identification

**Documentation**
- README files
- API documentation
- Architecture docs
- User guides
- Changelog maintenance

**Git Workflows**
- Branch strategies
- Commit message conventions
- PR descriptions
- Merge conflict resolution

### 🤝 Collaboration

**Code Review**
- Constructive feedback
- Best practice suggestions
- Alternative approaches
- Learning opportunities

**Communication**
- Technical explanations
- Status updates
- Documentation
- Knowledge sharing

## Claude Code-Specific Skills

### 🎯 Subagent Orchestration

**Task Delegation**
- Spawning parallel subagents
- Task distribution
- Coordinating multiple agents
- Aggregating results

**Context Management**
- Efficient context usage
- Subagent specialization
- Independent context windows

### 📁 File Operations

**File Handling**
- Reading files
- Writing files
- File searching
- Batch operations

**Directory Operations**
- Structure navigation
- Pattern matching
- Recursive operations

### 🔄 Git Integration

**Repository Operations**
- Status checking
- Diff viewing
- Commit creation
- Branch management

**History Analysis**
- Commit history review
- Blame investigation
- Change tracking

## AI-Enhanced Development Skills

### 🎨 Creative Problem Solving

**Alternative Approaches**
- Multiple solution generation
- Trade-off analysis
- Innovation and creativity
- Out-of-box thinking

**Optimization**
- Performance improvement
- Code simplification
- Resource efficiency
- User experience enhancement

### 📚 Learning & Adaptation

**Technology Adoption**
- New framework learning
- API exploration
- Best practice discovery
- Pattern recognition from examples

**Context Understanding**
- Codebase comprehension
- Business logic understanding
- Domain knowledge acquisition
- Technical debt assessment

## Specialized Domain Skills

### 🌐 Web Development

**Frontend**
- React, Vue, Angular, Svelte
- HTML/CSS/JavaScript
- Responsive design
- Accessibility (a11y)
- Performance optimization

**Backend**
- REST API design
- GraphQL
- WebSocket
- Authentication/authorization
- Session management

**Full-Stack**
- End-to-end development
- API integration
- State management
- Routing

### 📱 Mobile Development

**Cross-Platform**
- React Native
- Flutter
- Ionic

**Native**
- iOS (Swift, SwiftUI)
- Android (Kotlin, Jetpack Compose)

### 🎮 Other Domains

**Data Science**
- Pandas, NumPy
- Data visualization
- Machine learning pipelines
- Feature engineering

**Game Development**
- Unity (C#)
- Godot (GDScript)
- Game logic
- Physics implementation

**Embedded Systems**
- Arduino
- Raspberry Pi
- Microcontroller programming
- Hardware interaction

## What Claude Cannot Do Natively

Understanding limitations is as important as understanding capabilities:

### ❌ Cannot Do Without Tools/MCP

- **Execute code** (needs terminal access)
- **Access internet** (needs web search MCP)
- **Read local files** (needs filesystem MCP or Claude Code file access)
- **Make API calls** (needs fetch MCP)
- **Access databases** (needs database MCP)
- **Real-time information** (knowledge cutoff applies)
- **Browse websites** (needs browser automation MCP)

### ❌ General Limitations

- **Visual understanding** (no image analysis in Claude Code)
- **Audio processing** (no speech/music analysis)
- **Real-time execution** (needs verification)
- **External state** (no persistent memory without MCP)
- **Binary file operations** (limited to text files)

## Leveraging Claude Skills Effectively

### Best Practices

**1. Use Built-in Skills First**
```bash
# Good: Use native code generation
> Create a Python function to parse CSV files

# Unnecessary: Don't use MCP for tasks Claude handles natively
# (Don't need filesystem MCP just to generate code)
```

**2. Combine Skills**
```bash
# Combine reasoning + code generation + testing
> ultrathink a caching strategy, implement it, and write comprehensive tests
```

**3. Progressive Complexity**
```bash
# Start simple, add complexity as needed
> Create a basic REST API
> Add authentication
> Add rate limiting
> Add caching ultrathink
```

**4. Leverage Context**
```bash
# Reference previous work
> Based on the auth system we just built, add OAuth2 support
```

### Skill Combinations

**Architecture + Code + Tests**
```bash
> Design a microservices architecture think hard
> Implement the user service with authentication
> Write integration tests for the service
```

**Analysis + Refactoring + Documentation**
```bash
> Analyze this legacy code think
> Refactor it using modern patterns
> Document the changes and update the README
```

**Debugging + Optimization + Testing**
```bash
> Debug this performance issue think hard
> Optimize the slow queries
> Add performance tests to prevent regression
```

## Skills Development Roadmap

### Beginner: Understanding Core Skills
- Basic code generation
- Simple debugging
- Documentation reading
- Standard patterns

### Intermediate: Combining Skills
- Extended reasoning (think/think hard)
- Multi-file projects
- Testing strategies
- Architecture basics

### Advanced: Orchestration
- Subagent coordination
- UltraThink for complex problems
- Custom workflows
- Domain expertise

## Resources

### Skill-Specific Guides
- [Thinking Levels Guide](thinking-levels-guide.md) - Extended reasoning mastery
- [Subagent Best Practices](subagent-best-practices.md) - Multi-agent orchestration
- [MCP Servers Guide](mcp-servers-guide.md) - Extending capabilities

### Claude Code Documentation
- [Official Anthropic Docs](https://docs.anthropic.com/en/docs/claude-code/)
- [Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)

### Community
- [Claude Code Examples](../../examples/claude-code/)
- [Custom Subagents](../../examples/claude-code/custom-agents/)
- [Workflow Patterns](../../examples/claude-code/workflows/)

---

*Understanding Claude's native skills helps you work smarter, not harder. Use built-in capabilities first, extend with MCP when needed.*
