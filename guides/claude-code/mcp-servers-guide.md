# Model Context Protocol (MCP) Servers Guide

> **Complete reference for MCP servers, integration, and best practices**

*Last Updated: November 2025*

## What is MCP?

Model Context Protocol (MCP) is an open standard that enables Claude and other AI assistants to securely connect to external data sources and tools. Think of it as a universal adapter that lets Claude interact with your databases, APIs, filesystems, and other services.

> **Official Definition:** "MCP provides a standardized way to connect AI assistants to the data and tools they need" - [Anthropic MCP Documentation](https://modelcontextprotocol.io/)

## Why Use MCP Servers?

- **Extend Claude's capabilities** beyond its built-in knowledge
- **Access real-time data** from databases, APIs, and services
- **Automate workflows** by connecting multiple tools
- **Maintain security** with controlled, scoped access
- **Standardize integrations** across different AI tools

## Official MCP Servers

### Data & Databases

#### **PostgreSQL**
```json
{
  "postgres": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://user:password@localhost/dbname"],
    "description": "Direct PostgreSQL database access"
  }
}
```
**Use cases:**
- Query databases directly from Claude
- Analyze data patterns
- Generate reports
- Debug database issues

**Capabilities:**
- Execute SQL queries
- List tables and schemas
- Retrieve table structures
- Insert, update, and delete data

#### **SQLite**
```json
{
  "sqlite": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-sqlite", "/path/to/database.db"],
    "description": "SQLite database integration"
  }
}
```
**Use cases:**
- Local database analysis
- Embedded database management
- Development and testing

### Development Tools

#### **GitHub**
```json
{
  "github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
    },
    "description": "GitHub repository management"
  }
}
```
**Use cases:**
- Create and manage issues
- Review pull requests
- Search repositories
- Analyze commit history
- Manage projects

**Capabilities:**
- Repository operations
- Issue tracking
- PR management
- Code search
- Branch operations

#### **GitLab**
```json
{
  "gitlab": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-gitlab"],
    "env": {
      "GITLAB_PERSONAL_ACCESS_TOKEN": "glpat-your_token_here",
      "GITLAB_API_URL": "https://gitlab.com/api/v4"
    },
    "description": "GitLab integration"
  }
}
```

#### **Git**
```json
{
  "git": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-git", "/path/to/repo"],
    "description": "Local Git repository operations"
  }
}
```
**Use cases:**
- Local repository management
- Commit history analysis
- Branch operations
- Diff viewing

### Web & Search

#### **Brave Search**
```json
{
  "brave-search": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-brave-search"],
    "env": {
      "BRAVE_API_KEY": "your_brave_api_key"
    },
    "description": "Web search capabilities"
  }
}
```
**Use cases:**
- Real-time web search
- Research and fact-checking
- Finding documentation
- Current events and news

**Security Note:** Web search can expose Claude to prompt injection attacks. Use with caution.

#### **Fetch (HTTP)**
```json
{
  "fetch": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-fetch"],
    "description": "HTTP requests to APIs"
  }
}
```
**Use cases:**
- REST API integration
- Webhook testing
- API debugging
- Data fetching

### Browser Automation

#### **Puppeteer**
```json
{
  "puppeteer": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-puppeteer"],
    "description": "Browser automation and testing"
  }
}
```
**Use cases:**
- Website screenshots
- Web scraping
- E2E testing
- Form automation

### File Systems

#### **Filesystem**
```json
{
  "filesystem": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/directory"],
    "description": "Local filesystem access"
  }
}
```
**Use cases:**
- Read/write files
- Directory operations
- File searching
- Batch file processing

**Security:** Restrict to specific directories only.

#### **Google Drive**
```json
{
  "google-drive": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-google-drive"],
    "env": {
      "GOOGLE_CLIENT_ID": "your_client_id",
      "GOOGLE_CLIENT_SECRET": "your_client_secret"
    },
    "description": "Google Drive file access"
  }
}
```

### Productivity & Knowledge

#### **Slack**
```json
{
  "slack": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-slack"],
    "env": {
      "SLACK_BOT_TOKEN": "xoxb-your-token",
      "SLACK_TEAM_ID": "T1234567890"
    },
    "description": "Slack workspace integration"
  }
}
```
**Use cases:**
- Send messages
- Read channels
- Search conversations
- Automate workflows

#### **Notion**
```json
{
  "notion": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-notion"],
    "env": {
      "NOTION_API_KEY": "secret_your_key"
    },
    "description": "Notion workspace integration"
  }
}
```

#### **Obsidian**
```json
{
  "obsidian": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-obsidian"],
    "description": "Obsidian vault integration"
  }
}
```

### Monitoring & Operations

#### **Sentry**
```json
{
  "sentry": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-sentry"],
    "env": {
      "SENTRY_AUTH_TOKEN": "your_auth_token",
      "SENTRY_ORG": "your-org"
    },
    "description": "Error monitoring and debugging"
  }
}
```

#### **Memory (Context Persistence)**
```json
{
  "memory": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-memory"],
    "description": "Persistent memory across sessions"
  }
}
```
**Use cases:**
- Store context between sessions
- Remember user preferences
- Track project state
- Maintain conversation history

## Community MCP Servers

### AI & Machine Learning

- **Raycast AI** - Raycast integration
- **Anthropic** - Direct Claude API access
- **OpenAI** - GPT model access

### Development

- **Docker** - Container management
- **Kubernetes** - K8s cluster operations
- **AWS** - Amazon Web Services integration
- **Azure** - Microsoft Azure services
- **Google Cloud** - GCP integration

### Data Science

- **Pandas** - DataFrame operations
- **NumPy** - Numerical computing
- **Jupyter** - Notebook integration

### Databases

- **MongoDB** - NoSQL database access
- **Redis** - Key-value store operations
- **Elasticsearch** - Search and analytics

## MCP Configuration Best Practices

### 1. Security First

```json
{
  "servers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/safe/directory/only"],
      "description": "Restricted filesystem access"
    }
  }
}
```

**Security Guidelines:**
- ✅ Use environment variables for secrets
- ✅ Restrict filesystem paths to specific directories
- ✅ Use read-only access when possible
- ✅ Audit MCP server code before use
- ❌ Never commit API keys to version control
- ❌ Don't give unrestricted filesystem access

### 2. Environment Variables

Create a `.env` file (add to `.gitignore`):
```bash
# API Keys
BRAVE_API_KEY=your_brave_key_here
GITHUB_PERSONAL_ACCESS_TOKEN=ghp_your_token

# Database Connections
DATABASE_URL=postgresql://user:pass@localhost/db
REDIS_URL=redis://localhost:6379

# Service Tokens
SLACK_BOT_TOKEN=xoxb-your-token
SENTRY_AUTH_TOKEN=your_sentry_token
```

Reference in MCP config:
```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

### 3. Project-Specific Configuration

```
project/
├── .mcp.json              # Project MCP config
├── .env                   # Local environment (gitignored)
├── .env.example           # Template for team
└── CLAUDE.md             # Project context
```

### 4. Team Configuration

```json
{
  "servers": {
    "project-db": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${DATABASE_URL}"],
      "description": "Project database (use .env for connection)"
    },
    "project-github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      },
      "description": "Project GitHub repo"
    }
  }
}
```

Commit `.mcp.json` and `.env.example`, gitignore `.env`.

## Installation & Setup

### Installing MCP Servers

```bash
# Install globally
npm install -g @modelcontextprotocol/server-github
npm install -g @modelcontextprotocol/server-postgres

