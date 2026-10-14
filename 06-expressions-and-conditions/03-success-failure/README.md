# Success and Failure

GitHub Actions can execute steps depending on whether previous steps succeed or fail.

The two basic status functions are:

```text
success()
failure()
```

---

## success()

`success()` returns true when previous steps have succeeded.

Example:

```yaml
if: success()
```

---

## failure()

`failure()` returns true when a previous step has failed.

Example:

```yaml
if: failure()
```

---

## Real-Time Example

```text
Build
  |
  v
Test
  |
  +---- Failed ----> Failure Notification
  |
  v
Success
  |
  v
Deploy
```

---

## Why Is This Useful?

Failure handling is common in CI/CD.

Examples:

* Send notification
* Collect logs
* Upload diagnostic files
* Cleanup resources
* Stop deployment

---

## Important

A normal step after a failed step may be skipped because the default behavior is to continue only when the job is successful.

Use status check functions when you explicitly want different behavior.
