# Repository Variables

Repository variables allow us to store reusable configuration values in GitHub repository settings.

Instead of hard-coding configuration inside a workflow:

```yaml
AWS_REGION: ap-south-1
```

we can store it in GitHub.

---

## Where to Create Variables

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
Variables
```

Create variables such as:

```text
APP_NAME       = product-service
ENVIRONMENT    = dev
AWS_REGION     = ap-south-1
```

---

## Using Repository Variables

GitHub Actions uses:

```yaml
${{ vars.VARIABLE_NAME }}
```

Example:

```yaml
run: echo "${{ vars.APP_NAME }}"
```

Example:

```yaml
run: |
  echo "Application: ${{ vars.APP_NAME }}"
  echo "Environment: ${{ vars.ENVIRONMENT }}"
  echo "Region: ${{ vars.AWS_REGION }}"
```

---

## Why Use Repository Variables?

Without repository variables:

```yaml
run: echo "Deploying product-service to ap-south-1"
```

With repository variables:

```yaml
run: |
  echo "Deploying ${{ vars.APP_NAME }}"
  echo "Region: ${{ vars.AWS_REGION }}"
```

This makes the workflow easier to maintain.

---

## Variables vs Hard-Coded Values

```text
Hard-coded
    |
    +-- Difficult to change
    +-- Configuration mixed with workflow logic

Repository Variables
    |
    +-- Centralized configuration
    +-- Easier maintenance
    +-- Reusable
```

---

## Important

Repository variables are for normal configuration.

Do not store passwords or credentials as repository variables.

For sensitive information, use **GitHub Secrets**.
