# Linux Commands for File Operations in CLI

## 1. `cat`
The `cat` command is used to display the contents of a file, combine multiple files, or create a new file.

### Examples:
1. Display a file's content:
   ```bash
   cat filename.txt
   ```
2. Concatenate multiple files and display the result:
   ```bash
   cat file1.txt file2.txt
   ```
3. Create a new file (Ctrl+D to save):
   ```bash
   cat > newfile.txt
   ```

## 2. `less`
The `less` command lets you view a file one screen at a time.

### Steps to Use:
1. Move to the next item: Press `n`
2. Move to the top: Press `Shift + G`
3. Move to the bottom: Press `g`
4. Search forward: Type `/search_term`
5. Search backward: Type `?search_term`
6. Exit: Press `q`

### Example:
- View a file:
  ```bash
  less filename.txt
  ```

## 3. `more`
The `more` command is similar to `less` but has fewer features. It allows you to view a file one screen at a time.

### Example:
1. View a file:
   ```bash
   more filename.txt
   ```
2. Scroll one line at a time: Press `Enter`
3. Scroll one page at a time: Press `Space`
4. Exit: Press `q`

## 4. `touch`
The `touch` command is used to create an empty file or update the timestamp of an existing file.

### Example:
1. Create a new file:
   ```bash
   touch newfile.txt
   ```
2. Update a file's timestamp:
   ```bash
   touch existingfile.txt
   ```

## 5. `rm`
The `rm` command is used to delete files or directories.

### Examples:
1. Delete a file:
   ```bash
   rm filename.txt
   ```
2. Delete multiple files:
   ```bash
   rm file1.txt file2.txt
   ```
3. Delete a directory and its contents recursively:
   ```bash
   rm -r directory_name
   ```
4. Force delete without confirmation:
   ```bash
   rm -rf directory_name
   ```

## 6. `vi`
The `vi` editor is a powerful text editor available on most Linux systems.

### Steps to Use:
1. Open a file in `vi`:
   ```bash
   vi filename.txt
   ```
2. Press `i` to enter insert (edit) mode.
3. Make your changes.
4. Press `Esc` to exit insert mode.
5. Save the file and exit:
   - Save changes: `:w`
   - Save and exit: `:wq`
   - Exit without saving: `:q!`

### Example:
- Open and edit a file:
  ```bash
  vi filename.txt
  ```

## 7. `nano`
The `nano` editor is a simpler text editor compared to `vi`.

### Steps to Use:
1. Open a file in `nano`:
   ```bash
   nano filename.txt
   ```
2. Edit the file as needed.
3. Save the changes:
   - Press `Ctrl + O`, then `Enter` to save.
4. Exit the editor:
   - Press `Ctrl + X` to exit.

### Example:
- Open and edit a file:
  ```bash
  nano filename.txt
  ```
