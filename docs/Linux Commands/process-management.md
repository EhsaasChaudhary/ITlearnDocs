# Process Management Commands

## 1. `ps` - Display Process Information
- **Description**: Displays information about the currently running processes.
- **Example**:
  ```bash
  $ ps
  ```
  Output:
  ```
    PID TTY          TIME CMD
   1234 pts/0    00:00:01 bash
   5678 pts/0    00:00:00 ps
  ```
- **Options**:
  - `-e`: Displays all processes.
    ```bash
    $ ps -e
    ```
  - `-f`: Displays full format listing.
    ```bash
    $ ps -f
    ```
  - `-u username`: Displays processes for a specific user.
    ```bash
    $ ps -u feilzz
    ```

---

## 2. `top` - Display Real-Time Process Info
- **Description**: Shows a real-time view of system processes and resource usage.
- **Example**:
  ```bash
  $ top
  ```
  - Press `q` to quit.
- **Options**:
  - `-d seconds`: Sets the delay between updates.
    ```bash
    $ top -d 5
    ```
  - `-u username`: Displays processes for a specific user.
    ```bash
    $ top -u feilzz
    ```

---

## 3. `kill` - Terminate Processes
- **Description**: Sends signals to terminate or control processes.
- **Example**:
  ```bash
  $ kill 1234
  ```
  Terminates the process with PID 1234.
- **Options**:
  - `-9`: Forcefully kills a process.
    ```bash
    $ kill -9 1234
    ```
  - `-l`: Lists all available signals.
    ```bash
    $ kill -l
    ```

---

## 4. `jobs` - Display Background Jobs
- **Description**: Lists all background jobs in the current session.
- **Example**:
  ```bash
  $ jobs
  ```
  Output:
  ```
  [1]+  Running    sleep 100 &
  ```
- **Options**:
  - `-l`: Displays process IDs of jobs.
    ```bash
    $ jobs -l
    ```

---

## 5. `fg` - Bring Background Job to Foreground
- **Description**: Resumes a background job in the foreground.
- **Example**:
  ```bash
  $ fg %1
  ```
  Brings job 1 to the foreground.

---

## 6. `bg` - Resume Background Job
- **Description**: Resumes a stopped job in the background.
- **Example**:
  ```bash
  $ bg %1
  ```
  Resumes job 1 in the background.
  
---

## 7. `htop` - Interactive Process Viewer
- **Description**: Provides an interactive and visual view of system processes and resource usage.
- **Example**:
  ```bash
  $ htop
  ```
  Opens an interactive interface showing CPU, memory usage, and running processes.
- **Options**:
  - `-u <username>`: Show processes for a specific user.
    ```bash
    $ htop -u feilzz
    ```
  - `--sort-key`: Sort by a specific column (e.g., `%CPU`).
    ```bash
    $ htop --sort-key=%CPU
    ```

---

## 8. `pkill` - Kill Processes by Name
- **Description**: Terminates processes based on their name.
- **Example**:
  ```bash
  $ pkill firefox
  ```
  Kills all processes with the name `firefox`.
- **Options**:
  - `-u <username>`: Kill processes belonging to a specific user.
    ```bash
    $ pkill -u feilzz
    ```
  - `-signal`: Specify a signal to send (e.g., `SIGKILL`).
    ```bash
    $ pkill -9 firefox
    ```

---

## 9. `nice` - Set Process Priority
- **Description**: Launches a process with a specified priority level.
- **Example**:
  ```bash
  $ nice -n 10 myprogram
  ```
  Runs `myprogram` with a priority of `10`.
- **Options**:
  - `-n <priority>`: Specify the priority level (-20 is the highest, 19 is the lowest).
    ```bash
    $ nice -n -5 myprogram
    ```

---

## 10. `renice` - Change Process Priority
- **Description**: Changes the priority of a running process.
- **Example**:
  ```bash
  $ renice 5 -p 1234
  ```
  Changes the priority of process `1234` to `5`.
- **Options**:
  - `-p <pid>`: Specify the process ID.
    ```bash
    $ renice -10 -p 5678
    ```
  - `-u <username>`: Change priority for all processes of a user.
    ```bash
    $ renice 15 -u feilzz
    ```

---

## 11. `uptime` - Show System Uptime
- **Description**: Displays how long the system has been running along with load averages.
- **Example**:
  ```bash
  $ uptime
  ```
  Output: `09:45:12 up 1 day, 3:45, 2 users, load average: 0.00, 0.01, 0.05`
- **Options**:
  - None specific, but it's often used in scripts to check system stability.

---

## 12. `watch` - Run Command Periodically
- **Description**: Executes a command repeatedly at a set interval, showing the output.
- **Example**:
  ```bash
  $ watch -n 2 df -h
  ```
  Runs `df -h` every 2 seconds, showing disk usage.
- **Options**:
  - `-n <seconds>`: Set the interval in seconds.
    ```bash
    $ watch -n 5 ls
    ```
  - `-d`: Highlight differences between updates.
    ```bash
    $ watch -d free
    ```
---

## Usage Notes
These commands are essential for monitoring, controlling, and managing processes on a Linux system. They provide both real-time and static views of process activity.
