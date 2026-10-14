# GitHub Actions Contexts

Contexts provide information about the workflow execution.

They are accessed using expressions.

```text
${{ context.property }}
```

---

# GitHub Context

The `github` context provides GitHub-related information.

Examples:

```yaml
${{ github.repository }}
${{ github.ref_name }}
${{ github.sha }}
${{ github.actor }}
${{ github.event_name }}
```

---

# Environment Context

The `env` context provides environment variables.

Example:

```yaml
env:
  APP_NAME: product-service
```

Access it with:

```yaml
${{ env.APP_NAME }}
```

---

# Variables Context

Repository or organization variables are available through:

```yaml
${{ vars.APP_NAME }}
```

---

# Secrets Context

Secrets are available through:

```yaml
${{ secrets.API_TOKEN }}
```

Never intentionally print secret values.

---

# Job Context

The `job` context provides information about the current job.

---

# Steps Context

The `steps` context can access outputs from previous steps.

Example:

```yaml
steps:
  build:
    id: build

  deploy:
    run: echo "${{ steps.build.outputs.version }}"
```

---

# Needs Context

The `needs` context is used when one job depends on another job.

Example:

```yaml
jobs:

  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Build"

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploy"
```

---

# Common Contexts

```text
github
env
vars
secrets
job
steps
runner
needs
matrix
inputs
```

You do not need to memorize all contexts immediately.

Learn them as you use them in real workflows.

---

# Real-Time Example

```text
GitHub Event
     |
     v
GitHub Context
     |
     +-- Repository
     +-- Branch
     +-- Commit
     +-- Actor
     +-- Event
     |
     v
Expression
     |
     v
Condition
     |
     v
Build / Test / Deploy
```

Contexts are one of the most important concepts for advanced GitHub Actions workflows.
