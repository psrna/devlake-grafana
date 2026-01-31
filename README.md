# PR Merge Quality and Prow E2E Compliance Dashboard

This repository contains a Grafana dashboard JSON export that tracks merged PR
quality against OpenShift CI (Prow) E2E jobs and override usage.

## Files

- `pr-e2e-workflow-openshift-ci-dashboard.json`: Main Grafana dashboard export.
- `merged-prs-openshift-ci-daily.json`: Focused dashboard for daily merged PRs vs
  OpenShift CI success rate with drilldown table.

## Dashboard Overview

The dashboard:

- Compares merged PRs with and without a passing Prow E2E job.
- Counts merged PRs that include `/override` comments.
- Provides drilldowns to view PRs by outcome and override usage.

The daily drilldown dashboard:

- Plots daily merged PRs and daily OpenShift CI success rate (excluding aborted).
- Uses Job Name and Event Type filters for OpenShift CI jobs.
- Provides a click-through table of PRs merged on a selected day.

## Data Sources

- Grafana datasource: `mysql`
- Tables referenced: `lake.pull_requests`, `lake.pull_request_commits`,
  `lake.pull_request_comments`, `lake.ci_test_jobs`, `lake.repos`

## Variables

- `repo_id`: GitHub repo IDs (multi-select)
- `base_ref`: merge target branches (regex)
- `e2e_pattern`: substring for Prow job name match
- `override_check`: substring for `/override` comment match
- `bot_accounts`: comma-separated GitHub logins to exclude
- `bot_author_ids`: comma-separated author IDs to exclude
- `exclude_merged_by_ids`: comma-separated merged-by IDs to exclude
- `job_name`: OpenShift CI job name filter (multi-select, daily dashboard)
- `event_type`: OpenShift CI event type filter (multi-select, daily dashboard)
- `drill_day`: hidden day selector for drilldown table (daily dashboard)

## Importing into Grafana

1. Open Grafana and go to **Dashboards → Import**.
2. Upload `pr-e2e-workflow-openshift-ci-dashboard.json` or
   `merged-prs-openshift-ci-daily.json`.
3. Map the `mysql` datasource to your DevLake database.
4. Save the dashboard.

## Notes

- The dashboard expects DevLake schema and data to be present in MySQL.
- The `/override` detection is case-insensitive and matches comment bodies.
