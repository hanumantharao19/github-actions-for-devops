# GitHub Actions Events

## Objective

Understand events that trigger GitHub Actions workflows.

---

## What is an Event?

An **event** is an activity that causes a GitHub Actions workflow to run.

Example:

```yaml
on:
  push:
```

This means the workflow runs when code is pushed.

---

## Common Events

### Push

```yaml
on:
  push:
```

Runs when code is pushed.

### Pull Request

```yaml
on:
  pull_request:
```

Runs when a pull request event occurs.

### Manual Trigger

```yaml
on:
  workflow_dispatch:
```

Allows a user to manually start the workflow from GitHub.

### Schedule

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

Runs according to a schedule.

---

## Multiple Events

A workflow can respond to multiple events.

```yaml
on:
  push:
  pull_request:
  workflow_dispatch:
```

---

## Important Concept

The event answers:

> **When should my workflow run?**

The job answers:

> **What should my workflow do?**
