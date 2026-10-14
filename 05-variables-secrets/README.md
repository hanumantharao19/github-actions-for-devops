# 05 - Variables and Secrets

GitHub Actions workflows often need configuration values such as:

* Application name
* Environment name
* Version
* AWS region
* GCP project ID
* Docker image name
* API tokens
* Cloud credentials
* GitHub repository information

GitHub Actions provides different ways to manage these values.

## Learning Flow

```text
Variables and Secrets
        |
        +-- Environment Variables
        |
        +-- Repository Variables
        |
        +-- Secrets
        |
        +-- GitHub Context
```

---

## 1. Environment Variables

Environment variables store configuration values that can be used by workflow commands.

Example:

```yaml
env:
  APP_NAME: product-service
  ENVIRONMENT: dev
```

They can be accessed inside a shell command:

```yaml
run: echo "Application: $APP_NAME"
```

Environment variables can be defined at different levels:

```text
Workflow
   |
   +-- Job
   |     |
   |     +-- Step
   |
   +-- Job
```

Example:

```yaml
env:
  APP_NAME: product-service

jobs:

  build:
    env:
      ENVIRONMENT: dev

    steps:

      - name: Build
        env:
          VERSION: "1.0"
        run: |
          echo "$APP_NAME"
          echo "$ENVIRONMENT"
          echo "$VERSION"
```

---

# 2. Repository Variables

Repository variables are configuration values stored in the GitHub repository settings.

Example:

```text
APP_NAME = product-service
AWS_REGION = ap-south-1
```

They can be accessed using:

```yaml
${{ vars.APP_NAME }}
```

Example:

```yaml
run: echo "Application: ${{ vars.APP_NAME }}"
```

Repository variables are useful when configuration should not be hard-coded inside workflow files.

---

# 3. Secrets

Secrets are used for sensitive information.

Examples:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
GCP_SERVICE_ACCOUNT
API_TOKEN
DATABASE_PASSWORD
```

Secrets should NOT be written directly inside workflow YAML.

Bad:

```yaml
run: echo "password123"
```

Instead, store the value in GitHub Secrets and reference it:

```yaml
${{ secrets.DATABASE_PASSWORD }}
```

Example:

```yaml
env:
  DATABASE_PASSWORD: ${{ secrets.DATABASE_PASSWORD }}
```

GitHub masks secrets in workflow logs when they are used normally.

---

# 4. GitHub Context

GitHub automatically provides information about the workflow execution.

Examples:

```yaml
${{ github.repository }}
${{ github.ref }}
${{ github.sha }}
${{ github.actor }}
${{ github.event_name }}
```

For example:

```yaml
run: echo "Repository: ${{ github.repository }}"
```

This allows workflows to dynamically understand:

* Which repository triggered the workflow
* Which branch triggered it
* Which commit triggered it
* Which user triggered it
* Which event triggered it

---

# Variables vs Secrets

| Feature                   | Variables          | Secrets               |
| ------------------------- | ------------------ | --------------------- |
| Normal configuration      | Yes                | No                    |
| Sensitive information     | No                 | Yes                   |
| Example                   | AWS region         | AWS password          |
| Access syntax             | `${{ vars.NAME }}` | `${{ secrets.NAME }}` |
| Stored in GitHub          | Yes                | Yes                   |
| Should be printed in logs | Usually okay       | No                    |

---

# Real-Time DevOps Example

Consider a deployment pipeline:

```text
Developer
    |
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +--------------------+
    |                    |
    v                    v
Repository Variables   Secrets
    |                    |
    |                    +-- Cloud credentials
    |                    +-- API tokens
    |
    +-- Environment
    +-- Region
    +-- Application name
    |
    v
Build
    |
    v
Test
    |
    v
Deploy
```

For example:

```text
Repository Variable
    AWS_REGION = ap-south-1

Secret
    AWS_ACCESS_KEY_ID = ********
    AWS_SECRET_ACCESS_KEY = ********
```

The workflow can use both without hard-coding them.

---

# Important Security Rules

Never commit sensitive information to Git:

```text
Passwords
API keys
Cloud credentials
Private keys
Database credentials
Access tokens
```

Do not do this:

```yaml
env:
  PASSWORD: mypassword123
```

Use a GitHub Secret instead:

```yaml
env:
  PASSWORD: ${{ secrets.PASSWORD }}
```

---

# Learning Order

Learn these topics in this order:

```text
01-environment-variables
        |
        v
02-repository-variables
        |
        v
03-secrets
        |
        v
04-github-context
```

This section prepares you for the next topics:

```text
Variables & Secrets
        |
        v
Expressions & Conditions
        |
        v
Actions
        |
        v
CI/CD
        |
        v
Cloud Deployment
```