# Or use npx (recommended - always uses latest)
# No installation needed, specify in .mcp.json
```

### Configuration Locations

**User-level (global):**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/claude/claude_desktop_config.json`

**Project-level:**
- Create `.mcp.json` in project root
- Claude Code auto-detects and merges with user config

### Testing Configuration

```bash
# Test MCP connections
claude --mcp-debug

# View active MCP servers
claude --list-mcp-servers

# Test specific server
claude --test-mcp postgres
```

## Common MCP Patterns

### Pattern 1: Development Workflow
```json
{
  "servers": {
    "project-files": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/project"],
      "description": "Project filesystem"
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {"GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"}
    },
    "database": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${DEV_DB_URL}"]
    }
  }
}
```

### Pattern 2: Research & Documentation
```json
{
  "servers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {"BRAVE_API_KEY": "${BRAVE_KEY}"}
    },
    "obsidian": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-obsidian"]
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    }
  }
}
```

### Pattern 3: DevOps & Monitoring
```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {"GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"}
    },
    "sentry": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sentry"],
      "env": {
        "SENTRY_AUTH_TOKEN": "${SENTRY_TOKEN}",
        "SENTRY_ORG": "${SENTRY_ORG}"
      }
    },
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "${SLACK_TOKEN}",
        "SLACK_TEAM_ID": "${SLACK_TEAM}"
      }
    }
  }
}
```

