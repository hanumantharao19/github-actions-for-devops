# GitHub Context

GitHub Actions automatically provides information about the current workflow execution.

This information is available through the `github` context.

---

## Basic Syntax

```yaml
${{ github.PROPERTY }}
```

---

## Common GitHub Context Values

| Expression          | Meaning                         |
| ------------------- | ------------------------------- |
| `github.repository` | Repository name                 |
| `github.ref_name`   | Branch or tag name              |
| `github.ref`        | Full Git reference              |
| `github.sha`        | Commit SHA                      |
| `github.actor`      | User who triggered the workflow |
| `github.event_name` | Event that triggered workflow   |
| `github.workflow`   | Workflow name                   |
| `github.job`        | Current job ID                  |

---

## Example

```yaml
run: echo "Repository: ${{ github.repository }}"
```

Example output:

```text
Repository: hanu/github-actions-for-devops
```

Another example:

```yaml
run: echo "Branch: ${{ github.ref_name }}"
```

Output:

```text
Branch: main
```

---

## Why Is GitHub Context Useful?

It allows a workflow to dynamically understand its execution environment.

For example:

```text
Git push
    |
    v
GitHub Actions
    |
    +-- Repository
    +-- Branch
    +-- Commit
    +-- User
    +-- Event
    |
    v
Workflow
```

---

## Real-Time CI/CD Example

Suppose a developer pushes code to:

```text
main
```

GitHub provides:

```text
Repository = company/product-service
Branch     = main
Commit     = abc123...
Actor      = developer
Event      = push
```

The workflow can use this information.

Example:

```yaml
run: |
  echo "Repository: ${{ github.repository }}"
  echo "Branch: ${{ github.ref_name }}"
  echo "Commit: ${{ github.sha }}"
```

---

## GitHub Context vs Repository Variables

These are different concepts.

### GitHub Context

GitHub automatically provides the information:

```yaml
${{ github.repository }}
${{ github.sha }}
${{ github.actor }}
```

### Repository Variables

You create the configuration:

```yaml
${{ vars.APP_NAME }}
${{ vars.AWS_REGION }}
```

### Secrets

You securely store sensitive information:

```yaml
${{ secrets.API_TOKEN }}
```

---

## Important Concept

You will use GitHub context heavily in later topics such as:

```text
Expressions
Conditions
Pull Requests
Branch-based deployments
Reusable workflows
CI/CD
Cloud deployments
```
