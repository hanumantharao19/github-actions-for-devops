# Environment Variables

Environment variables allow us to pass configuration values to workflow jobs and steps.

## Example

```yaml
env:
  APP_NAME: product-service
  ENVIRONMENT: dev
```

Inside a shell command:

```yaml
run: echo "$APP_NAME"
```

---

## Variable Scope

GitHub Actions supports different scopes.

```text
Workflow
   |
   +-- Job
         |
         +-- Step
```

### Workflow Level

```yaml
env:
  APP_NAME: product-service
```

Available throughout the workflow.

### Job Level

```yaml
jobs:
  build:
    env:
      VERSION: "1.0"
```

Available to all steps in that job.

### Step Level

```yaml
steps:

  - name: Build
    env:
      BUILD_NUMBER: "100"
    run: echo "$BUILD_NUMBER"
```

Available only to that step.

---

## Real-Time DevOps Usage

For example:

```text
APP_NAME = product-service
ENVIRONMENT = dev
VERSION = 1.0
```

A CI/CD pipeline can use these values during:

```text
Build
  |
Test
  |
Docker Build
  |
Deployment
```

For sensitive values, use **GitHub Secrets** instead of normal environment variables.
