{
  "servers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/directory"],
      "description": "Access to local filesystem"
    },
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "your-brave-api-key-here"
      },
      "description": "Web search capabilities"
    },
    "github": {
      "command": "npx", 
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-github-token-here"
      },
      "description": "GitHub integration for repos, issues, PRs"
    },
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"],
      "description": "Browser automation for screenshots and testing"
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://user:password@localhost/dbname"],
      "description": "PostgreSQL database access"
    }
  }
}

/*
MCP CONFIG TEMPLATE INSTRUCTIONS:

Based on: Official Claude Code MCP Documentation and Tutorials
Warning: "Use third party MCP servers at your own risk. Make sure you trust the MCP servers, and be especially careful when using MCP servers that talk to the internet, as these can expose you to prompt injection risk." - Anthropic Official Documentation

1. SECURITY FIRST:
   - Never commit API keys to version control
   - Use environment variables for sensitive data
   - Consider using .env files with .gitignore

2. COMMON MCP SERVERS:
   
   Web & APIs:
   - brave-search: Web search functionality
   - fetch: HTTP requests to APIs
   - slack: Slack integration
   
   Development:
   - github: Repository management
   - puppeteer: Browser automation
   - sentry: Error monitoring
   
   Data:
   - postgres: PostgreSQL access
   - sqlite: SQLite database
   - redis: Redis key-value store
   
   Productivity:
   - google-drive: Access Google Drive documents
   - notion: Notion workspace integration
   - obsidian: Note-taking app integration

3. SETUP STEPS:
   
   a) Copy this file to your project root as .mcp.json
   
   b) Replace placeholders:
      - API keys with your actual keys or env vars
      - Database URLs with your connection strings
      - File paths with your actual directories
   
   c) Install required MCP servers:
      npm install -g @modelcontextprotocol/server-*
   
   d) Test the connection:
      claude --mcp-debug

4. ENVIRONMENT VARIABLES:
   Create a .env file (and add it to .gitignore):
   
   BRAVE_API_KEY=your_key_here
   GITHUB_PERSONAL_ACCESS_TOKEN=ghp_your_token
   DATABASE_URL=postgresql://user:pass@localhost/db

5. PROJECT-SPECIFIC CONFIG:
   You can also create project-specific .mcp.json files that 
   team members will automatically inherit when working in 
   that directory.

6. DEBUGGING:
   Use the --mcp-debug flag to troubleshoot connection issues:
   claude --mcp-debug

Remove these comments when customizing for your project.
*/
