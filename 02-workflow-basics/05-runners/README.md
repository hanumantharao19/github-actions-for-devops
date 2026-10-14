# GitHub Actions Runners

## Objective

Understand GitHub Actions runners.

---

## What is a Runner?

A **runner** is the machine that executes a GitHub Actions job.

For example:

```yaml
runs-on: ubuntu-latest
```

This tells GitHub to execute the job on an Ubuntu runner.

---

## GitHub-Hosted Runners

Common GitHub-hosted runners include:

```text
ubuntu-latest
windows-latest
macos-latest
```

Example:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
```

---

## Runner

Think of a runner as:

```text
GitHub Actions
      |
      v
Runner
      |
      +-- Execute commands
      +-- Run scripts
      +-- Run tests
      +-- Build application
```

---

## Why do we need a Runner?

GitHub Actions workflows contain commands.

Those commands need a machine to execute them.

Therefore:

```text
Workflow
   |
   v
Job
   |
   v
Runner
   |
   v
Commands
```

---

## Common Runners

### Ubuntu

```yaml
runs-on: ubuntu-latest
```

### Windows

```yaml
runs-on: windows-latest
```

### macOS

```yaml
runs-on: macos-latest
```

For most DevOps workloads, Ubuntu runners are commonly used.
