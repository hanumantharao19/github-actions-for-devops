# Expressions

Expressions allow GitHub Actions to dynamically evaluate values.

The basic syntax is:

```yaml
${{ expression }}
```

---

## Accessing Variables

Repository variable:

```yaml
${{ vars.APP_NAME }}
```

Secret:

```yaml
${{ secrets.API_TOKEN }}
```

GitHub context:

```yaml
${{ github.repository }}
```

---

## Example

```yaml
run: echo "Application: ${{ vars.APP_NAME }}"
```

---

## Comparing Values

Expressions can compare values.

Example:

```yaml
${{ github.ref_name == 'main' }}
```

Another example:

```yaml
${{ github.event_name == 'push' }}
```

---

## Logical Operators

You can use:

```text
==
!=
&&
||
!
```

Example:

```yaml
${{ github.ref_name == 'main' && github.event_name == 'push' }}
```

---

## Why Expressions Are Important

Expressions make workflows dynamic.

Instead of hard-coding:

```text
Deploy to production
```

we can make the workflow decide:

```text
Is branch main?
       |
      Yes
       |
       v
Deploy
```

Expressions are heavily used with:

* `if`
* variables
* contexts
* job outputs
* reusable workflows
* matrices

---

## Important

Expressions are usually written inside:

```text
${{ }}
```

For example:

```yaml
${{ github.ref_name }}
```
