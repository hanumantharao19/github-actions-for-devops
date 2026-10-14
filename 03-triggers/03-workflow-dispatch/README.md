# Workflow Dispatch

## Objective

Learn how to manually execute a GitHub Actions workflow and pass inputs to it.

---

## What is `workflow_dispatch`?

`workflow_dispatch` allows us to manually start a workflow from the GitHub Actions UI.

Example:

```yaml
on:
  workflow_dispatch:
```

---

## Why is it useful?

In real DevOps projects, we may want to manually start:

* Deployment
* Rollback
* Database migration
* Infrastructure changes
* Emergency operations

---

## Workflow Inputs

We can ask the user for input.

Example:

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Deployment environment"
        required: true
        type: choice
        options:
          - dev
          - qa
          - prod
```

When the workflow is manually started, GitHub displays the input.

---

## Example

```text
Run workflow

Environment:
[ dev ▼ ]

        Run workflow
```

The selected value can then be used by the job.

---

## Real-Time Example

```text
Engineer
   |
   | Run workflow
   v
GitHub Actions
   |
   +---- dev
   +---- qa
   +---- prod
   |
   v
Deployment
```
