# PR Merge Quality and Prow E2E Compliance Dashboard

This repository contains a Grafana dashboard JSON export that tracks merged PR
quality against OpenShift CI (Prow) E2E jobs and override usage.

## Files

- `pr-e2e-workflow-openshift-ci-dashboard.json`: Grafana dashboard export.

## Dashboard Overview

The dashboard:

- Compares merged PRs with and without a passing Prow E2E job.
- Counts merged PRs that include `/override` comments.
- Provides drilldowns to view PRs by outcome and override usage.

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

## Importing into Grafana

1. Open Grafana and go to **Dashboards → Import**.
2. Upload `pr-e2e-workflow-openshift-ci-dashboard.json`.
3. Map the `mysql` datasource to your DevLake database.
4. Save the dashboard.

## Notes

- The dashboard expects DevLake schema and data to be present in MySQL.
- The `/override` detection is case-insensitive and matches comment bodies.
