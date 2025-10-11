# MNY LTDD Telemetry Repository

This repository contains research telemetry data for the MNY Platform LTDD (Lock Test Driven Development) system.

## Purpose

This is a **data-only repository** that stores telemetry exported from the main application repository for research purposes. It enables:

- Clean separation between application code and research data
- Long-term storage of telemetry without bloating the main repo
- Easy access for analysis tools and research papers
- Reproducible research dataset with complete audit trail

## Structure

```
history/          # Time-series data (JSONL format)
  scorecard-*.jsonl       # Daily scorecards
  infra-*.jsonl           # Infrastructure health metrics
  capabilities-*.jsonl    # Capability contract violations
  waivers-*.jsonl         # Skip waiver tracking

daily/            # Human-readable daily reports (Markdown)
  YYYY-MM-DD-ltdd-scorecard.md
  YYYY-MM-DD-infra.json
  YYYY-MM-DD-capabilities.json
  YYYY-MM-DD-release-health.json
  YYYY-MM-DD-pr-metrics.json
  YYYY-MM-DD-waiver-debt.json
  YYYY-MM-DD-ai-attribution.json

schema/           # JSON schemas for validation
  scorecard.schema.json
  infra.schema.json
  capabilities.schema.json
```

## Data Sources

All data is automatically exported from:
- **Source Repo:** https://github.com/peterdsimonson/mny-platform
- **Workflow:** `.github/workflows/nightly-scorecard.yml`
- **Frequency:** Nightly at 03:17 UTC
- **Commit Author:** LTDD Telemetry Bot

## Research Use

This dataset supports a publishable research paper on:
- LTDD methodology and effectiveness
- AI-assisted development regression prevention
- Contract-based testing vs traditional testing
- Meta-layer verification (Infrastructure Contracts)

## Data Integrity

- All commits include source SHA and timestamp
- No manual edits (bot-only commits)
- Schema validation before push
- Complete audit trail via git history

## License

Research data only. See main repository for code license.
