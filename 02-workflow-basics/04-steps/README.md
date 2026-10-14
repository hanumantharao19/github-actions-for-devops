# GitHub Actions Steps

## Objective

Understand steps inside a GitHub Actions job.

---

## What is a Step?

A **step** is an individual task performed inside a job.

Example:

```yaml
steps:

  - name: Step 1
    run: echo "First step"

  - name: Step 2
    run: echo "Second step"
```

---

## Multiple Steps

A job can contain multiple steps.

```text
Job
 |
 +-- Step 1: Checkout code
 |
 +-- Step 2: Install dependencies
 |
 +-- Step 3: Run tests
 |
 +-- Step 4: Build application
```

Steps execute sequentially by default.

---

## `run`

The `run` keyword executes a shell command.

Example:

```yaml
- name: Show current directory
  run: pwd
```

Multiple commands can be executed using `|`.

```yaml
- name: Run multiple commands
  run: |
    pwd
    ls -la
    echo "Hello"
```

---

## Important

A job contains steps.

```text
Workflow
   |
   +-- Job
        |
        +-- Step
        +-- Step
        +-- Step
```
