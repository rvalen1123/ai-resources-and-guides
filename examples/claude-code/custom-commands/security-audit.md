---
name: security-audit
description: Comprehensive security review using multiple expert perspectives
---

Perform a comprehensive security audit of: "$ARGUMENTS"

Deploy 3 security-focused subagents in parallel:

1. **Vulnerability Scanner**: Check for OWASP Top 10 issues, injection attacks, and common security flaws
2. **Auth Specialist**: Review authentication, authorization, and session management
3. **Data Guardian**: Analyze data handling, encryption, and privacy compliance

Each agent should provide specific findings with line numbers and severity ratings. Consolidate into a prioritized security report.

Usage: `/security-audit "authentication endpoints in src/auth/"`
