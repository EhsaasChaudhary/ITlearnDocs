# Initializing git on local

## Git Init

The `git init` command initializes a new Git repository in the specified directory. This command creates a `.git` folder that contains all the metadata and history for the repository.

### **Usage**:
```bash
git init [directory]
```

- If no directory is specified, it initializes the current folder.

### **Options**:
- `--bare`: Initializes a bare repository that does not have a working directory. Bare repositories are typically used for remote repositories.
  ```bash
  git init --bare
  ```
- `--quiet`: Suppresses the output message.
  ```bash
  git init --quiet
  ```
- `--shared[=permissions]`: Configures repository permissions to be shared among a group. Common values for permissions are `group`, `all`, or `umask`.
  ```bash
  git init --shared=group
  ```
- `--separate-git-dir=<git-dir>`: Creates a Git repository with the `.git` folder stored in a separate directory.
  ```bash
  git init --separate-git-dir=/path/to/git-dir
  ```
- `-b <branch-name>`: Creates the repository with an initial branch named `<branch-name>` instead of the default `main` branch.
  ```bash
  git init -b <branch-name>
  ```

---

## Additional Git Commands

### Configure User Information
Before starting, configure your Git user name and email:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
---
