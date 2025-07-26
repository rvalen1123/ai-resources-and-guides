---
name: debug-squad
description: Deploy 3 specialized debugging subagents in parallel
---

Deploy 3 specialized subagents to debug this issue: "$ARGUMENTS"

1. **Bug Hunter**: Systematically trace the bug through the codebase using search and analysis
2. **Log Detective**: Analyze logs, error messages, and execution flow
3. **Solution Architect**: Propose multiple fix approaches with trade-offs

Each subagent should work in parallel and report back their findings. Then synthesize the results into a clear debugging plan.

Usage: `/debug-squad "User login fails after password reset"`
