# Git / Github Commands

## **Git Init**

The `git init` command initializes a new Git repository in the specified directory. This command creates a `.git` folder that contains all the metadata and history for the repository.

#### **Usage**:
```bash
git init [directory]
```

- If no directory is specified, it initializes the current folder.

#### **Options**:
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

## **Git Status**
The `git status` command displays the state of the working directory and staging area. It shows which changes have been staged, which have not, and which files are not being tracked by Git.

#### **Usage**:
```bash
git status [options]
```

#### **Options**:
- `--short`: Provides a brief summary of the status.
  ```bash
  git status --short
  ```
- `--branch`: Displays information about the current branch.
  ```bash
  git status --branch
  ```
- `--ignored`: Lists the ignored files.
  ```bash
  git status --ignored
  ```

---

## **Git add**
The `git add` command adds changes in the working directory to the staging area, preparing them for a commit.

#### **Usage**:
```bash
git add [file-pattern]
```
- To stage all changes:
  ```bash
  git add .
  ```
- To stage a specific file:
  ```bash
  git add <file-name>
  ```

#### **Options**:
- `-n` or `--dry-run`: Shows what files would be added without actually staging them.
  ```bash
  git add -n
  ```
- `-p` or `--patch`: Interactively stages hunks of changes.
  ```bash
  git add -p
  ```
  For more information about using `git add -p`, refer to this external article: [Explaining git add -p Command with Examples](https://www.slingacademy.com/article/explaining-git-add-p-command-examples)

## **Git log**
The `git log` command displays the commit history of a repository, showing the sequence of commits.

#### **Usage**:
```bash
git log [options]
```

#### **Options**:
- `--oneline`: Displays each commit on one line for brevity.
  ```bash
  git log --oneline
  ```
- `--graph`: Shows a graphical representation of the branch structure.
  ```bash
  git log --graph
  ```
- `--author=<author>`: Filters commits by a specific author.
  ```bash
  git log --author="Author Name"
  ```
- `--since=<date>` and `--until=<date>`: Filters commits within a date range.
  ```bash
  git log --since="2023-01-01" --until="2023-12-31"
  ```
- `-p`: Shows the differences introduced in each commit.
  ```bash
  git log -p
  ```

## **Git commit**
The `git commit` command saves the staged changes to the repository, creating a new commit.

#### **Usage**:
```bash
git commit -m "Commit message"
```

#### **Options**:
- `-m <message>`: Adds a commit message directly.
  ```bash
  git commit -m "Initial commit"
  ```
- `-a`: Automatically stages tracked files before committing.
  ```bash
  git commit -a -m "Updated files"
  ```
- `--amend`: Modifies the most recent commit, including its message.
  ```bash
  git commit --amend -m "Updated commit message"
  ```
- `--no-edit`: Amends the last commit without changing its message.
  ```bash
  git commit --amend --no-edit
  ```

---

## **Git Diff**

### **`git diff`**
The `git diff` command displays the differences between various states of a Git repository.

#### **What It Does**:
- Shows changes in the working directory that have not yet been staged.
- Displays differences between the staging area and the last commit.
- Compares two specific commits or branches.

#### **Usage**:
```bash
git diff [options]
```

#### **Options**:
- Compare working directory to staging area:
  ```bash
  git diff
  ```
- Compare staging area to the last commit:
  ```bash
  git diff --cached
  ```
  - Compare staging area to the last staged commit:
  ```bash
  git diff --staged
  ```
- Compare two commits:
  ```bash
  git diff <commit1> <commit2>
  ```
- Compare changes for a specific file:
  ```bash
  git diff <file-name>
  ```
- `--stat`: Displays a summary of changes with the number of insertions and deletions.
  ```bash
  git diff --stat
  ```
- `--name-only`: Shows only the names of changed files.
  ```bash
  git diff --name-only
  ```
- `-p`: Displays the patch format of the changes.
  ```bash
  git diff -p
  ```
- `--color`: Forces colored output for better readability.
  ```bash
  git diff --color
  ```

---

## **Git Remove (Git RM)**

### **`git rm`**
The `git rm` command is used to remove files from both the working directory and the staging area.

#### **What It Does**:
- Deletes the specified files from the working directory.
- Stages the removal of these files, so the deletion is recorded in the next commit.

#### **Usage**:
```bash
git rm [options] <file-name>
```

#### **Options**:
- Remove a file and stage the removal:
  ```bash
  git rm <file-name>
  ```
- Remove multiple files:
  ```bash
  git rm file1 file2
  ```
- `--cached`: Removes the file only from the staging area while keeping it in the working directory.
  ```bash
  git rm --cached <file-name>
  ```
- `-f` or `--force`: Forces the removal of a file.
  ```bash
  git rm -f <file-name>
  ```
- `--dry-run`: Shows what files would be removed without actually deleting them.
  ```bash
  git rm --dry-run <file-name>
  ```

---

## **Git Checkout**

### **`git checkout`**
The `git checkout` command is used to switch between branches or restore files in a Git repository.

#### **What It Does**:
- Switches to an existing branch.
- Creates a new branch and switches to it (with `-b` option).
- Restores a specific file or files to a previous state.

#### **Usage**:
```bash
git checkout [options] <branch-name>
```

#### **Options**:
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

## Git Revert

### `git revert`
The `git revert` command is used to undo changes in a Git repository by creating a new commit that reverses the changes introduced by a previous commit.

#### What It Does:
- Reverts changes made by a specific commit.
- Creates a new commit to record the reversal.
- Does not alter the commit history (unlike `git reset`).

#### Usage:
```bash
git revert [options] <commit-hash>
```

#### Options:
- Revert a specific commit:
  ```bash
  git revert <commit-hash>
  ```
- Revert multiple commits interactively:
  ```bash
  git revert -i <commit-range>
  ```
- Abort a revert operation in progress:
  ```bash
  git revert --abort
  ```
- Revert a commit without creating a new commit (apply changes to the working directory):
  ```bash
  git revert --no-commit <commit-hash>
  ```
- Edit the commit message for the revert:
  ```bash
  git revert --edit <commit-hash>
  ```

---

## Git Reset

### `git reset`
The `git reset` command is used to undo changes in a Git repository by moving the current branch’s HEAD to a specific state, effectively resetting the repository to that point. It modifies the staging area (index) and the working directory depending on the options used. Unlike `git revert`, which creates a new commit to reverse changes, `git reset` can alter the commit history by removing commits from the current branch.

#### What It Does:
- **Moves the HEAD**: It changes the current branch’s HEAD to a specific commit.
- **Modifies the Staging Area**: It can modify the index (staging area) to match the new commit.
- **Modifies the Working Directory**: It can update the working directory to reflect the state of the commit.

#### Usage:
```bash
git reset [options] <commit-hash>
```

#### Options:
1. **Soft Reset (`--soft`)**:
   - Moves the HEAD to a specified commit but **keeps changes in the staging area**. This allows you to amend or commit those changes later.
   - **Usage**:
     ```bash
     git reset --soft <commit-hash>
     ```
   - **Use Case**: If you want to undo a commit but keep the changes staged for a new commit.

2. **Mixed Reset (`--mixed`)** (default option):
   - Moves the HEAD to a specified commit and **unstages** changes (removes changes from the staging area) but keeps the modifications in the working directory.
   - **Usage**:
     ```bash
     git reset --mixed <commit-hash>
     ```
   - **Use Case**: If you want to unstage changes and leave them in your working directory.

3. **Hard Reset (`--hard`)**:
   - Moves the HEAD to a specified commit and **resets both the staging area and working directory** to match the specified commit. Any uncommitted changes are lost.
   - **Usage**:
     ```bash
     git reset --hard <commit-hash>
     ```
   - **Use Case**: If you want to discard changes completely and reset to a specific commit. **Warning**: This is destructive and can lead to data loss if there are uncommitted changes.

4. **Keep Reset (`--keep`)**:
   - Resets the HEAD and updates the staging area to match the specified commit, but **keeps changes in the working directory**. If there are conflicting changes, it prevents the reset from happening.
   - **Usage**:
     ```bash
     git reset --keep <commit-hash>
     ```
   - **Use Case**: If you want to reset the staging area to a previous commit but keep changes in the working directory without discarding any conflicting changes.

5. **Merge Reset (`--merge`)**:
   - Similar to the `--keep` option, but it allows resetting with a little more flexibility. It preserves the working directory and attempts to preserve the index (staging area), but conflicts may arise when there are changes in both the commit history and the working directory.
   - **Usage**:
     ```bash
     git reset --merge <commit-hash>
     ```
   - **Use Case**: When you want to reset the branch to a specific state but want to preserve most of your current changes.

6. **Reset to the Previous Commit**:
   - To reset to the previous commit, you can use the shorthand `HEAD~1`:
     ```bash
     git reset --hard HEAD~1
     ```
   - **Use Case**: This can be helpful to undo the most recent commit and reset your working directory and staging area.

---
