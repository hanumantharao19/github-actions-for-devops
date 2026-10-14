# Scheduled Workflows

## Objective

Learn how to automatically run GitHub Actions workflows using cron schedules.

---

## What is a Scheduled Workflow?

A scheduled workflow runs automatically according to a defined schedule.

Example:

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

---

## Cron

Cron uses five fields:

```text
minute hour day-of-month month day-of-week
```

Example:

```text
0 0 * * *
```

Means:

> Run every day at 00:00 UTC.

---

## Examples

Every day:

```text
0 0 * * *
```

Every Monday:

```text
0 0 * * 1
```

Every hour:

```text
0 * * * *
```

---

## Real-Time Uses

Scheduled workflows can be used for:

* Scheduled testing
* Dependency checks
* Security scans
* Cleanup jobs
* Reports
* Infrastructure checks

---

## Important

GitHub Actions cron schedules use **UTC**.

Therefore, convert your required local time to UTC when creating the schedule.
