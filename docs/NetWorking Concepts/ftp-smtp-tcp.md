# Overview of FTP, SMTP, and TCP/IP Protocols

## **FTP (File Transfer Protocol)**

### What It Is:
- FTP is a protocol for transferring files between a client and a server on a network.
- It uses a client-server model and typically operates on ports 20 and 21.

### How It Works:
1. A client establishes a connection with an FTP server.
2. Files can be uploaded, downloaded, or manipulated on the server.
3. It supports active and passive modes for data transfer.

### Use Cases:
- Website maintenance (uploading files to a web server).
- Sharing files across systems in a controlled environment.

### Commands and Examples:
1. **Connect to an FTP server:**
   ```bash
   ftp ftp.example.com
   ```
   - Prompts for username and password.

   **Local Test:**
   - Install an FTP server (e.g., FileZilla Server) on your system.
   - Start the server and use `ftp 127.0.0.1` to connect locally.

2. **List files in the current directory on the server:**
   ```bash
   ls
   ```
   **Local Test:**
   - Ensure the FTP server directory contains files to test listing.

3. **Download a file from the server:**
   ```bash
   get filename.txt
   ```
   **Local Test:**
   - Place a file in the server directory and download it to your local system.

4. **Upload a file to the server:**
   ```bash
   put localfile.txt
   ```
   **Local Test:**
   - Use a local file and verify it appears in the FTP server directory after upload.

5. **Exit FTP:**
   ```bash
   bye
   ```

---

## **SMTP (Simple Mail Transfer Protocol)**

### What It Is:
- SMTP is used to send emails across the internet.
- Operates on port 25 (default), 465 (secure), or 587 (submission).

### How It Works:
1. The client sends an email to an SMTP server.
2. The server forwards the email to the recipient's mail server.
3. The recipient retrieves the email using protocols like POP3 or IMAP.

### Use Cases:
- Sending automated emails (notifications, alerts).
- Testing email server configurations.

### Commands and Examples:
1. **Test SMTP using `telnet`:**
   ```bash
   telnet smtp.example.com 25
   ```
   - Opens a connection to the SMTP server.

   **Local Test:**
   - Install a mail server (e.g., Postfix or Sendmail) locally.
   - Use `telnet 127.0.0.1 25` to connect to the local server.

2. **Send an email manually (example):**
   ```bash
   HELO domain.com
   MAIL FROM: <sender@example.com>
   RCPT TO: <recipient@example.com>
   DATA
   Subject: Test Email
   This is a test email.
   .
   QUIT
   ```
   **Local Test:**
   - Configure your local mail server to accept emails and verify that emails are logged or delivered.

3. **Check server response:**
   - Server responds with status codes like `250` (OK) or `550` (Error).

   **Local Test:**
   - Use logs from the local mail server to analyze responses.

---

## **TCP/IP (Transmission Control Protocol/Internet Protocol)**

### What It Is:
- TCP/IP is a suite of communication protocols used to connect devices on a network.
- TCP ensures reliable delivery, while IP handles addressing and routing.

### How It Works:
1. TCP breaks data into packets and ensures they are delivered reliably.
2. IP ensures packets are routed and addressed to the correct destination.
3. Together, they form the backbone of internet communication.

### Use Cases:
- Ensuring reliable data transmission (e.g., web browsing, email).
- Network diagnostics and connectivity tests.

### Commands and Examples:
1. **Check if a port is open (using `netcat`):**
   ```bash
   nc -zv google.com 443
   ```
   - Tests if port 443 (HTTPS) on Google is reachable.

   **Local Test:**
   - Run a local server (e.g., Python's HTTP server) using: 
   ```bash
   python -m http.server 808
   ```
   - Check port connectivity using:
   ```bash
    nc -zv 127.0.0.1 8080
   ```

2. **Ping a server to check connectivity:**
   ```bash
   ping example.com
   ```
   **Local Test:**
   - Use `ping 127.0.0.1` to test connectivity to your local system.

3. **View TCP/IP configuration:**
   ```bash
   ifconfig (Linux/macOS)
   ipconfig (Windows)
   ```
   **Local Test:**
   - Run the command to view network details of your local machine.

4. **Trace the route packets take to a server:**
   ```bash
   traceroute example.com (Linux/macOS)
   tracert example.com (Windows)
   ```
   **Local Test:**
   - Use `traceroute 127.0.0.1` or `tracert 127.0.0.1` to trace routes to your own system.

---

## **Key Differences:**

| Protocol | Purpose                       | Common Ports | Tools/Commands         |
|----------|-------------------------------|--------------|------------------------|
| **FTP**  | File transfers                | 20, 21       | `ftp`, `sftp`, `curl` |
| **SMTP** | Sending emails                | 25, 465, 587 | `telnet`, `sendmail`  |
| **TCP/IP**| Data communication backbone  | Various      | `ping`, `netcat`      |

These protocols form the foundation of internet and network communication.
---
