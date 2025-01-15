## Git Revert

### `git revert`
The `git revert` command is used to undo changes in a Git repository by creating a new commit that reverses the changes introduced by a previous commit.

### What It Does:
- Reverts changes made by a specific commit.
- Creates a new commit to record the reversal.
- Does not alter the commit history (unlike `git reset`).

### Usage:
```bash
git revert [options] <commit-hash>
```

### Options:
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

### What It Does:
- **Moves the HEAD**: It changes the current branch’s HEAD to a specific commit.
- **Modifies the Staging Area**: It can modify the index (staging area) to match the new commit.
- **Modifies the Working Directory**: It can update the working directory to reflect the state of the commit.

### Usage:
```bash
git reset [options] <commit-hash>
```

### Options:
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

## Git Stash

The `git stash` command temporarily shelves changes in your working directory so you can work on something else without committing the changes.

### Syntax
```bash
git stash [options]
```

### Common Use Cases
1. **Save Changes**:
   ```bash
   git stash
   ```
   Temporarily saves all changes in the working directory.

2. **List Stashes**:
   ```bash
   git stash list
   ```
   Displays a list of all saved stashes.

3. **Apply Stashed Changes**:
   ```bash
   git stash apply
   ```
   Reapplies the most recent stash to your working directory.

4. **Apply and Drop Stash**:
   ```bash
   git stash pop
   ```
   Reapplies the most recent stash and removes it from the stash list.

5. **Drop a Specific Stash**:
   ```bash
   git stash drop stash@{index}
   ```
   Removes a specific stash from the list.

6. **Clear All Stashes**:
   ```bash
   git stash clear
   ```
   Deletes all saved stashes.

### Options
- `--keep-index`: Stashes only the changes in the working directory, preserving the staged changes.
  ```bash
  git stash --keep-index
  ```

- `--include-untracked`: Includes untracked files in the stash.
  ```bash
  git stash --include-untracked
  ```

- `--all`: Includes all files (tracked, untracked, and ignored) in the stash.
  ```bash
  git stash --all
  ```

- `list`: Displays all stashed changes.

- `pop`: Applies the stash and removes it from the stash list.

- `apply`: Reapplies the stash without removing it from the stash list.

- `drop`: Deletes a specific stash by its index.

### Examples
- Save changes and include untracked files:
  ```bash
  git stash --include-untracked
  ```

- Reapply the most recent stash:
  ```bash
  git stash apply
  ```

- Remove all stashes:
  ```bash
  git stash clear
  ```

- View all stashed changes:
  ```bash
  git stash list
  ```

- Apply and remove the most recent stash:
  ```bash
  git stash pop
  ```

- Drop a specific stash:
  ```bash
  git stash drop stash@{1}
  ```

### Notes
- Stashing is useful when you want to switch branches without committing your changes.
- You can stash specific files using:
  ```bash
  git stash push -m "message" <file>
  ```
- Use `git stash show` to view the changes in a stash:
  ```bash
  git stash show -p stash@{0}
  ```
---
