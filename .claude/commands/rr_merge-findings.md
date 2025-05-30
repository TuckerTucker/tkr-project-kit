# Merge and Aggregate Analysis Findings

Combine all agent findings into comprehensive reports.

## Steps

1. Collect all findings:
```bash
echo "📊 Collecting analysis results..."
mkdir -p reports/agents

for agent in overview security a11y performance quality deps; do
  if [ -f "trees/analysis-$agent/findings.json" ]; then
    cp "trees/analysis-$agent/findings.json" "reports/agents/${agent}-findings.json"
    cp "trees/analysis-$agent/analysis-report.md" "reports/agents/${agent}-report.md"
  fi
done
```

2. Aggregate JSON findings:
```bash
cd reports
cat agents/*-findings.json | jq -s '
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
' > aggregated-findings.json
```

3. Generate executive summary:
```bash
cat > executive-summary.md << 'EOF'
# Repository Analysis Executive Summary

## Overview
Generated: $(date)
Repository: ${TARGET_REPO}

## Key Findings Summary
[Parse aggregated-findings.json and summarize]

## Priority Actions
[Extract top recommendations across all agents]

## Individual Reports
- [Overview Analysis](agents/overview-report.md)
- [Security Analysis](agents/security-report.md)
- [Accessibility Analysis](agents/a11y-report.md)
- [Performance Analysis](agents/performance-report.md)
- [Code Quality Analysis](agents/quality-report.md)
- [Dependencies Analysis](agents/deps-report.md)
EOF
```

4. Create visual dashboard:
```bash
# Generate HTML dashboard with charts
# Could be a separate artifact if needed
```

5. Clean up worktrees (optional):
```bash
read -p "Remove analysis worktrees? (y/n) " -n 1 -r
if [[ $REPLY =~ ^[Yy]$ ]]; then
  for agent in overview security a11y performance quality deps; do
    git worktree remove "trees/analysis-$agent"
  done
fi
```