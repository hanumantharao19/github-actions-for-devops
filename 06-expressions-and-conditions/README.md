# 06 - Expressions and Conditions

GitHub Actions uses expressions and conditions to make workflows dynamic.

Until now, we learned how to:

```text
Workflow
   |
   +-- Events
   +-- Triggers
   +-- Commands
   +-- Variables
   +-- Secrets
   +-- GitHub Context
```

Now we learn how to make decisions inside workflows.

---

## Learning Flow

```text
01 Expressions
      |
      v
02 if Conditions
      |
      v
03 Success / Failure
      |
      v
04 Status Check Functions
      |
      v
05 Contexts
```

---

# 1. Expressions

Expressions allow GitHub Actions to calculate values or access information dynamically.

Example:

```yaml
run: echo "Branch: ${{ github.ref_name }}"
```

Another example:

```yaml
run: echo "Application: ${{ vars.APP_NAME }}"
```

Common syntax:

```text
${{ expression }}
```

---

# 2. if Conditions

Conditions allow a job or step to execute only when a particular condition is true.

Example:

```yaml
if: github.ref_name == 'main'
```

This is useful for deployment workflows.

```text
feature branch
      |
      v
   Build
      |
      v
    Test
      |
      v
   main?
    /   \
   No    Yes
   |      |
 Stop   Deploy
```

---

# 3. Success and Failure

A workflow can behave differently depending on whether previous steps succeeded or failed.

Example:

```yaml
if: success()
```

or:

```yaml
if: failure()
```

This is useful for:

* Notifications
* Cleanup
* Debugging
* Deployment decisions

---

# 4. Status Check Functions

GitHub Actions provides functions such as:

```text
success()
failure()
always()
cancelled()
```

Example:

```yaml
if: failure()
```

This allows us to execute a step only when an earlier step fails.

---

# 5. Contexts

Contexts provide information about the current workflow execution.

Examples:

```yaml
github.repository
github.ref_name
github.sha
github.actor
github.event_name
```

Other contexts include:

```text
github
env
vars
secrets
job
steps
runner
matrix
needs
inputs
```

These become very important in real CI/CD pipelines.

---

# Real-Time CI/CD Example

A deployment workflow can use expressions and conditions like this:

```text
Developer
    |
    v
Pull Request
    |
    v
Build
    |
    v
Test
    |
    +---- Failed ----> Notify
    |
    v
Tests Passed
    |
    v
Is branch main?
    |
   Yes
    |
    v
Deploy Production
```

Expressions and conditions allow GitHub Actions to make these decisions automatically.

---

# Learning Objective

After completing this section, you should understand:

* GitHub Actions expressions
* `${{ }}` syntax
* `if` conditions
* Step conditions
* Job conditions
* `success()`
* `failure()`
* `always()`
* `cancelled()`
* GitHub Actions contexts
* How conditions are used in CI/CD
