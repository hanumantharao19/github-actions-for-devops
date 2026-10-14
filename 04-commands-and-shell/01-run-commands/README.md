# Run Commands

## Objective

Learn how to execute shell commands inside a GitHub Actions runner.

---

## `run`

The `run` keyword executes a command on the runner.

Example:

```yaml
- name: Print message
  run: echo "Hello GitHub Actions"
```

---

## Linux Commands

Because we are using an Ubuntu runner, we can execute common Linux commands.

Examples:

```text
pwd
ls
whoami
date
uname
git --version
```

---

## Real-Time Usage

CI/CD workflows commonly execute commands such as:

```text
npm install
npm test
mvn test
pytest
terraform init
terraform plan
docker build
docker push
```

---

## Important

The command runs on the runner, not on your local computer.

```text
Your Computer
     |
     | git push
     v
GitHub
     |
     v
GitHub Actions
     |
     v
GitHub Runner
     |
     v
run command
```
