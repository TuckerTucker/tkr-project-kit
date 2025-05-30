# Execute Parallel Repository Analysis (No Worktrees)
## Execute these tasks in parallel

> Variables: REPO_PATH (default: $(pwd)), TARGET_REPO (default: ${REPO_PATH}), MAX_DEPTH (default: 3)
> Execute all agent tasks concurrently for maximum efficiency
> All agents work on the same repository without creating copies

TASK 1 - Overview Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/overview/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/overview/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

TASK 2 - Security Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/security/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/security/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

TASK 3 - Accessibility Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/a11y/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/a11y/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

TASK 4 - Performance Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/performance/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/performance/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

TASK 5 - Code Quality Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/quality/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/quality/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

TASK 6 - Dependencies Analysis:
- READ `${REPO_PATH}/_project/repo-review/reports/agents/deps/AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- WRITE outputs to `${REPO_PATH}/_project/repo-review/reports/agents/deps/`:
  - `analysis-report.md` (human-readable findings)
  - `findings.json` (structured data)
  - `metrics.json` (analysis metrics)

MONITOR progress:
- TRACK completion of each task
- LOG timestamps to `${REPO_PATH}/_project/repo-review/reports/execution-metrics.json`
- ENSURE all agents complete their analysis before proceeding to merge phase