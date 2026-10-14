# Status Check Functions

GitHub Actions provides status check functions that allow workflows to react to job and step status.

The commonly used functions are:

```text
success()
failure()
always()
cancelled()
```

---

## 1. success()

Runs when previous steps have succeeded.

```yaml
if: success()
```

Use for:

```text
Successful build
Successful tests
Successful deployment
```

---

## 2. failure()

Runs when a previous step has failed.

```yaml
if: failure()
```

Use for:

```text
Failure notification
Debug information
Failure handling
```

---

## 3. always()

Runs regardless of whether previous steps succeeded or failed.

```yaml
if: always()
```

Useful for:

```text
Cleanup
Logs
Diagnostics
Reporting
```

---

## 4. cancelled()

Runs when the workflow or job has been cancelled.

```yaml
if: cancelled()
```

This can be useful for cleanup or cancellation handling.

---

## Comparison

| Function      | Executes when                 |
| ------------- | ----------------------------- |
| `success()`   | Previous work succeeded       |
| `failure()`   | Previous work failed          |
| `always()`    | Regardless of previous result |
| `cancelled()` | Workflow/job was cancelled    |

---

## Real-Time CI/CD

```text
                Build
                  |
                  v
                Test
             /         \
        Success       Failure
           |             |
           v             v
        Deploy       Notify
           |
           v
        Cleanup
           |
           v
       always()
```

These functions become especially useful in production CI/CD workflows.
