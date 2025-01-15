## Git Branch
```bash
git branch -M main
```
This command renames the default branch to `main`.

### Options for `git branch`
- `git branch`: Lists all local branches.
  ```bash
  git branch
  ```
- `git branch -a`: Lists all branches, including remote branches.
  ```bash
  git branch -a
  ```
- `git branch -d <branch>`: Deletes a local branch.
  ```bash
  git branch -d feature-branch
  ```
- `git branch --set-upstream-to=<remote>/<branch>`: Sets upstream tracking for a branch.
  ```bash
  git branch --set-upstream-to=origin/main
  ```
---

## Git Switch

The `git switch` command is a modern replacement for branch-related operations previously handled by `git checkout`. It simplifies switching branches and creating new branches.

### Syntax
```bash
git switch [options] <branch-name>
```

### Common Use Cases
1. **Switching to an Existing Branch**:
   ```bash
   git switch <branch-name>
   ```
   Example:
   ```bash
   git switch main
   ```

2. **Creating and Switching to a New Branch**:
   ```bash
   git switch -c <new-branch-name>
   ```
   Example:
   ```bash
   git switch -c feature/login-module
   ```

3. **Switching to a Remote-Tracking Branch**:
   ```bash
   git switch --track <remote-branch>
   ```
   Example:
   ```bash
   git switch --track origin/feature-xyz
   ```

### Options
- `-c`: Creates a new branch and switches to it.
- `--create`: Synonym for `-c`.
- `--track`: Creates a new branch to track a remote branch.
- `--detach`: Switches to a branch in a detached HEAD state.
- `--discard-changes`: Discards local changes when switching branches (use with caution).

### Examples
- Switch to the `development` branch:
  ```bash
  git switch development
  ```

- Create and switch to a new branch named `feature-api`:
  ```bash
  git switch -c feature-api
  ```

- Switch to a remote-tracking branch:
  ```bash
  git switch --track origin/bugfix-123
  ```

- Switch to a branch in detached HEAD state:
  ```bash
  git switch --detach feature-old
  ```

### Notes
- `git switch` is available in Git 2.23 and later.
- Unlike `git checkout`, `git switch` focuses exclusively on branch-related operations, making it less error-prone.
- Use `git switch` instead of `git checkout` when working with branches for clearer intent.

---

## Git Restore

The `git restore` command is used to restore files or revert changes in the working directory and staging area. It was introduced in Git 2.23 as part of the effort to separate the functionality of `git checkout` into more focused commands.

### Syntax
```bash
git restore [options] <file-path>
```

### Common Use Cases
1. **Restore a File to Its Last Committed State**:
   ```bash
   git restore <file-path>
   ```
   Example:
   ```bash
   git restore README.md
   ```

2. **Unstage a File**:
   ```bash
   git restore --staged <file-path>
   ```
   Example:
   ```bash
   git restore --staged index.html
   ```

3. **Restore All Files in the Repository**:
   ```bash
   git restore .
   ```

4. **Discard Changes Completely**:
   ```bash
   git restore --source=HEAD <file-path>
   ```
   Example:
   ```bash
   git restore --source=HEAD config.yaml
   ```

### Options
- `--staged`: Unstages a file from the index (staging area) without changing the working directory.
- `--source=<commit>`: Specifies the commit to restore from (default is `HEAD`).
- `--worktree`: Restores changes in the working directory (default behavior).
- `--`: Separates file paths from options, avoiding ambiguity.
- `--patch` or `-p`: Allows interactive restoration of parts of a file.

### Examples
- Restore a single file to its committed state:
  ```bash
  git restore app.js
  ```

- Unstage a file:
  ```bash
  git restore --staged app.js
  ```

- Discard all local changes:
  ```bash
  git restore .
  ```

- Interactively restore hunks in a file:
  ```bash
  git restore -p app.js
  ```

### Notes
- `git restore` is available in Git 2.23 and later.
- Use this command instead of `git checkout` for file-specific operations for better clarity.
- Be cautious when discarding changes as they cannot be recovered unless committed.

---

## Git Checkout

