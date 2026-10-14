# Workflow Structure

## Objective

Understand the basic structure of a GitHub Actions workflow.

---

## Workflow Structure

A GitHub Actions workflow generally contains three main sections:

```yaml
name:

on:

jobs:
```

Example:

```yaml
name: My Workflow

on:
  push:

jobs:
  my-job:
    runs-on: ubuntu-latest

    steps:
      - name: Print message
        run: echo "Hello GitHub Actions"
```

---

## 1. `name`

Defines the name of the workflow.

```yaml
name: My Workflow
```

The name is displayed in the GitHub Actions interface.

---

## 2. `on`

Defines the event that triggers the workflow.

```yaml
on:
  push:
```

This workflow runs when code is pushed to GitHub.

---

## 3. `jobs`

Defines the work that the workflow should perform.

```yaml
jobs:
  my-job:
```

A workflow can contain one or multiple jobs.

---

## 4. `runs-on`

Defines the runner where the job executes.

```yaml
runs-on: ubuntu-latest
```

---

## 5. `steps`

Defines the individual tasks inside the job.

```yaml
steps:
  - name: Print message
    run: echo "Hello GitHub Actions"
```

---

## Complete Structure

```text
Workflow
   |
   +-- name
   |
   +-- on
   |
   +-- jobs
        |
        +-- job
             |
             +-- runs-on
             |
             +-- steps
```

## Key Point

Remember:

```text
name → Workflow name

on → When to run

jobs → What work to perform

runs-on → Where to run

steps → Individual tasks
```
