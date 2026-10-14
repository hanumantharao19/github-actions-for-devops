# Setup Python Action

The setup-python action installs and configures Python for the GitHub Actions runner.

Example:

```yaml
uses: actions/setup-python@v5
```

---

## Why Do We Need It?

For Python applications, the CI pipeline may need to execute:

```bash
python
pip
pytest
```

We can configure Python using:

```yaml
- name: Setup Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.12'
```

---

## CI Flow

```text
Checkout
   |
   v
Setup Python
   |
   v
Install Dependencies
   |
   v
Run Tests
   |
   v
Build / Package
```

---

## Example

```yaml
steps:

  - name: Checkout
    uses: actions/checkout@v4

  - name: Setup Python
    uses: actions/setup-python@v5
    with:
      python-version: '3.12'

  - name: Install dependencies
    run: pip install -r requirements.txt

  - name: Run tests
    run: pytest
```

---

## `with`

The `with` section provides inputs to an action.

Example:

```yaml
with:
  python-version: '3.12'
```

This tells the setup-python action which Python version to configure.
