# 09 - GitHub Actions CI

## Overview

In the previous sections, we learned individual GitHub Actions concepts such as:

* Workflows
* Events
* Triggers
* Jobs
* Steps
* Runners
* Environment variables
* Secrets
* Expressions
* Conditions
* Actions
* Artifacts
* Caching

Now we will combine these concepts to build **real Continuous Integration (CI) pipelines**.

## What is CI?

Continuous Integration means automatically building and validating application code whenever developers make changes.

Typical CI flow:

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
Checkout Code
   |
   v
Install Dependencies
   |
   v
Build
   |
   v
Test
   |
   v
Code Validation
   |
   v
CI Passed / Failed
```

## CI Pipeline

A typical application CI pipeline contains:

```text
Checkout
   |
   v
Setup Runtime
   |
   v
Install Dependencies
   |
   v
Build
   |
   v
Test
   |
   v
Publish Test Results / Artifacts
```

## Topics

### 01 - Python CI

Learn how to create a CI pipeline for a Python application.

Topics:

* Checkout source code
* Setup Python
* Install dependencies
* Run Python tests
* Use dependency caching
* Build validation

### 02 - Node.js CI

Learn how to create a CI pipeline for a Node.js application.

Topics:

* Checkout source code
* Setup Node.js
* npm dependency installation
* npm test
* npm build
* npm caching

### 03 - Java CI

Learn how to create a CI pipeline for a Java Maven application.

Topics:

* Checkout source code
* Setup Java
* Maven dependency management
* Maven build
* Unit tests
* Package application

### 04 - Multi-Job CI

Learn how to split CI into multiple jobs.

Example:

```text
             ┌───────────────┐
             │    Checkout   │
             └───────┬───────┘
                     |
          ┌──────────┼──────────┐
          v          v          v
       Lint Job   Test Job   Build Job
          |          |          |
          └──────────┼──────────┘
                     v
                CI Summary
```

## Why CI is Important

Without CI:

```text
Developer
   |
   v
Write Code
   |
   v
Push Code
   |
   v
Manual Testing
   |
   v
Manual Build
```

With CI:

```text
Developer
   |
   v
git push
   |
   v
GitHub Actions
   |
   ├── Build
   ├── Test
   ├── Lint
   └── Validate
          |
          v
      CI Result
```

## Real-Time DevOps Example

For a `product-service` application:

```text
Developer
    |
    | Pull Request
    v
GitHub
    |
    v
GitHub Actions
    |
    ├── Checkout
    ├── Setup Python
    ├── Install Dependencies
    ├── Run Tests
    ├── Build
    └── Upload Artifact
            |
            v
       CI Passed
            |
            v
       Merge PR
```

Later, CI will connect to CD:

```text
GitHub
   |
   v
CI
   |
   ├── Build
   ├── Test
   └── Package
          |
          v
       Artifact
          |
          v
         CD
          |
     ┌────┼────┐
     v    v    v
    DEV  QA   PROD
```

## Important Concepts

| Concept    | Purpose                                    |
| ---------- | ------------------------------------------ |
| CI         | Automatically validate code                |
| Build      | Compile/package application                |
| Test       | Verify application behavior                |
| Lint       | Check code quality/style                   |
| Dependency | External libraries required by application |
| Artifact   | Build output that can be reused            |
| Cache      | Speeds up dependency installation          |
| Runner     | Machine where CI executes                  |

## Learning Goal

After completing this section, you should be able to create GitHub Actions CI pipelines for:

* Python
* Node.js
* Java
* Multi-job applications

These concepts will be used later for:

* Docker CI
* Terraform CI
* AWS deployment
* GCP deployment
* Kubernetes deployment
* Complete CI/CD projects
