# Initialize Parallel Review Worktrees

Create parallel git worktrees for each analysis agent.

## Variables
- REPO_PATH: Path to repository to analyze
- AGENT_COUNT: Number of parallel agents (default: 6)

## Steps

1. Create trees directory structure:
```bash
mkdir -p trees reports
```

2. Set up worktrees for each agent:
```bash
agents=("overview" "security" "a11y" "performance" "quality" "deps")
for agent in "${agents[@]}"; do
  git worktree add "trees/analysis-$agent" -b "analysis/$agent"
done
```

3. Copy agent prompts to each worktree:
```bash
for agent in "${agents[@]}"; do
  cp ".claude/agents/${agent}-agent.md" "trees/analysis-$agent/AGENT_PROMPT.md"
done
```

4. Create shared analysis config:
```bash
cat > trees/analysis.config.json << 'EOF'
{
  "repo_path": "${REPO_PATH}",
  "analysis_date": "$(date -u +%Y-%m-%d)",
  "output_format": "markdown+json",
  "report_sections": [
    "executive_summary",
    "findings",
    "recommendations",
    "metrics"
  ]
}
EOF
```

5. Verify setup:
```bash
git worktree list
echo "✅ Initialized ${#agents[@]} analysis worktrees"
```