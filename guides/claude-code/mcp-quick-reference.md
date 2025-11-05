# MCP Servers Quick Reference

> **Fast lookup for common MCP server configurations**

## Essential MCP Servers

### GitHub
```json
{
  "github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
    }
  }
}
```
**Get token:** https://github.com/settings/tokens

### PostgreSQL
```json
{
  "postgres": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-postgres", "${DATABASE_URL}"]
  }
}
```
**Example URL:** `postgresql://user:pass@localhost:5432/dbname`

### Filesystem
```json
{
  "filesystem": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/directory"]
  }
}
```
**Security:** Only grant access to needed directories

### Brave Search
```json
{
  "brave-search": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-brave-search"],
    "env": {
      "BRAVE_API_KEY": "${BRAVE_KEY}"
    }
  }
}
```
**Get key:** https://brave.com/search/api/

### Git
```json
{
  "git": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-git", "/path/to/repo"]
  }
}
```

### Memory
```json
{
  "memory": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-memory"]
  }
}
```
**Use case:** Persistent context across sessions

## Configuration Locations

**User-level (Global):**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/claude/claude_desktop_config.json`

**Project-level:**
- Create `.mcp.json` in project root

## Quick Setup

1. **Create .env file:**
```bash
GITHUB_TOKEN=ghp_your_token
DATABASE_URL=postgresql://user:pass@localhost/db
BRAVE_KEY=your_brave_api_key
```

2. **Add to .gitignore:**
```bash
echo ".env" >> .gitignore
```

3. **Create .env.example for team:**
```bash
GITHUB_TOKEN=your_github_token_here
DATABASE_URL=postgresql://user:pass@localhost/dbname
BRAVE_KEY=your_brave_api_key_here
```

4. **Create .mcp.json:**
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

## Common Combinations

### Web Development Stack
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/project/path"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {"GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"}
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "${DATABASE_URL}"]
    }
  }
}
```

### Research & Documentation
```json
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {"BRAVE_API_KEY": "${BRAVE_KEY}"}
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/documents"]
    }
  }
}
```

### DevOps & Monitoring
```json
{
  "mcpServers": {
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

## Testing Configuration

```bash
# List active MCP servers
claude --list-mcp-servers

# Test MCP connection
claude --mcp-debug

# Test specific server
claude --test-mcp github
```

## Security Checklist

- [ ] Never commit API keys to git
- [ ] Use environment variables for secrets
- [ ] Restrict filesystem access to specific directories
- [ ] Use read-only database connections when possible
- [ ] Audit third-party MCP servers before use
- [ ] Be cautious with web search (prompt injection risk)
- [ ] Review MCP server permissions regularly

## Troubleshooting

**Server not found:**
```json
// Add -y flag to npx
"args": ["-y", "@modelcontextprotocol/server-name"]
```

**Environment variables not working:**
```bash
# Check .env file exists
ls -la .env

# Verify format (no spaces around =)
KEY=value  # correct
KEY = value  # incorrect
```

**Permission denied:**
```bash
# Check file/directory permissions
ls -la /path/to/directory

# Verify database connection
psql "${DATABASE_URL}"
```

## More Information

- [Complete MCP Servers Guide](mcp-servers-guide.md)
- [MCP Config Template](../../templates/claude-code/mcp-config-template.json)
- [Official MCP Documentation](https://modelcontextprotocol.io/)

---

*Quick reference for common scenarios. See full guide for advanced usage.*
