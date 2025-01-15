## Git Push
- Push the Code to the Remote Repository
```bash
git push -u origin main
```
This command pushes the changes in your local `main` branch to the `main` branch of the remote repository and sets the remote as the default upstream.

### Options for `git push`
- `-f`: Forces the push, overwriting changes.
  ```bash
  git push -f
  ```
- `--tags`: Pushes all tags to the remote repository.
  ```bash
  git push --tags
  ```
- `--delete <remote>/<branch>`: Deletes a branch on the remote repository.
  ```bash
  git push origin --delete feature-branch
  ```
---

## Git Pull

The `git pull` command is used to fetch and merge changes from a remote repository into your current branch. It combines `git fetch` and `git merge` into a single command.

### Syntax
```bash
git pull [options] [repository] [refspec]
```

### Common Use Cases
1. **Pull Changes from the Default Remote and Branch**:
   ```bash
   git pull
   ```
   Fetches and merges changes from the remote-tracking branch.

2. **Pull Changes from a Specific Remote Branch**:
   ```bash
   git pull origin main
   ```
   Fetches and merges changes from the `main` branch of the `origin` remote.

3. **Rebase Instead of Merging**:
   ```bash
   git pull --rebase
   ```
   Fetches changes and rebases your commits on top of them.

### Options
- `--rebase`: Rebase the current branch on top of the upstream branch after fetching changes.
  ```bash
  git pull --rebase
  ```

- `--all`: Fetches and merges changes from all configured remotes.
  ```bash
  git pull --all
  ```

- `--no-commit`: Fetches and merges changes without committing the result.
  ```bash
  git pull --no-commit
  ```

- `--squash`: Creates a single squashed commit for all changes fetched.
  ```bash
  git pull --squash
  ```

- `--no-rebase`: Ensures that the pull operation does not perform a rebase.
  ```bash
  git pull --no-rebase
  ```

### Examples
- Fetch and merge changes from the `develop` branch:
  ```bash
  git pull origin develop
  ```

- Rebase your branch on top of the `main` branch:
  ```bash
  git pull --rebase origin main
  ```

- Fetch changes from all remotes:
  ```bash
  git pull --all
  ```

- Perform a pull without committing the merge result:
  ```bash
  git pull --no-commit
  ```

### Notes
- If there are conflicts during the merge, resolve them and then commit the changes.
- To pull changes from a specific remote and branch while rebasing:
  ```bash
  git pull --rebase origin feature-branch
  ```
- Ensure your local branch is up to date before pushing changes after a pull:
  ```bash
  git pull origin main
  git push origin main
  ```
---

## Git Fetch

The `git fetch` command downloads objects and refs from another repository. Unlike `git pull`, it does not merge the changes into your current branch but updates your local tracking branches with the latest changes from the remote.

### Syntax
```bash
git fetch [options] [repository] [refspec]
```

### Common Use Cases
1. **Fetch Updates from the Default Remote**:
   ```bash
   git fetch
   ```
   Retrieves all updates from the remote repository without applying them to your working directory.

2. **Fetch from a Specific Remote**:
   ```bash
   git fetch origin
   ```
   Updates the local tracking branches from the `origin` remote.

3. **Fetch a Specific Branch**:
   ```bash
   git fetch origin main
   ```
   Fetches updates only for the `main` branch from the `origin` remote.

### Options
- `--all`: Fetches updates from all remotes.
  ```bash
  git fetch --all
  ```

- `--dry-run`: Displays what would be fetched without actually fetching the updates.
  ```bash
  git fetch --dry-run
  ```

- `--prune`: Removes local references to remote branches that no longer exist.
  ```bash
  git fetch --prune
  ```

- `--tags`: Fetches all tags from the remote repository.
  ```bash
  git fetch --tags
  ```

- `--depth <depth>`: Fetches a limited history of commits for shallow repositories.
  ```bash
  git fetch --depth 1
  ```

### Examples
- Fetch updates from all remotes and prune stale branches:
  ```bash
  git fetch --all --prune
  ```

- Fetch a specific branch and display details without making changes:
  ```bash
  git fetch --dry-run origin feature-branch
  ```

- Fetch all tags:
  ```bash
  git fetch --tags
  ```

- Fetch updates with a shallow clone:
  ```bash
  git fetch --depth 1
  ```

### Notes
- Use `git fetch` regularly to keep your tracking branches updated.
- Combine `git fetch` with `git log` to inspect remote changes before merging them into your local branch.
  ```bash
  git fetch origin main
  git log HEAD..origin/main
  ```
- To integrate fetched changes, follow up with `git merge` or `git rebase` as appropriate.

---

## Git Clone

The `git clone` command creates a copy of an existing remote repository locally. It is commonly used to start working on an existing project.

### Syntax
```bash
git clone [options] <repository> [directory]
```

### Common Use Cases
1. **Clone a Repository into a New Directory**:
   ```bash
   git clone https://github.com/user/repo.git
   ```
   Creates a local copy of the repository.

2. **Clone into a Specific Directory**:
   ```bash
   git clone https://github.com/user/repo.git my-folder
   ```
   Clones the repository into a folder named `my-folder`.

3. **Clone Only a Specific Branch**:
   ```bash
   git clone -b main --single-branch https://github.com/user/repo.git
   ```
   Clones only the `main` branch.

### Options
- `-b` or `--branch`: Clone a specific branch instead of the default branch.
  ```bash
  git clone -b feature-branch https://github.com/user/repo.git
  ```

- `--single-branch`: Clone only the history of the specified branch.
  ```bash
  git clone --single-branch -b main https://github.com/user/repo.git
  ```

- `--depth`: Perform a shallow clone with a limited commit history.
  ```bash
  git clone --depth 1 https://github.com/user/repo.git
  ```

- `--recurse-submodules`: Clone submodules along with the repository.
  ```bash
  git clone --recurse-submodules https://github.com/user/repo.git
  ```

- `--mirror`: Clone a repository for use as a mirror, copying all refs and branches.
  ```bash
  git clone --mirror https://github.com/user/repo.git
  ```

### Examples
- Clone a repository into the current directory:
  ```bash
  git clone https://github.com/user/repo.git .
  ```

- Clone a specific branch with limited commit history:
  ```bash
  git clone --depth 10 -b main https://github.com/user/repo.git
  ```

- Clone a repository along with its submodules:
  ```bash
  git clone --recurse-submodules https://github.com/user/repo.git
  ```

### Notes
- After cloning, you can navigate into the repository and begin working:
  ```bash
  cd repo
  ```
- Ensure that you have the necessary permissions to clone private repositories.
- Use `git remote -v` to verify the remote URLs of the cloned repository.

---

## Git Remote
```bash
git remote add origin git@github.com:EhsaasChaudhary/dfdf.git
```
This links your local repository to a remote repository hosted on GitHub.

### Options for `git remote`
- `git remote -v`: Lists the remotes and their URLs.
  ```bash
  git remote -v
  ```
- `git remote rename <old-name> <new-name>`: Renames a remote.
  ```bash
  git remote rename origin upstream
  ```
- `git remote remove <name>`: Removes a remote.
  ```bash
  git remote remove origin
  ```

---
