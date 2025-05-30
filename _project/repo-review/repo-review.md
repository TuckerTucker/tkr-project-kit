# Parallel Repository Review System

A comprehensive code analysis framework that uses multiple specialized AI agents to review repositories from different perspectives simultaneously.

## Overview

This system leverages git worktrees to enable parallel analysis by six specialized agents:
- **Overview**: Architecture and structure analysis
- **Security**: Vulnerability scanning and security assessment
- **Accessibility**: WCAG compliance and a11y best practices
- **Performance**: Optimization opportunities identification
- **Code Quality**: Technical debt and maintainability assessment
- **Dependencies**: Supply chain and license compliance review

## Quick Start

```bash
# 1. Initialize the review system
/claude rr_init-review

# 2. Execute parallel analysis
/claude rr_execute-review TARGET_REPO=https://github.com/user/repo MAX_DEPTH=3

# 3. Merge findings into comprehensive report
/claude rr_merge-findings
```

## Directory Structure

```
_project/
├── _claude/
│   ├── rr_init-review.md      # Initialize review worktrees
│   ├── rr_execute-review.md   # Execute parallel analysis
│   └── rr_merge-findings.md   # Aggregate results
└── repo-review/
    ├── agents/          # Specialized agent configurations
    ├── templates/       # Report templates and schemas
    ├── trees/           # Git worktrees (created during init)
    └── reports/         # Final analysis reports
```

## Agent Capabilities

### Overview Agent
- Maps system architecture and data flow
- Identifies design patterns and anti-patterns
- Documents technology stack decisions
- Creates architecture diagrams

### Security Agent
- Scans for OWASP Top 10 vulnerabilities
- Checks authentication and authorization
- Reviews dependency vulnerabilities
- Provides remediation recommendations

### Accessibility Agent
- Ensures WCAG 2.1 AA compliance
- Reviews keyboard navigation
- Checks screen reader support
- Validates color contrast ratios

### Performance Agent
- Analyzes bundle sizes and load times
- Identifies query optimization opportunities
- Reviews caching strategies
- Suggests performance improvements

### Code Quality Agent
- Assesses technical debt
- Reviews test coverage
- Checks documentation completeness
- Identifies refactoring opportunities

### Dependencies Agent
- Reviews license compliance
- Checks for security vulnerabilities
- Analyzes dependency health
- Identifies unused dependencies

## Output Formats

Each agent produces:
- `analysis-report.md`: Human-readable findings
- `findings.json`: Structured data following the schema
- `metrics.json`: Analysis metrics and statistics

The merge process creates:
- `executive-summary.md`: High-level overview
- `aggregated-findings.json`: Combined structured data
- Individual agent reports in `reports/agents/`

## Customization

Modify agent behavior by editing files in `_project/repo-review/agents/`
Adjust report formats using templates in `_project/repo-review/templates/`