# Execute Parallel Repository Analysis
## Execute these tasks in parallel

> Variables: REPO_PATH (default: $(pwd)), TARGET_REPO (default: ${REPO_PATH}), MAX_DEPTH (default: 3)
> Execute all agent tasks concurrently for maximum efficiency

TASK 1 - Overview Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-overview`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

TASK 2 - Security Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-security`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

TASK 3 - Accessibility Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-a11y`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

TASK 4 - Performance Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-performance`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

TASK 5 - Code Quality Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-quality`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

TASK 6 - Dependencies Analysis:
- CD `${REPO_PATH}/_project/repo-review/trees/analysis-deps`
- READ `AGENT_PROMPT.md`
- ANALYZE repository at `${TARGET_REPO}` with depth `${MAX_DEPTH}`
- GENERATE `analysis-report.md` and `findings.json`
- LOG metrics to `metrics.json`

MONITOR progress:
- TRACK completion of each task
- LOG timestamps to `${REPO_PATH}/_project/repo-review/reports/execution-metrics.json`