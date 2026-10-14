# Pull Request Trigger

## Objective

Learn how to control when a workflow runs for pull request events.

---

## Pull Request Activity

A pull request can have different activities.

Common activities include:

```text
opened
synchronize
reopened
closed
```

We can specify which activities should trigger the workflow.

---

## Example

```yaml
on:
  pull_request:
    types:
      - opened
      - synchronize
      - reopened
```

The workflow runs when:

* A pull request is opened
* New commits are pushed to the pull request
* A closed pull request is reopened

---

## Branch Filtering

We can also restrict the target branch.

```yaml
on:
  pull_request:
    branches:
      - main
```

This means:

> Run when a pull request targets the `main` branch.

---

## Real-Time CI Example

```text
Developer
    |
    v
Feature Branch
    |
    v
Pull Request
    |
    v
main
    |
    v
GitHub Actions
    |
    +-- Build
    +-- Test
    +-- Code Quality
```

This is commonly used for CI.
