# Merge and Aggregate Analysis Findings
## Execute these tasks

> Variables: REPO_PATH (default: $(pwd))
> Consolidate all agent findings into unified reports

COLLECT findings from all agents:
- RUN `mkdir -p ${REPO_PATH}/_project/repo-review/reports/agents`
- FOR each agent in [overview security a11y performance quality deps]:
  - IF exists `${REPO_PATH}/_project/repo-review/trees/analysis-$agent/findings.json`:
    - COPY to `${REPO_PATH}/_project/repo-review/reports/agents/${agent}-findings.json`
    - COPY `analysis-report.md` to `${REPO_PATH}/_project/repo-review/reports/agents/${agent}-report.md`

AGGREGATE JSON findings:
- CD `${REPO_PATH}/_project/repo-review/reports`
- RUN jq aggregation on `agents/*-findings.json`:
  ```jq
  {
    analysis_date: .[0].analysis_date,
    repository: .[0].repository,
    summary: {
      total_issues: [.[] | .findings[].severity] | length,
      critical: [.[] | .findings[] | select(.severity == "critical")] | length,
      high: [.[] | .findings[] | select(.severity == "high")] | length,
      medium: [.[] | .findings[] | select(.severity == "medium")] | length,
      low: [.[] | .findings[] | select(.severity == "low")] | length
    },
    findings_by_agent: [.[] | {(.agent_type): .findings}] | add,
    recommendations: [.[] | .recommendations[]] | unique
  }
  ```
- WRITE output to `aggregated-findings.json`

GENERATE executive summary:
- CREATE `${REPO_PATH}/_project/repo-review/reports/executive-summary.md`:
  - ADD header with date and repository
  - PARSE `aggregated-findings.json` for key metrics
  - EXTRACT top priority recommendations
  - LINK to individual agent reports

CREATE visual artifacts (optional):
- GENERATE charts from aggregated data in `${REPO_PATH}/_project/repo-review/reports/`
- CREATE HTML dashboard if needed

CLEANUP worktrees (interactive):
- PROMPT "Remove analysis worktrees? (y/n)"
- IF yes:
  - FOR each agent:
    - RUN `git worktree remove ${REPO_PATH}/_project/repo-review/trees/analysis-$agent`