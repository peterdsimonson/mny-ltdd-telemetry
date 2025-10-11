# Research Data Sources

This directory contains daily LTDD scorecards (human-readable).

For machine-readable data, see `../telemetry/scorecards/*.jsonl`.

## Format

Each scorecard documents:

- Quality metrics (CI runs, failures, capability violations)
- Delivery metrics (PRs merged, lead time)
- Waiver debt (active/expired waivers)
- Production health (deployed commit, health status)
- AI attribution (AI vs human commits)

## Research Use

These daily snapshots provide:

- Time-series data for trend analysis
- Evidence of LTDD effectiveness
- Regression prevention metrics
- Waiver debt reduction over time
