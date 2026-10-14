# Environment Variables

## Objective

Learn how to define and use environment variables in GitHub Actions.

---

## What is an Environment Variable?

An environment variable is a key-value pair that stores information that can be used by commands and applications.

Example:

```text
APP_NAME=product-service
ENVIRONMENT=dev
```

---

## Define Variables

Variables can be defined using `env`.

```yaml
env:
  APP_NAME: product-service
  ENVIRONMENT: dev
```

They can be used in commands:

```yaml
run: echo "$APP_NAME"
```

---

## Variable Levels

Environment variables can be defined at different levels.

### Workflow Level

Available to the entire workflow.

```yaml
env:
  APP_NAME: product-service
```

### Job Level

Available to a particular job.

```yaml
jobs:
  build:
    env:
      ENVIRONMENT: dev
```

### Step Level

Available only to one step.

```yaml
- name: Build
  env:
    VERSION: "1.0"
  run: echo "$VERSION"
```

---

## Real-Time Example

```text
Workflow
   |
   +-- APP_NAME
   |
   +-- Job
        |
        +-- ENVIRONMENT
        |
        +-- Step
             |
             +-- VERSION
```

---

## Environment Variables vs Secrets

Normal configuration:

```text
APP_NAME=product-service
ENVIRONMENT=dev
```

Sensitive information should not be stored as plain environment variables.

Examples of sensitive information:

```text
Passwords
API keys
Tokens
Cloud credentials
Private keys
```

Those should be stored using GitHub Secrets.

We will learn GitHub Secrets in the next section.

---

## Important

Environment variables store configuration values.

Secrets should be used for sensitive information.
