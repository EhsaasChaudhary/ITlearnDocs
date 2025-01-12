# Text Processing Commands

## Overview
Text processing commands in Linux are essential for manipulating and analyzing text files. These commands allow users to filter, extract, transform, and format text efficiently.

---

## Commands and Their Usage

### 1. `grep` - Search for Patterns
- **Description**: Searches for specific patterns in a file or input stream.
- **Examples**:
  ```bash
  # Search for the word 'error' in a file
  $ grep 'error' logfile.txt

  # Search for a pattern recursively in all files in a directory
  $ grep -r 'error' /var/logs

  # Display line numbers with matches
  $ grep -n 'error' logfile.txt

  # Ignore case during search
  $ grep -i 'error' logfile.txt
  ```
- **Options**:
  - `-r`: Recursive search.
  - `-i`: Case-insensitive search.
  - `-n`: Show line numbers.
  - `-v`: Invert match (show lines that do not match).

---

### 2. `sed` - Stream Editor
- **Description**: Edits text in a stream or file line by line.
- **Examples**:
  ```bash
  # Replace 'old' with 'new' in a file
  $ sed 's/old/new/' file.txt

  # Replace globally in each line
  $ sed 's/old/new/g' file.txt

  # Delete lines containing 'error'
  $ sed '/error/d' file.txt

  # Edit file in-place
  $ sed -i 's/old/new/g' file.txt
  ```
- **Options**:
  - `-i`: Edit file in-place.
  - `-e`: Execute multiple commands.
  - `-n`: Suppress automatic printing of pattern space.

---

### 3. `awk` - Pattern Scanning and Processing
- **Description**: Processes and analyzes text files based on patterns and fields.
- **Examples**:
  ```bash
  # Print the first column of a file
  $ awk '{print $1}' file.txt

  # Print lines where the second column equals 100
  $ awk '$2 == 100' file.txt

  # Sum the values in the second column
  $ awk '{sum += $2} END {print sum}' file.txt

  # Use a custom delimiter
  $ awk -F: '{print $1}' /etc/passwd
  ```
- **Options**:
  - `-F`: Specify field separator.
  - `-v`: Assign a variable.
  - `-f`: Read program from a file.

---

### 4. `cut` - Extract Specific Fields
- **Description**: Extracts specific columns or fields from a file or input stream.
- **Examples**:
  ```bash
  # Extract the first 10 characters of each line
  $ cut -c 1-10 file.txt

  # Extract the second column using a tab delimiter
  $ cut -f2 file.txt

  # Use a custom delimiter (colon in this case)
  $ cut -d':' -f1 /etc/passwd
  ```
- **Options**:
  - `-c`: Extract specific characters.
  - `-f`: Extract specific fields.
  - `-d`: Specify delimiter.

---

### 5. `sort` - Sort Lines of Text
- **Description**: Sorts lines in text files based on specified criteria.
- **Examples**:
  ```bash
  # Sort a file alphabetically
  $ sort file.txt

  # Sort a file numerically
  $ sort -n file.txt

  # Sort in reverse order
  $ sort -r file.txt

  # Sort based on a specific column
  $ sort -k2 file.txt
  ```
- **Options**:
  - `-n`: Numeric sort.
  - `-r`: Reverse order.
  - `-k`: Specify column.

---

### 6. `uniq` - Remove Duplicate Lines
- **Description**: Filters out duplicate lines in a file.
- **Examples**:
  ```bash
  # Remove duplicate lines (file must be sorted first)
  $ uniq file.txt

  # Show counts of duplicate lines
  $ uniq -c file.txt

  # Ignore case during comparison
  $ uniq -i file.txt
  ```
- **Options**:
  - `-c`: Show counts of duplicates.
  - `-i`: Ignore case.
  - `-d`: Only show duplicate lines.

---

### 7. `tr` - Translate or Delete Characters
- **Description**: Translates or deletes characters in a stream.
- **Examples**:
  ```bash
  # Replace all lowercase letters with uppercase
  $ echo 'hello' | tr 'a-z' 'A-Z'

  # Delete all digits from input
  $ echo '123abc456' | tr -d '0-9'

  # Replace spaces with underscores
  $ echo 'hello world' | tr ' ' '_'
  ```
- **Options**:
  - `-d`: Delete characters.
  - `-s`: Squeeze repeated characters.

---

### 8. `wc` - Word, Line, and Character Count
- **Description**: Counts lines, words, and characters in a file.
- **Examples**:
  ```bash
  # Count lines
  $ wc -l file.txt

  # Count words
  $ wc -w file.txt

  # Count characters
  $ wc -c file.txt

  # Count all (lines, words, characters)
  $ wc file.txt
  ```
- **Options**:
  - `-l`: Count lines.
  - `-w`: Count words.
  - `-c`: Count characters.

---

## Practice Examples
Here are steps to practice text processing commands:

1. **Create a Sample Text File**:
   ```bash
   echo -e "line1: hello world\nline2: linux commands\nline3: text processing" > sample.txt
   ```

2. **Practice with `grep`**:
   ```bash
   # Find lines containing the word 'line'
   grep 'line' sample.txt

   # Find lines containing 'hello' ignoring case
   grep -i 'hello' sample.txt
   ```

3. **Practice with `sed`**:
   ```bash
   # Replace 'hello' with 'hi'
   sed 's/hello/hi/' sample.txt

   # Delete lines containing 'linux'
   sed '/linux/d' sample.txt
   ```

4. **Practice with `awk`**:
   ```bash
   # Print the first word of each line
   awk '{print $1}' sample.txt

   # Print lines where the second column is 'commands'
   awk '$2 == "commands"' sample.txt
   ```

5. **Practice with `cut`**:
   ```bash
   # Extract the first 5 characters of each line
   cut -c 1-5 sample.txt

   # Extract the second field using ':' as a delimiter
   cut -d':' -f2 sample.txt
   ```

6. **Combine Commands**:
   ```bash
   # Extract lines containing 'line', replace 'line' with 'Line', and save to a new file
   grep 'line' sample.txt | sed 's/line/Line/' > output.txt
   ```

---

## Summary
These text processing commands are powerful tools for analyzing and manipulating text data in Linux. Mastering them can significantly improve your efficiency and capability when working with text files.
