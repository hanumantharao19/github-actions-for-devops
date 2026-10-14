# GitHub Secrets

GitHub Secrets are used to store sensitive information required by GitHub Actions.

Examples:

```text
API tokens
Cloud credentials
Database passwords
Private keys
Access tokens
```

---

## Why Do We Need Secrets?

Never hard-code credentials in workflow files.

Bad:

```yaml
env:
  PASSWORD: mypassword123
```

Anyone with access to the repository may be able to see it.

Instead:

```text
GitHub Secret
      |
      v
GitHub Actions
      |
      v
Workflow
```

---

## Create a Repository Secret

Go to:

```text
GitHub Repository
    |
    v
Settings
    |
    v
Secrets and variables
    |
    v
Actions
    |
    v
Secrets
```

Create:

```text
API_TOKEN
```

with your test value.

---

## Access a Secret

Use:

```yaml
${{ secrets.API_TOKEN }}
```

Example:

```yaml
env:
  API_TOKEN: ${{ secrets.API_TOKEN }}
```

Then use it inside the step:

```yaml
run: |
  if [ -n "$API_TOKEN" ]; then
    echo "API token is configured"
  fi
```

---

## Never Print Secrets

Do NOT do:

```yaml
run: echo "$API_TOKEN"
```

Even though GitHub attempts to mask secrets in logs, workflows should never intentionally print sensitive values.

---

## Real-Time Example

A deployment pipeline might require:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
DATABASE_PASSWORD
API_TOKEN
```

These should be stored as secrets.

Normal configuration such as:

```text
AWS_REGION
APP_NAME
ENVIRONMENT
```

can be stored as variables.

---

## Variables vs Secrets

```text
Configuration
     |
     +---- Repository Variables
     |       |
     |       +-- APP_NAME
     |       +-- AWS_REGION
     |       +-- ENVIRONMENT
     |
     +---- Secrets
             |
             +-- API_TOKEN
             +-- PASSWORD
             +-- CLOUD_CREDENTIALS
```

---

## Security Rule

> If the value must be kept confidential, treat it as a secret.

Never commit credentials directly into Git repositories.
