# Download Artifact

Artifacts can be downloaded by another job in the same workflow.

The basic action is:

```yaml
uses: actions/download-artifact@v5
```

---

# Why Do We Need This?

Consider a CI/CD pipeline:

```text
Build Job
    |
    v
Create Application
    |
    v
Upload Artifact
    |
    v
Deploy Job
    |
    v
Download Artifact
    |
    v
Deploy Application
```

The build job and deploy job run on different runners.

Therefore, files created by the build job are not automatically available to the deploy job.

The artifact provides the bridge.

---

# Upload

Build job:

```yaml
- name: Upload artifact
  uses: actions/upload-artifact@v4
  with:
    name: application-build
    path: build/
```

---

# Download

Deploy job:

```yaml
- name: Download artifact
  uses: actions/download-artifact@v5
  with:
    name: application-build
    path: build/
```

---

# Important Concept

Each GitHub-hosted job normally gets a fresh runner.

```text
Build Runner
    |
    +-- build/app.jar
    |
    v
Upload Artifact
    |
    v
GitHub
    |
    v
Deploy Runner
    |
    v
Download Artifact
    |
    +-- build/app.jar
```

This is one of the most important reasons artifacts are used in CI/CD.
