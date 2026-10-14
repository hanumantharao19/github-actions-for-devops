# 04 - Multi-Job CI

## Objective

Learn how to divide a CI pipeline into multiple jobs.

Instead of putting everything into one job:

```text
Build
  |
Test
  |
Lint
```

we can create separate jobs.

## Pipeline

```text
                 GitHub
                    |
                    v
              GitHub Actions
                    |
          ┌─────────┼─────────┐
          |         |         |
          v         v         v
       Lint Job  Test Job  Build Job
          |         |         |
          └─────────┼─────────┘
                    |
                    v
               CI Complete
```

## Why Multiple Jobs?

Separate jobs provide:

* Better organization
* Parallel execution
* Independent failure reporting
* Easier troubleshooting
* Faster CI pipelines

## Example

```text
lint
test
build
```

By default, independent jobs can run in parallel.

## Job Dependency

If we want:

```text
Test
  |
  v
Build
```

we use:

```yaml
needs: test
```

Example:

```yaml
build:
  needs: test
```

This means the build job waits for the test job.

## Real-Time CI

```text
              Pull Request
                   |
                   v
             GitHub Actions
                   |
        ┌──────────┼──────────┐
        v          v          v
      Lint        Test       Build
        |          |          |
        └──────────┼──────────┘
                   |
                   v
              CI Passed
```

This structure is useful when building larger CI/CD pipelines.
