# LTDD Scorecard — ${DATE}

**Generated:** $(date -u +"%Y-%m-%d %H:%M:%S UTC")  
**Purpose:** Research telemetry for publishable LTDD paper

---

## 📊 Quality & Stability (last 24h)

- **CI runs:** ${total_runs}
- **Instant infra failures (<10s):** ${fast_fails}
- **Capability Matrix failed specs:** ${caps_failed}
- **Coverage Guard failures:** ${cov_failures}

## 🚀 Delivery Metrics

- **PRs merged (24h):** ${pr_total}
- **Total commits (24h):** ${total_commits}
- **AI-assisted commits:** ${ai_commits} ($(echo "scale=0; ${ai_commits} * 100 / (${total_commits} + 1)" | bc)%)

## 🔒 Waiver Debt

- **Active waivers:** ${waiver_count}
- **Expired waivers:** ${waiver_expired}

## 🏥 Production Health

- **Health endpoint:** ${health_ok}
- **Deployed commit:** ${health_commit}

---

## 📁 Research Data Sources

- \`telemetry/scorecards/${DATE}.jsonl\` (machine-readable)
- \`telemetry/daily/infra.json\` (workflow health)
- \`telemetry/daily/coverage.json\` (coverage guard)
- \`telemetry/daily/capabilities.json\` (capability matrix)
- \`telemetry/daily/release-health.json\` (production snapshot)
- \`telemetry/daily/pr-metrics.json\` (lead time)
- \`telemetry/daily/waiver-debt.json\` (skip waivers)
- \`telemetry/daily/ai-attribution.json\` (AI vs human commits)

---

**LTDD Status:** $([ ${fast_fails} -eq 0 ] && [ ${cov_failures} -eq 0 ] && [ ${waiver_expired} -eq 0 ] && echo "✅ HEALTHY" || echo "⚠️  DEGRADED")

**Next Scorecard:** $(date -u -d "1 day" +"%Y-%m-%d" 2>/dev/null || date -u -v+1d +"%Y-%m-%d") 03:17 UTC
