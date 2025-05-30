# Execute Parallel Repository Analysis

Run all analysis agents in parallel on the target repository.

## Variables
- TARGET_REPO: Repository path or URL to analyze
- MAX_DEPTH: Analysis depth (1-5, default: 3)

## Parallel Execution

For each worktree, execute the corresponding analysis:

### Task Template:
```
cd trees/analysis-{AGENT_NAME}
cat AGENT_PROMPT.md

Analyze the repository at: ${TARGET_REPO}
Analysis depth: ${MAX_DEPTH}

1. Clone/copy the target repository if needed
2. Execute your specialized analysis according to your agent prompt
3. Generate findings in both:
   - Human-readable report: analysis-report.md
   - Structured data: findings.json
4. Create any supporting artifacts (diagrams, charts, etc.)
5. Log analysis metrics: metrics.json
```

## Parallel Tasks:

### Task 1: Overview Analysis
Execute in trees/analysis-overview

### Task 2: Security Analysis  
Execute in trees/analysis-security

### Task 3: Accessibility Analysis
Execute in trees/analysis-a11y

### Task 4: Performance Analysis
Execute in trees/analysis-performance

### Task 5: Code Quality Analysis
Execute in trees/analysis-quality

### Task 6: Dependencies Analysis
Execute in trees/analysis-deps

## Progress Tracking:
Monitor each agent's progress and log completion times.