## Troubleshooting

### Common Issues

**MCP server not found:**
```bash
# Solution: Use npx with -y flag
"args": ["-y", "@modelcontextprotocol/server-github"]
```

**Authentication failures:**
- Verify environment variables are set
- Check token permissions
- Ensure `.env` file is loaded

**Connection timeouts:**
- Check network connectivity
- Verify service URLs
- Test credentials manually

**Permission denied:**
- Check filesystem paths
- Verify directory permissions
- Ensure tokens have required scopes

### Debug Mode

```bash
# Enable debug logging
export MCP_DEBUG=1
claude --mcp-debug

# View detailed logs
claude --mcp-logs
```

## Security Considerations

### Risk Assessment

**LOW RISK:**
- ✅ Local filesystem (restricted paths)
- ✅ Git operations (local repos)
- ✅ Memory server (local storage)

**MEDIUM RISK:**
- ⚠️ Database access (read-only recommended)
- ⚠️ GitHub/GitLab (scope tokens appropriately)
- ⚠️ Internal APIs (authenticate properly)

**HIGH RISK:**
- 🔴 Web search (prompt injection risk)
- 🔴 Browser automation (security implications)
- 🔴 Fetch/HTTP (unrestricted access)

### Prompt Injection Protection

When using web search or fetch MCP servers:
- Validate and sanitize inputs
- Use allowlists for domains
- Review outputs before taking action
- Be cautious with automated actions

> **Official Warning:** "Use third party MCP servers at your own risk. Make sure you trust the MCP servers, and be especially careful when using MCP servers that talk to the internet, as these can expose you to prompt injection risk." - Anthropic

## Creating Custom MCP Servers

### Basic MCP Server Structure

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  {
    name: "my-custom-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);

// Define tools
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "my_tool",
        description: "What this tool does",
        inputSchema: {
          type: "object",
          properties: {
            param: { type: "string" }
          }
        }
      }
    ]
  };
});

// Handle tool calls
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  // Implement tool logic
});

const transport = new StdioServerTransport();
await server.connect(transport);
```

### Publishing Custom MCP Servers

1. Create npm package
2. Implement MCP SDK interfaces
3. Test locally
4. Publish to npm
5. Document usage

See [MCP Documentation](https://modelcontextprotocol.io/) for full guide.

## Resources

### Official Documentation
- [MCP Protocol Specification](https://modelcontextprotocol.io/)
- [Anthropic MCP Guide](https://docs.anthropic.com/en/docs/build-with-claude/mcp)
- [MCP Server SDK](https://github.com/modelcontextprotocol/sdk)

### Community
- [MCP Servers Registry](https://github.com/modelcontextprotocol/servers)
- [Community Servers List](https://github.com/topics/mcp-server)
- [MCP Discussions](https://github.com/modelcontextprotocol/discussions)

### Examples
- [Example MCP Servers](https://github.com/modelcontextprotocol/examples)
- [Template MCP Server](../../templates/claude-code/mcp-config-template.json)

---

*MCP enables Claude to be more than an assistant - it becomes an integrated part of your development workflow.*
