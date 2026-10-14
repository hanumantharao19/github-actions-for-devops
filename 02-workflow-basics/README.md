# GitHub Actions – Workflow Basics

## Learning Objectives

By the end of this section, you will understand:

- GitHub Actions workflow structure
- Events that trigger workflows
- Jobs and job execution
- Steps and shell commands
- GitHub-hosted runners
- How workflows, jobs, runners, and steps work together

---

## 1. What Is a GitHub Actions Workflow?

A **workflow** is an automated process defined using a YAML file. It contains one or more jobs that GitHub Actions executes when a specified event occurs or when a user manually starts it.

Workflows are stored in the repository's `.github/workflows/` directory.

### Example: Basic Workflow

```yaml
name: Workflow Basics Demo

on:
  workflow_dispatch:

jobs:
  first-job:
    runs-on: ubuntu-latest

    steps:
      - name: Print message
        run: echo "Hello from GitHub Actions"
```

### Explanation

- `name`: Defines the workflow name.
- `on`: Specifies when the workflow should run.
- `workflow_dispatch`: Allows manual execution from GitHub.
- `jobs`: Defines the jobs in the workflow.
- `first-job`: The ID of the job.
- `runs-on`: Specifies the runner that executes the job.
- `steps`: Defines the tasks performed by the job.
- `run`: Executes a shell command.

### Workflow Execution Flow

```text
GitHub Repository
       |
       v
Workflow YAML
       |
       v
Trigger Event
       |
       v
Job
       |
       v
Runner
       |
       v
Steps
       |
       v
Execution Result
```

Example: See [`01-workflow-structure.yml`](examples/01-workflow-structure.yml).

---

## 2. GitHub Actions Events

### What Is an Event?

An **event** is an activity that triggers a GitHub Actions workflow.

For example, when a developer pushes code to a repository, a workflow configured for the `push` event can run automatically.

### 2.1 Push Event

```yaml
on:
  push:
```

Runs when a push event occurs in the repository.

You can restrict it to a particular branch:

```yaml
on:
  push:
    branches:
      - main
```

This workflow runs when a push event occurs on the `main` branch.

### 2.2 Pull Request Event

```yaml
on:
  pull_request:
```

Runs when a pull request event occurs, such as opening or updating a pull request, subject to the event configuration.

### 2.3 Manual Trigger

```yaml
on:
  workflow_dispatch:
```

Allows a user to start a workflow manually from the GitHub Actions interface.

This is useful for demonstrations, testing, and controlled deployments.

### 2.4 Schedule Event

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

Runs according to a cron schedule. This example specifies midnight UTC every day.

Scheduled workflows use UTC and can be delayed under some conditions.

### 2.5 Multiple Events

A workflow can support multiple trigger events.

```yaml
on:
  push:
  pull_request:
  workflow_dispatch:
```

This workflow can be triggered by push events, pull request events, or manual execution.

### Important Concept

- **Event:** When should the workflow run?
- **Job:** What group of tasks should execute?
- **Step:** What individual task should run?

Example: See [`02-events.yml`](examples/02-events.yml).

---

## 3. GitHub Actions Jobs

### What Is a Job?

A **job** is a group of steps that execute on the same runner.

A workflow can contain multiple jobs. By default, jobs without dependencies can run in parallel.

### Example: Multiple Jobs

```yaml
name: Jobs Demo

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Build application
        run: echo "Building application"

  test:
    runs-on: ubuntu-latest

    steps:
      - name: Run tests
        run: echo "Running tests"

  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Deploy application
        run: echo "Deploying application"
```

### Understanding the Example

This workflow contains three jobs:

- `build`: Simulates building an application.
- `test`: Simulates running tests.
- `deploy`: Simulates deploying an application.

These jobs are independent, so GitHub Actions can execute them in parallel.

**Important:** This example demonstrates job execution only. It does not implement a real application build, test suite, or deployment.

### Running Jobs Sequentially with `needs`

If the test job must wait for the build job, use `needs`.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Build application
        run: echo "Building application"

  test:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - name: Run tests
        run: echo "Running tests"

  deploy:
    needs: test
    runs-on: ubuntu-latest

    steps:
      - name: Deploy application
        run: echo "Deploying application"
```

### Execution Flow

```text
Build Job
    |
    v
Test Job
    |
    v
Deploy Job
```

Here, the `test` job starts after `build` succeeds, and `deploy` starts after `test` succeeds, subject to GitHub Actions job conditions.

### Important Points

- Each job has its own runner.
- Jobs can run in parallel by default.
- Use `needs` to define dependencies between jobs.
- Jobs running on separate runners do not automatically share files or the same local environment.

Example: See [`03-jobs.yml`](examples/03-jobs.yml).

---

## 4. GitHub Actions Steps

### What Is a Step?

A **step** is an individual task inside a job.

Steps within the same job execute sequentially by default, and they run on the same runner.

### Example: Multiple Steps

```yaml
name: Steps Demo

