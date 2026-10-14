# Dependency Caching

Dependency caching stores reusable dependency data so future workflow runs can execute faster.

---

## Why Cache Dependencies?

Consider a Node.js project:

```text
package.json
package-lock.json
```

The workflow may run:

```bash
npm install
```

Every workflow run may need to download dependencies again.

Caching can reduce this repeated work.

---

# Without Cache

```text
Workflow Run
    |
    v
npm install
    |
    v
Download dependencies
    |
    v
Build
```

Every run may download dependencies again.

---

# With Cache

```text
First Run
    |
    v
Download dependencies
    |
    v
Create cache
    |
    v
Future Run
    |
    v
Restore cache
    |
    v
Faster build
```

---

# Setup Node Cache

The `setup-node` action supports package-manager caching.

Example:

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'npm'
```

This configures caching for npm data.

---

# Cache vs Artifact

| Artifact            | Cache                     |
| ------------------- | ------------------------- |
| Workflow output     | Reusable dependency data  |
| Build package       | npm/pip dependency cache  |
| Test report         | Speeds up future runs     |
| Passed between jobs | Used across workflow runs |
| Example: `app.zip`  | Example: npm cache        |

---

# Important

Do not use a cache as a replacement for an artifact.

Use:

```text
Artifact → Preserve/share workflow output
Cache    → Speed up future workflow runs
```
