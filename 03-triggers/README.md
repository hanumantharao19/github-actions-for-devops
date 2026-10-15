# GitHub Actions – Triggers

## 1. What Is a Trigger?

A **trigger** determines when a GitHub Actions workflow runs.

Common triggers include pushing code, creating a pull request, manually starting a workflow, or running it on a schedule.

## 2. Push Trigger

Runs a workflow when code is pushed to a repository.

```yaml
on:
  push:
```

To run only when code is pushed to `main`:

```yaml
on:
  push:
    branches:
      - main
```

**Use case:** Run CI checks after a developer pushes code.

## 3. Pull Request Trigger

Runs a workflow when a pull request event occurs.

```yaml
on:
  pull_request:
    branches:
      - main
```

This targets pull requests whose base branch is `main`.

**Use case:** Run tests and code-quality checks before merging code.

## 4. Manual Trigger — `workflow_dispatch`

Allows a user to start a workflow manually from GitHub Actions.

```yaml
on:
  workflow_dispatch:
```

You can also accept inputs:

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Choose environment"
        required: true
        type: choice
        options:
          - dev
          - qa
          - prod
```

**Use case:** Manually trigger deployments or infrastructure changes.

## 5. Scheduled Trigger — `schedule`

Runs a workflow according to a cron expression.

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

This example runs daily at midnight UTC.

Common cron examples:

| Cron | Meaning |
|---|---|
| `0 0 * * *` | Every day at midnight UTC |
| `0 * * * *` | Every hour |
| `0 0 * * 1` | Every Monday at midnight UTC |

**Use case:** Run scheduled security scans, cleanup jobs, or reports.

## 6. Path Filters

Path filters control whether a workflow runs based on which files change.

```yaml
on:
  push:
    paths:
      - "app/**"
      - "*.yml"
```

The workflow runs for pushes that change files matching these patterns.

To exclude specific paths, use `paths-ignore`:

```yaml
on:
  push:
    paths-ignore:
      - "docs/**"
```

**Use case:** Run application tests only when relevant application files change.

Note: `paths` and `paths-ignore` cannot be used together for the same event.

## 7. Branch Filters

Branch filters control which branches trigger a workflow.

Include specific branches:

```yaml
on:
  push:
    branches:
      - main
      - develop
```

Exclude branches:

```yaml
on:
  push:
    branches-ignore:
      - "feature/**"
```

**Use case:** Run CI on development branches and production deployment workflows on `main`.

Note: `branches` and `branches-ignore` cannot be used together for the same event.

## 8. Quick Summary

| Trigger | Purpose |
|---|---|
| `push` | Run after code is pushed |
| `pull_request` | Run for pull request events |
| `workflow_dispatch` | Start manually |
| `schedule` | Run on a schedule |
| `paths` | Filter by changed files |
| `branches` | Filter by branch name |

**Remember:** Triggers define *when* a workflow runs. Jobs and steps define *what* it does.

## 9. Practice

1. Create a workflow that runs only on pushes to `main`.
2. Create a workflow that runs for pull requests targeting `main`.
3. Add a manual trigger.
4. Schedule a workflow to run daily.
5. Configure a workflow to run only when files under `app/` change.
6. Configure a workflow to run on `main` and `develop`.

