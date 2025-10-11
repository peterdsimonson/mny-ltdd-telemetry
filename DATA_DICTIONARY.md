# DATA DICTIONARY — mny-ltdd-telemetry

**Schema versioning:** All artifacts include `schema_version`. Increment when fields change.

## 1) history/workflow-runs/YYYY/YYYY-MM-DD/run-<id>.json

- `schema_version` (string) — e.g., `"1.0.0"`.
- `period` (string) — `"pre-nightly"` or `"post-nightly"`.
- `source_repo` (string) — `"owner/repo"`.
- `run_id` (number) — GitHub Actions run ID.
- `run_number` (number) — Run number within repo.
- `workflow_id` (number) — ID of the workflow definition.
- `workflow_name` (string|null) — Workflow display name.
- `event` (string) — Trigger (e.g., `pull_request`, `push`, `schedule`).
- `status` (string) — `queued|in_progress|completed`.
- `conclusion` (string|null) — `success|failure|cancelled|skipped|null`.
- `actor` (string|null) — Login of triggering user/bot (may be anonymized).
- `head_branch` (string|null)
- `head_sha` (string)
- `created_at` (ISO8601 string)
- `updated_at` (ISO8601 string)
- `duration_ms` (number) — `(updated_at - created_at) * 1000`.
- `instant_failure` (boolean) — `conclusion=failure` and `duration<10s`.
- `artifacts_url` (string)
- `logs_url` (string)
- `html_url` (string)

## 2) daily/workflow-runs/YYYY/YYYY-MM-DD/summary.json

- `schema_version` (string)
- `period` (string)
- `source_repo` (string)
- `day` (YYYY-MM-DD string)
- `totals.runs` (number)
- `totals.failures` (number)
- `totals.instant_failures` (number)
- `totals.success` (number)
- `status_breakdown[]` — array of `{ conclusion: string|null, count: number }`
- `example_run_ids[]` — up to 5 run IDs for inspection

## 3) daily/capabilities/YYYY/YYYY-MM-DD/\*.json

_(Produced by nightly preview tests; used for regression rates)_

- `schema_version` (string)
- `day` (string)
- `contracts_total` (number)
- `violations_total` (number)
- `contracts[]` — `{ id, name, passed: boolean, violations: string[] }`

## 4) daily/pr-metrics/YYYY/YYYY-MM-DD/\*.json

- `schema_version` (string)
- `day` (string)
- `prs[]` — per-PR metrics:
  - `number` (number)
  - `ai_assisted` (boolean)
  - `first_commit_time` (ISO string)
  - `first_success_status_time` (ISO string|null)
  - `time_to_green_minutes` (number|null)

## 5) daily/release-health/YYYY/YYYY-MM-DD/\*.json

- `schema_version` (string)
- `day` (string)
- `service` (string)
- `region` (string)
- `deployed_commit` (string|null)
- `health_ok` (boolean)
- `revision` (string|null)
- `checked_at` (ISO string)

## 6) daily/coverage/YYYY/YYYY-MM-DD/\*.json

- `schema_version` (string)
- `day` (string)
- `contracts_total` (number)
- `covered_contracts` (number)
- `skipped_contracts` (number)
- `waivers[]` — `{ id, expires: ISO string, approved_by: string }`

---

## Anonymization/Privacy

Before pushing:

- Hash usernames (`actor`) using a fixed salt if anonymization is required.
- Redact secrets/URLs from log snippets (if any are added later).

## Provenance

Include `generated_at` timestamps in rollups where feasible. All times are UTC.

## Schema Evolution

When fields change:

1. Increment `schema_version` (e.g., `1.0.0` → `1.1.0` for additions, `2.0.0` for breaking changes)
2. Document changes in `CHANGELOG.md`
3. Update this dictionary
4. Ensure backward compatibility in analysis scripts
