# First GitHub Actions Workflow

## Objective

Create and run our first GitHub Actions workflow.

---

## What is GitHub Actions?

**GitHub Actions** is a CI/CD automation platform provided by GitHub.

It allows us to automatically perform tasks such as:

* Run tests
* Build applications
* Build Docker images
* Run Terraform
* Deploy applications
* Perform security scans

Example:

```text
Developer
    |
    | git push
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    v
Build / Test / Deploy
```

---

# Basic GitHub Actions Concepts

A GitHub Actions workflow is mainly made up of:

```text
Workflow
   |
   +---- Trigger
   |
   +---- Job
          |
          +---- Runner
          |
          +---- Steps
```

---

## 1. What is a Workflow?

A **workflow** is an automated process defined in a YAML file.

The workflow tells GitHub:

> "When should I run, what should I run, and where should I run it?"

Workflow files are stored inside:

```text
.github/workflows/
```

Example:

```text
.github/workflows/first-workflow.yml
```

A repository can have multiple workflows.

Example:

```text
.github/workflows/
├── first-workflow.yml
├── python-ci.yml
├── docker-build.yml
└── terraform-ci.yml
```

---

## 2. What is a Trigger?

A **trigger** defines **when a workflow should start**.

For example:

```yaml
on:
  push:
```

This means:

> Run the workflow whenever code is pushed to the repository.

Other common triggers are:

```text
push
pull_request
workflow_dispatch
schedule
```

Example:

```yaml
on:
  push:
  pull_request:
```

The workflow will run for both `push` and `pull_request` events.

---

## 3. What is a Job?

A **job** is a group of steps that GitHub Actions executes together.

Example:

```yaml
jobs:
  first-job:
```

A workflow can contain one or multiple jobs.

Example:

```text
Workflow
   |
   +---- Job 1: Build
   |
   +---- Job 2: Test
   |
   +---- Job 3: Deploy
```

Jobs can run in parallel or one job can depend on another job.

---

## 4. What is a Runner?

A **runner** is the machine where a GitHub Actions job actually executes.

Example:

```yaml
runs-on: ubuntu-latest
```

This tells GitHub:

> Run this job on a GitHub-hosted Ubuntu runner.

Common runners include:

```text
ubuntu-latest
windows-latest
macos-latest
```

The runner provides the environment required to execute our commands.

---

## 5. What is a Step?

A **step** is an individual task inside a job.

Example:

```yaml
steps:
  - name: Print message
    run: echo "Hello from GitHub Actions"
```

A job can contain multiple steps.

Example:

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

## 6. What is `run`?

`run` is used to execute a shell command on the runner.

Example:

```yaml
- name: Print message
  run: echo "Hello from GitHub Actions"
```

We can execute normal Linux commands:

```yaml
run: |
  pwd
  ls -la
  echo "Hello"
```

---

## 7. What is `name`?

`name` gives a meaningful name to a workflow or step.

Workflow:

```yaml
name: First GitHub Actions Workflow
```

Step:

```yaml
- name: Print message
```

Names make the workflow easier to understand in GitHub Actions.

---

# Complete Workflow

Our first workflow:

```yaml
name: First GitHub Actions Workflow

on:
  push:

jobs:
  first-job:
    runs-on: ubuntu-latest

    steps:
      - name: Print message
        run: echo "Hello from GitHub Actions"
```

---

# Understanding the Workflow

```text
name
 |
 |-- Workflow name
 |
 v
on
 |
 |-- When should the workflow run?
 |
 v
jobs
 |
 |-- What work should be performed?
 |
 v
first-job
 |
 |-- Job
 |
 v
runs-on
 |
 |-- Which machine should run the job?
 |
 v
steps
 |
 |-- Individual tasks
 |
 v
run
 |
 |-- Command to execute
```

---

# Project Structure

```text
01-first-workflow/
├── README.md
└── .github/
    └── workflows/
        └── first-workflow.yml
```

---

# Execution Flow

When we push code to GitHub:

```text
Developer
    |
    | git push
    v
GitHub Repository
    |
    v
Trigger: push
    |
    v
Workflow
    |
    v
Job: first-job
    |
    v
Runner: ubuntu-latest
    |
    v
Step: Print message
    |
    v
echo "Hello from GitHub Actions"
```

---

# Run the Workflow

Make a change and push it to GitHub:

```bash
git add .
git commit -m "Add first GitHub Actions workflow"
git push
```

Then open:

```text
GitHub Repository
       ↓
     Actions
       ↓
First GitHub Actions Workflow
```

You should see the workflow execution and the output:

```text
Hello from GitHub Actions
```

---

# Key Points

Remember these five concepts:

| Concept  | Meaning                        |
| -------- | ------------------------------ |
| Workflow | Complete automation process    |
| Trigger  | Defines when the workflow runs |
| Job      | Group of tasks                 |
| Runner   | Machine where the job runs     |
| Step     | Individual task inside a job   |

Simple way to remember:

```text
Workflow
   ↓
Trigger
   ↓
Job
   ↓
Runner
   ↓
Steps
```
