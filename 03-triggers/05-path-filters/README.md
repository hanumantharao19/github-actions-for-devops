# Path Filters

## Objective

Run a workflow only when specific files or directories are changed.

---

## Why Path Filters?

Consider a repository:

```text
project/
├── application/
├── terraform/
├── documentation/
└── README.md
```

Suppose we have a Terraform workflow.

We don't want Terraform to run when only documentation changes.

We can use a path filter.

---

## Example

```yaml
on:
  push:
    paths:
      - 'terraform/**'
```

Now the workflow runs only when files under `terraform/` change.

---

## Multiple Paths

```yaml
on:
  push:
    paths:
      - 'terraform/**'
      - 'modules/**'
```

---

## Ignore Paths

We can also ignore specific paths.

```yaml
on:
  push:
    paths-ignore:
      - 'documentation/**'
```

---

## Real-Time Example

```text
Git Push
    |
    v
Which files changed?
    |
    +---- terraform/** ------> Run Terraform workflow
    |
    +---- docs/** -----------> Skip
    |
    +---- README.md ---------> Skip
```

This helps reduce unnecessary CI/CD executions.