on:
  workflow_dispatch:

jobs:
  steps-job:
    runs-on: ubuntu-latest

    steps:
      - name: Step 1 - Show message
        run: echo "Starting workflow"

      - name: Step 2 - Show directory
        run: pwd

      - name: Step 3 - List files
        run: ls -la

      - name: Step 4 - Complete
        run: echo "Workflow completed"
```

### Understanding `run`

The `run` keyword executes a shell command.

Example:

```yaml
- name: Show current directory
  run: pwd
```

### Running Multiple Commands

Use the pipe (`|`) symbol to write multiple commands in one step.

```yaml
- name: Run multiple commands
  run: |
    pwd
    ls -la
    echo "Hello from GitHub Actions"
```

These commands execute in order within the same step.

### Using Actions in Steps

A step can execute a shell command using `run` or invoke a reusable action using `uses`.

For example:

```yaml
steps:
  - name: Checkout repository
    uses: actions/checkout@v4

  - name: Display message
    run: echo "Repository checked out"
```

The checkout action downloads the repository contents into the runner's workspace.

### Important Points

- A job contains one or more steps.
- Steps execute sequentially by default.
- Use `run` to execute shell commands.
- Use `uses` to invoke an action.
- Files created by one step can generally be accessed by subsequent steps in the same job.

Example: See [`04-steps.yml`](examples/04-steps.yml).

---

## 5. GitHub Actions Runners

### What Is a Runner?

A **runner** is the machine that executes a GitHub Actions job.

A workflow defines the job, and `runs-on` specifies the type of runner on which that job should execute.

### Example

```yaml
jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Display operating system
        run: uname -a
```

In this example, GitHub Actions runs the job on an Ubuntu runner.

### 5.1 GitHub-Hosted Runners

GitHub provides managed runners for supported operating systems.

Common examples include:

**Ubuntu**

```yaml
runs-on: ubuntu-latest
```

**Windows**

```yaml
runs-on: windows-latest
```

**macOS**

```yaml
runs-on: macos-latest
```

GitHub manages the underlying machine for GitHub-hosted runners. Availability, supported images, and usage charges depend on the runner and account plan.

### 5.2 Why Do We Need a Runner?

A workflow contains instructions, but those instructions need a machine to execute them.

Runners execute tasks such as:

- Running shell scripts
- Installing dependencies
- Building applications
- Running automated tests
- Building container images
- Executing Terraform commands
- Deploying applications

### Runner Execution Flow

```text
GitHub Actions Workflow
          |
          v
          Job
          |
          v
        Runner
          |
          v
     Execute Steps
          |
          v
     Return Results
```

### 5.3 Self-Hosted Runners

A self-hosted runner is a machine that you configure and maintain to execute GitHub Actions jobs.

It can run on your own server, virtual machine, or supported cloud infrastructure.

Example:

```yaml
jobs:
  build:
    runs-on: self-hosted

    steps:
      - name: Print message
        run: echo "Running on a self-hosted runner"
```

The repository or organization must have an eligible self-hosted runner available for the job.

### 5.4 Choosing a Runner

| Runner | Common use |
|---|---|
| `ubuntu-latest` | Linux builds, DevOps automation, Terraform and containers |
| `windows-latest` | Windows applications and PowerShell workloads |
| `macos-latest` | macOS and Apple-platform development |
| `self-hosted` | Jobs requiring custom machines, tools, or network access |

For most beginner DevOps examples, start with `ubuntu-latest`.

Example: See [`05-runners.yml`](examples/05-runners.yml).

---

## 6. How Everything Works Together

Consider a CI/CD workflow for an application.

```text
Developer Pushes Code
         |
         v
    Push Event
         |
         v
    Build Job
    Ubuntu Runner
         |
         v
     Build Steps
         |
         v
     Test Job
    Ubuntu Runner
         |
         v
      Test Steps
         |
         v
    Deploy Job
    Ubuntu Runner
         |
         v
    Deploy Steps
```

This is a conceptual example. In a real pipeline, configure job dependencies using `needs`, check out the application code, run actual tests, and set up appropriate deployment credentials and permissions.

### Summary

| Concept | Purpose |
|---|---|
| Workflow | Defines the automated process |
| Event | Determines when a workflow is triggered |
| Job | Groups steps that execute on a runner |
| Runner | Machine that executes a job |
| Step | Individual task inside a job |
| `run` | Executes a shell command |
| `uses` | Invokes an action |
| `needs` | Defines job dependencies |

---

## 7. Hands-On Practice

1. Create a workflow that runs manually.
2. Print a welcome message.
3. Display the current directory.
4. List the repository files.
5. Create two independent jobs and observe their execution.
6. Add `needs` to make one job wait for another.
7. Change the runner from `ubuntu-latest` to `windows-latest`.
8. Add a `push` trigger and test it by pushing a commit to the configured branch.

## Next Section

**GitHub Actions Triggers** — explore events, branch filters, path filters, and workflow execution conditions in more detail.

