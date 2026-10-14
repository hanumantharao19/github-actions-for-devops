# GitHub Actions Jobs

## Objective

Understand jobs in GitHub Actions.

---

## What is a Job?

A **job** is a group of steps that execute together on a runner.

Example:

```yaml
jobs:
  build:
```

A workflow can contain multiple jobs.

---

## Multiple Jobs

Example:

```text
Workflow
   |
   +---- Build Job
   |
   +---- Test Job
   |
   +---- Deploy Job
```

Each job can have its own runner and steps.

---

## Example

```yaml
jobs:

  build:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Building application"

  test:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Testing application"
```

By default, independent jobs can run in parallel.

---

## Important

A job contains:

```text
Job
 |
 +-- Runner
 |
 +-- Steps
```

Example:

```yaml
build:
  runs-on: ubuntu-latest

  steps:
    - run: echo "Build"
```