### **`git checkout`**
The `git checkout` command is used to switch between branches or restore files in a Git repository.

### **What It Does**:
- Switches to an existing branch.
- Creates a new branch and switches to it (with `-b` option).
- Restores a specific file or files to a previous state.

### **Usage**:
```bash
git checkout [options] <branch-name>
```

### **Options**:
- Switch to an existing branch:
  ```bash
  git checkout <branch-name>
  ```
- Create and switch to a new branch:
  ```bash
  git checkout -b <new-branch-name>
  ```
- Restore a file to its state in the last commit:
  ```bash
  git checkout -- <file-name>
  ```
- Switch to a specific commit (detached HEAD state):
  ```bash
  git checkout <commit-hash>
  ```
- `--orphan <new-branch-name>`: Creates a new branch with no history.
  ```bash
  git checkout --orphan <new-branch-name>
  ```
- `--detach`: Operates in a detached HEAD state, allowing inspection of an arbitrary commit.
  ```bash
  git checkout --detach <commit-hash>
  ```
---

## Git Merge

The `git merge` command is used to combine the changes from one branch into the current branch. It is a key tool for integrating work in Git, often used in collaborative workflows.

### Syntax
```bash
git merge [options] <branch>
```

### Common Use Cases
1. **Merge a Branch into the Current Branch**:
   ```bash
   git merge <branch-name>
   ```
   Example:
   ```bash
   git merge feature-branch
   ```

2. **Merge with a Commit Message**:
   ```bash
   git merge -m "Merge message" <branch-name>
   ```
   Example:
   ```bash
   git merge -m "Merging feature into main" feature-branch
   ```

3. **Abort a Merge**:
   ```bash
   git merge --abort
   ```
   Use this if there are conflicts you do not want to resolve.

### Options
- `--no-ff`: Creates a merge commit even if a fast-forward merge is possible.
  ```bash
  git merge --no-ff <branch>
  ```

- `--squash`: Combines all changes into a single commit.
  ```bash
  git merge --squash <branch>
  ```

- `--abort`: Cancels the merge process.
  ```bash
  git merge --abort
  ```

- `--commit`: Completes the merge with a merge commit.

- `-m <message>`: Adds a custom message to the merge commit.

- `--strategy=<strategy>`: Specifies a merge strategy (e.g., `recursive`, `ours`, `theirs`).
  ```bash
  git merge --strategy=recursive <branch>
  ```

### Examples
- Merge `development` into `main`:
  ```bash
  git merge development
  ```

- Merge with a commit message:
  ```bash
  git merge -m "Merging hotfix" hotfix-branch
  ```

- Perform a squash merge:
  ```bash
  git merge --squash feature-enhancement
  ```

- Abort an ongoing merge:
  ```bash
  git merge --abort
  ```

### Notes
- Resolve conflicts manually if they arise during a merge. Use `git status` to see the conflicting files.
- After resolving conflicts, complete the merge using:
  ```bash
  git commit
  ```
- Avoid merging too frequently without testing to maintain repository stability.
---

## Git Rebase

The `git rebase` command is used to reapply commits from one branch onto another, effectively rewriting the commit history. It is commonly used to maintain a linear project history and integrate changes more cleanly.

### Syntax
```bash
git rebase [options] <upstream>
```

### Common Use Cases
1. **Rebase the Current Branch onto Another Branch**:
   ```bash
   git rebase <branch>
   ```
   Example:
   ```bash
   git rebase main
   ```

2. **Interactive Rebase to Edit Commit History**:
   ```bash
   git rebase -i <commit>
   ```
   Example:
   ```bash
   git rebase -i HEAD~3
   ```
   This opens an editor where you can modify, reorder, or squash commits.

3. **Continue a Stopped Rebase**:
   ```bash
   git rebase --continue
   ```
   Use this after resolving conflicts during a rebase.

4. **Abort a Rebase**:
   ```bash
   git rebase --abort
   ```
   This restores the branch to its original state before the rebase started.

### Options
- `-i` or `--interactive`: Starts an interactive rebase session, allowing you to edit the commit history.
  ```bash
  git rebase -i <commit>
  ```

