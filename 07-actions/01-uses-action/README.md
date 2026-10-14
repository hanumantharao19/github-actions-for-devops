# Using GitHub Actions with `uses`

GitHub Actions allows workflows to use reusable actions.

The syntax is:

```yaml
uses: owner/repository@version
```

Example:

```yaml
uses: actions/checkout@v4
```

---

## `run` vs `uses`

`run` executes a command:

```yaml
- name: Show directory
  run: pwd
```

`uses` runs an existing action:

```yaml
- name: Checkout repository
  uses: actions/checkout@v4
```

---

## Action Structure

```text
owner/repository@version
```

Example:

```text
actions/checkout@v4
```

| Part       | Value      |
| ---------- | ---------- |
| Owner      | `actions`  |
| Repository | `checkout` |
| Version    | `v4`       |

---

## Why Use Actions?

Actions provide reusable functionality.

Instead of writing all the logic ourselves, we can use existing actions for common tasks.

Examples:

```text
Checkout code
Setup Node.js
Setup Python
Configure AWS
Login to Docker
Upload artifacts
Run security scans
```

---

## Important

An action is normally used as a workflow step:

```yaml
steps:

  - name: Use action
    uses: owner/repository@version
```
