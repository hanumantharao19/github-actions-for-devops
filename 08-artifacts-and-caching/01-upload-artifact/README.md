# Upload Artifact

An artifact is a file or collection of files produced during a workflow that we want to preserve.

GitHub Actions provides the `upload-artifact` action for this purpose.

Example:

```yaml
uses: actions/upload-artifact@v4
```

---

## Why Upload Artifacts?

Suppose a build creates:

```text
build/
├── app.jar
├── config/
└── README.md
```

The workflow can upload the build directory as an artifact.

```text
Build
  |
  v
Create build/
  |
  v
Upload Artifact
  |
  v
GitHub
```

---

## Example

```yaml
- name: Upload build files
  uses: actions/upload-artifact@v4
  with:
    name: application-build
    path: build/
```

---

## Artifact Name

The artifact is given a name:

```yaml
name: application-build
```

This name can later be used when downloading the artifact.

---

## Real-Time Usage

Artifacts are commonly used for:

* Application packages
* Test reports
* Coverage reports
* Logs
* Build output
* Deployment packages

---

## Important

An artifact is not the same as a Git commit.

Artifacts are files produced by a workflow and stored separately from the repository source code.