- `--onto <new-base>`: Rebases the branch onto a different base.
  ```bash
  git rebase --onto <new-base> <upstream> <branch>
  ```
  Example:
  ```bash
  git rebase --onto main feature-branch-old feature-branch-new
  ```

- `--continue`: Continues the rebase after conflicts are resolved.

- `--skip`: Skips the current conflicting commit and proceeds with the rebase.
  ```bash
  git rebase --skip
  ```

- `--abort`: Aborts the rebase and restores the branch to its original state.

- `--preserve-merges`: Preserves merge commits during a rebase.
  ```bash
  git rebase --preserve-merges main
  ```

- `--no-ff`: Ensures that no fast-forward merges are performed during the rebase.

### Examples
- Rebase the current branch onto `development`:
  ```bash
  git rebase development
  ```

- Start an interactive rebase to modify the last 5 commits:
  ```bash
  git rebase -i HEAD~5
  ```

- Rebase `feature-branch` onto `main`:
  ```bash
  git rebase --onto main development feature-branch
  ```

- Skip a conflicting commit during a rebase:
  ```bash
  git rebase --skip
  ```

- Abort a rebase and undo all changes:
  ```bash
  git rebase --abort
  ```

  ### Notes
- Use `git rebase` with caution when working on shared branches as it rewrites commit history.
- To avoid conflicts, ensure your branch is up to date with the target branch before rebasing:
  ```bash
  git fetch origin
  git rebase origin/main
  ```
- After rebasing, force-push the changes to the remote repository:
  ```bash
  git push --force
  ```
---

## Git Cherry-Pick

The `git cherry-pick` command is used to apply a specific commit from one branch onto another. It allows you to select specific changes without merging the entire branch.

### Syntax
```bash
git cherry-pick [options] <commit-hash>
```

### Common Use Cases
1. **Apply a Single Commit to the Current Branch**:
   ```bash
   git cherry-pick <commit-hash>
   ```
   Example:
   ```bash
   git cherry-pick a1b2c3d4
   ```

2. **Apply a Range of Commits**:
   ```bash
   git cherry-pick <start-commit>^..<end-commit>
   ```
   Example:
   ```bash
   git cherry-pick f1e2d3c4^..g5h6i7j8
   ```

3. **Apply Multiple Non-Sequential Commits**:
   ```bash
   git cherry-pick <commit1> <commit2> <commit3>
   ```
   Example:
   ```bash
   git cherry-pick a1b2c3d4 f5e6d7c8 g9h0i1j2
   ```

### Options
- `-e` or `--edit`: Allows you to modify the commit message before applying it.
  ```bash
  git cherry-pick -e <commit-hash>
  ```

- `-n` or `--no-commit`: Applies the changes without committing them.
  ```bash
  git cherry-pick -n <commit-hash>
  ```

- `--continue`: Continues the cherry-pick after resolving conflicts.
  ```bash
  git cherry-pick --continue
  ```

- `--abort`: Aborts the cherry-pick and restores the branch to its original state.
  ```bash
  git cherry-pick --abort
  ```

- `--skip`: Skips the current conflicting commit and proceeds with the next one.
  ```bash
  git cherry-pick --skip
  ```

### Examples
- Apply a specific commit to the current branch:
  ```bash
  git cherry-pick 123abc
  ```

- Apply a range of commits from another branch:
  ```bash
  git cherry-pick feature-branch^..main
  ```

- Modify the commit message while cherry-picking:
  ```bash
  git cherry-pick -e 456def
  ```

- Cherry-pick without committing the changes:
  ```bash
  git cherry-pick -n 789ghi
  ```

- Continue a stopped cherry-pick after resolving conflicts:
  ```bash
  git cherry-pick --continue
  ```

### Notes
- `git cherry-pick` is useful when you want to backport specific fixes or features to a different branch.
- Use `git log` or `git reflog` to find the commit hashes you want to cherry-pick.
- Be cautious when cherry-picking changes across branches with different histories, as it may lead to conflicts.

---
