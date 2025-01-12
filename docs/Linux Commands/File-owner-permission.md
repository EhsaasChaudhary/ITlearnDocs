# File Permissions and Ownership in Linux

## Overview
File permissions and ownership in Linux determine who can read, write, or execute a file or directory. These settings ensure system security and controlled access.

## Commands for Managing File Permissions and Ownership

### 1. `chmod` - Change File Permissions
- **Description**: Modifies the read, write, and execute permissions for files and directories.
- **Examples**:
  ```bash
  # Give read, write, and execute permissions to the owner
  $ chmod u+rwx file.txt

  # Remove write permissions for the group
  $ chmod g-w file.txt

  # Set permissions using numeric notation
  $ chmod 755 file.txt
  ```
- **Options**:
  - `-R`: Apply changes recursively to directories.
    ```bash
    $ chmod -R 755 folder
    ```
  - `--reference`: Apply permissions from a reference file.
    ```bash
    $ chmod --reference=reference.txt target.txt
    ```

---

### 2. `chown` - Change File Ownership
- **Description**: Alters the ownership of a file or directory.
- **Examples**:
  ```bash
  # Change owner to 'user'
  $ chown user file.txt

  # Change owner and group
  $ chown user:group file.txt
  ```
- **Options**:
  - `-R`: Apply changes recursively.
    ```bash
    $ chown -R user:group folder
    ```
  - `--from`: Change ownership only if the current owner matches.
    ```bash
    $ chown --from=current_user new_user file.txt
    ```

---

### 3. `chgrp` - Change Group Ownership
- **Description**: Modifies the group associated with a file or directory.
- **Examples**:
  ```bash
  # Change group to 'developers'
  $ chgrp developers file.txt
  ```
- **Options**:
  - `-R`: Apply changes recursively.
    ```bash
    $ chgrp -R developers folder
    ```
  - `--reference`: Apply group ownership from a reference file.
    ```bash
    $ chgrp --reference=reference.txt target.txt
    ```

---

### 4. `ls -l` - List File Permissions
- **Description**: Displays the permissions of files and directories in a detailed format.
- **Example**:
  ```bash
  $ ls -l file.txt
  -rw-r--r-- 1 user group 1234 Jan 1 10:00 file.txt
  ```
  - The first column (`-rw-r--r--`) shows permissions for owner, group, and others.

---

### 5. `umask` - Default Permissions
- **Description**: Sets the default permissions for new files and directories.
- **Examples**:
  ```bash
  # View current umask value
  $ umask
  0022

  # Set a new umask value
  $ umask 0027
  ```
- **Explanation**: A `umask` value of `0022` means:
  - Owner: Read, write
  - Group: Read-only
  - Others: Read-only

---

### 6. `stat` - Detailed File Information
- **Description**: Provides detailed information about a file, including permissions and ownership.
- **Example**:
  ```bash
  $ stat file.txt
  File: file.txt
  Size: 1234       Blocks: 8          IO Block: 4096   regular file
  Device: 802h/2050d   Inode: 123456    Links: 1
  Access: 2025-01-05 10:00:00.000000000 +0000
  Modify: 2025-01-05 10:00:00.000000000 +0000
  Change: 2025-01-05 10:00:00.000000000 +0000
  Birth: -
  ```

---

### 7. `getfacl` and `setfacl` - Access Control Lists (ACLs)
- **Description**: Manages fine-grained file permissions using ACLs.

#### `getfacl` - View ACLs
- **Example**:
  ```bash
  $ getfacl file.txt
  # file: file.txt
  # owner: user
  # group: group
  user::rw-
  group::r--
  other::r--
  ```

#### `setfacl` - Modify ACLs
- **Examples**:
  ```bash
  # Grant user 'john' read permission
  $ setfacl -m u:john:r file.txt

  # Remove all ACL entries
  $ setfacl -b file.txt
  ```

- **Options**:
  - `-m`: Modify ACL entries.
  - `-x`: Remove specific ACL entries.
  - `-b`: Remove all ACL entries.
  - `-R`: Apply changes recursively.

---

## Acronyms Used
- **ACL**: Access Control List
- **IO Block**: Input/Output Block
- **umask**: User file creation mode mask

---

## Summary
These commands provide robust control over file permissions and ownership, allowing administrators and users to manage access securely and efficiently. By mastering these tools, you can ensure the integrity and confidentiality of your files and directories.
