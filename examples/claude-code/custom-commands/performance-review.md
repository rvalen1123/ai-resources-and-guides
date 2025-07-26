---
name: performance-review
description: Multi-angle performance analysis and optimization recommendations
---

Analyze performance of: "$ARGUMENTS"

Deploy 3 performance-focused subagents in parallel:

1. **Algorithm Analyzer**: Review time/space complexity, identify O(n²) patterns, suggest better algorithms
2. **Resource Monitor**: Check memory usage, database queries, network calls, and caching opportunities  
3. **Bottleneck Hunter**: Profile critical paths, find slow functions, measure actual performance impact

Each agent should provide measurable recommendations with expected performance gains. Create an optimization roadmap prioritized by impact vs effort.

Usage: `/performance-review "user dashboard loading in src/dashboard/"`
