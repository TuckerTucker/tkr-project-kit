# Initialize Parallel Review Worktrees
## Execute these tasks

> Variables: REPO_PATH (default: $(pwd))
> Use absolute paths for all commands

CREATE directory structure:
- RUN `mkdir -p ${REPO_PATH}/_project/repo-review/trees ${REPO_PATH}/_project/repo-review/reports`

CREATE worktrees for each agent:
- SET agents: overview security a11y performance quality deps
- FOR each agent:
  - RUN `git worktree add -b analysis/$agent ${REPO_PATH}/_project/repo-review/trees/analysis-$agent`

DEPLOY agent prompts:
- FOR each agent:
  - COPY `${REPO_PATH}/_project/repo-review/agents/${agent}-agent.md` to `${REPO_PATH}/_project/repo-review/trees/analysis-$agent/AGENT_PROMPT.md`

CREATE shared config:
- WRITE to `${REPO_PATH}/_project/repo-review/trees/analysis.config.json`:
  ```json
  {
    "repo_path": "${REPO_PATH}",
    "analysis_date": "$(date -u +%Y-%m-%d)",
    "output_format": "markdown+json",
    "report_sections": ["executive_summary", "findings", "recommendations", "metrics"]
  }
  ```

VERIFY setup:
- RUN `git worktree list`
- CONFIRM 6 worktrees created in `${REPO_PATH}/_project/repo-review/trees/`