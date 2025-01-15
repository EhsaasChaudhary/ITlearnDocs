## Git Status
The `git status` command displays the state of the working directory and staging area. It shows which changes have been staged, which have not, and which files are not being tracked by Git.

### **Usage**:
```bash
git status [options]
```

### **Options**:
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

## Git add
The `git add` command adds changes in the working directory to the staging area, preparing them for a commit.

### **Usage**:
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

### **Options**:
- `-n` or `--dry-run`: Shows what files would be added without actually staging them.
  ```bash
  git add -n
  ```
- `-p` or `--patch`: Interactively stages hunks of changes.
  ```bash
  git add -p
  ```
  For more information about using `git add -p`, refer to this external article: [Explaining git add -p Command with Examples](https://www.slingacademy.com/article/explaining-git-add-p-command-examples)
---

## Git log
The `git log` command displays the commit history of a repository, showing the sequence of commits.

### **Usage**:
```bash
git log [options]
```

### **Options**:
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
- `--grep`: Filter based on keywords/ commit message.
  ```bash
  git log --grep="keyword/CM"
  ```
  - `-n`: Filter limited number of commit.
  ```bash
  git log -n 5"
  ```
   - `--pretty`: Customize how the log is displayed:.
  ```bash
  git log --pretty=format:"%h - %an, %ar : %s"
  ```
---
## Git commit
The `git commit` command saves the staged changes to the repository, creating a new commit.

### **Usage**:
```bash
git commit -m "Commit message"
```

### **Options**:
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

## Git Diff

### **`git diff`**
The `git diff` command displays the differences between various states of a Git repository.

### **What It Does**:
- Shows changes in the working directory that have not yet been staged.
- Displays differences between the staging area and the last commit.
- Compares two specific commits or branches.

### **Usage**:
```bash
git diff [options]
```

### **Options**:
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

## Git rm (remove)

### **`git rm`**
The `git rm` command is used to remove files from both the working directory and the staging area.

### **What It Does**:
- Deletes the specified files from the working directory.
- Stages the removal of these files, so the deletion is recorded in the next commit.

### **Usage**:
```bash
git rm [options] <file-name>
```

### **Options**:
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

## Git Tags

Tags are used in Git to mark specific points in a repository's history, often used to indicate release versions (e.g., `v1.0`, `v2.1`). Tags are immutable references to commits.

### Types of Tags

1. **Lightweight Tags**: These are simple pointers to a commit, without any additional metadata.
   ```bash
   git tag <tagname>
   ```
   Example:
   ```bash
   git tag v1.0
   ```

2. **Annotated Tags**: These are stored as full objects in the Git database and include metadata like the tagger's name, email, and date. Annotated tags are recommended for public releases.
   ```bash
   git tag -a <tagname> -m "Tag message"
   ```
   Example:
   ```bash
   git tag -a v1.0 -m "Initial release"
   ```

### Listing Tags
To see all tags in the repository:
```bash
git tag
```

### Deleting Tags
To delete a tag locally:
```bash
git tag -d <tagname>
```

To delete a tag remotely:
```bash
git push origin --delete <tagname>
```

### Pushing Tags to a Remote Repository
To push a single tag:
```bash
git push origin <tagname>
```

To push all tags:
```bash
git push origin --tags
```

### Checking Out a Tag
While tags cannot be directly modified, you can check out a tag to view its associated commit:
```bash
git checkout <tagname>
```
---

## Git Show

The `git show` command is used to display detailed information about Git objects such as commits, tags, or trees. It is commonly used to inspect the details of a specific commit.

### Syntax
```bash
git show <object>
```

### Use Cases
1. **Viewing a Commit**: Displays details of a commit including the author, date, commit message, and changes made.
   ```bash
   git show <commit-hash>
   ```

2. **Viewing a Tag**: Shows information about a specific tag, including its metadata and associated commit.
   ```bash
   git show <tagname>
   ```

3. **Viewing a File at a Specific Commit**: Outputs the content of a file as it existed in a given commit.
   ```bash
   git show <commit-hash>:<filepath>
   ```

### Options
- `--name-only`: Shows only the names of changed files in a commit.
  ```bash
  git show --name-only <commit-hash>
  ```

- `--name-status`: Displays the names of changed files along with their status (added, modified, deleted).
  ```bash
  git show --name-status <commit-hash>
  ```

- `--pretty`: Formats the output. For example:
  ```bash
  git show --pretty=oneline <commit-hash>
  ```

- `--stat`: Shows a summary of changes including file names, insertions, and deletions.
  ```bash
  git show --stat <commit-hash>
  ```

### Examples
- Show the latest commit:
  ```bash
  git show
  ```

- Show details of a specific commit:
  ```bash
  git show 4f2e5a7
  ```

- Show a specific file from a commit:
  ```bash
  git show 4f2e5a7:src/main.java
  ```

### Notes
The `git show` command is a powerful tool for inspecting repository history and understanding changes. It combines commit and diff information for a holistic view of the repository state.

---
