# 08 - Artifacts and Caching

GitHub Actions runners are temporary machines.

When a job finishes, files created on the runner are normally not available to another job unless we explicitly preserve or transfer them.

GitHub Actions provides **artifacts** for storing files produced by a workflow and **caching** for reusing dependencies between workflow runs.

---

## Learning Flow

```text
01 Upload Artifact
        |
        v
02 Download Artifact
        |
        v
03 Dependency Caching
        |
        v
04 Build Artifact
```

---

# Artifact vs Cache

These two concepts are different.

## Artifact

An artifact is a file or group of files produced by a workflow that we want to preserve or pass to another job.

Examples:

```text
Build package
ZIP file
JAR file
Test reports
Coverage reports
Logs
Docker-related build output
```

---

## Cache

A cache stores files that can be reused in future workflow runs to make builds faster.

Common example:

```text
Node.js dependencies
Python packages
Package manager caches
Build dependencies
```

---

## Simple Difference

```text
Artifact
    |
    +-- Output of the workflow
    +-- Preserve/share files
    +-- Build packages
    +-- Test reports
    +-- Logs


Cache
    |
    +-- Reusable data
    +-- Speed up future runs
    +-- Dependencies
    +-- Package manager cache
```

---

# Artifact Flow

```text
Build Job
    |
    v
Create Files
    |
    v
Upload Artifact
    |
    v
GitHub
    |
    v
Download Artifact
    |
    v
Another Job
```

---

# Cache Flow

```text
First Workflow Run
        |
        v
Install Dependencies
        |
        v
Create Cache
        |
        v
Future Workflow Run
        |
        v
Restore Cache
        |
        v
Faster Build
```

---

# Real-Time CI/CD Example

A typical pipeline might look like:

```text
Checkout
   |
   v
Install Dependencies
   |
   v
Build Application
   |
   v
Create Build Package
   |
   v
Upload Artifact
   |
   v
Test / Deploy Job
   |
   v
Download Artifact
   |
   v
Deploy
```

---

# Important Concepts

After completing this section, you should understand:

* What is an artifact?
* Uploading artifacts
* Downloading artifacts
* Passing files between jobs
* What is dependency caching?
* Why caching improves build speed
* Difference between artifacts and caches
* Build artifacts in CI/CD

---

# Important Rule

Do not confuse:

```text
Artifact = workflow output
Cache    = reusable data used to speed up workflows
```

A build ZIP file is normally an artifact.

Node.js dependencies are a common caching example.
