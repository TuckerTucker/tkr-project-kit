# Initialize Parallel Review (No Worktrees)
## Execute these tasks

> Variables: REPO_PATH (default: $(pwd))
> Use absolute paths for all commands

CREATE directory structure:
- RUN `mkdir -p ${REPO_PATH}/_project/repo-review/reports/agents/{overview,security,a11y,performance,quality,deps}`
- RUN `mkdir -p ${REPO_PATH}/_project/repo-review/reports/consolidated`

PREPARE agent workspaces:
- SET agents: overview security a11y performance quality deps
- FOR each agent:
  - COPY `${REPO_PATH}/_project/repo-review/agents/${agent}-agent.md` to `${REPO_PATH}/_project/repo-review/reports/agents/$agent/AGENT_PROMPT.md`

CREATE shared config:
- WRITE to `${REPO_PATH}/_project/repo-review/reports/analysis.config.json`:
  ```json
  {
    "repo_path": "${REPO_PATH}",
    "analysis_date": "$(date -u +%Y-%m-%d)",
    "output_format": "markdown+json",
    "report_sections": ["executive_summary", "findings", "recommendations", "metrics"],
    "agents": ["overview", "security", "a11y", "performance", "quality", "deps"]
  }
  ```

VERIFY setup:
- RUN `ls -la ${REPO_PATH}/_project/repo-review/reports/agents/`
- CONFIRM 6 agent directories created with AGENT_PROMPT.md files