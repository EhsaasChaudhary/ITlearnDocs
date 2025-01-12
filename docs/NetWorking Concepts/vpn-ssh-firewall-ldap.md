
# VPN Overview

## What is VPN?
A Virtual Private Network (VPN) creates a secure, encrypted connection between your device and a remote server. VPNs are commonly used for:

- Securing data transmission over public networks.
- Accessing region-restricted services.
- Hiding your IP address to enhance privacy.

### Common VPN Commands and Examples

#### 1. **OpenVPN Connection**
```bash
sudo openvpn --config myvpn.ovpn
```
*Use Case:* Connect to a VPN using an OpenVPN configuration file.

#### 2. **Check VPN Status**
```bash
nmcli connection show
```
*Use Case:* Display active network connections, including VPN.

#### 3. **Disconnect VPN**
```bash
nmcli connection down <vpn_name>
```
*Use Case:* Terminate the VPN connection.

## Best Practices

- Use strong authentication methods (e.g., certificates).
- Avoid public VPN services for sensitive tasks.
- Regularly update VPN client software.

---

# SSH Overview

## What is SSH?
Secure Shell (SSH) is a cryptographic network protocol for secure communication over an insecure network. It is commonly used for:

- Remote server administration.
- Secure file transfers.
- Port forwarding.

### Common SSH Commands and Examples

#### 1. **SSH to Remote Server**
```bash
ssh user@host
```
*Use Case:* Connect to a remote server using the specified username and host.

#### 2. **Copy Files Securely Using SCP**
```bash
scp file.txt user@host:/path/
scp user@host:/path/file.txt .
```
*Use Case:* Upload or download files securely to/from a remote server.

#### 3. **Generate SSH Key**
```bash
ssh-keygen -t rsa -b 2048
```
*Use Case:* Create an RSA key pair for passwordless authentication.

#### 4. **Copy SSH Key to Remote Server**
```bash
ssh-copy-id user@host
```
*Use Case:* Enable passwordless SSH login to a remote server.

#### 5. **SSH Port Forwarding**
```bash
ssh -L 8080:localhost:80 user@host
```
*Use Case:* Forward a local port (8080) to a remote port (80) via SSH.

#### 6. **Execute Command on Remote Server**
```bash
ssh user@host "ls -la"
```
*Use Case:* Run a command remotely without starting an interactive shell.

## Best Practices

- Use SSH keys instead of passwords.
- Restrict SSH access to specific IPs.
- Disable root login and use non-default ports.


## Advanced Use Cases

### VPN with WireGuard
```bash
sudo wg-quick up wg0
```
*Use Case:* Activate a WireGuard VPN interface.

### SSH Tunneling for Proxying
```bash
ssh -D 9050 user@host
```
*Use Case:* Set up a dynamic SOCKS proxy through an SSH connection.

### Securely Sync Directories with `rsync` over SSH
```bash
rsync -avz -e ssh /local/path/ user@host:/remote/path/
```
*Use Case:* Synchronize directories between a local and remote machine.

---

# Firewall Overview

## What is a Firewall?
A firewall is a network security device or software designed to monitor and control incoming and outgoing traffic based on predefined security rules. Firewalls are commonly used to:

- Protect systems from unauthorized access.
- Control traffic flow within and across networks.
- Prevent malicious attacks and data breaches.

### Types of Firewalls
- **Network Firewalls:** Protect an entire network.
- **Host-Based Firewalls:** Installed on individual devices.
- **Cloud Firewalls:** Protect cloud-based infrastructure.

### Common Firewall Commands and Examples

#### 1. **List Active Rules**
```bash
sudo ufw status
sudo iptables -L
```
*Use Case:* Check active firewall rules.

#### 2. **Allow Traffic on a Port**
```bash
sudo ufw allow 22/tcp
```
*Use Case:* Enable SSH access.

#### 3. **Block Traffic on a Port**
```bash
sudo ufw deny 80/tcp
```
*Use Case:* Block HTTP access.

#### 4. **Enable Firewall**
```bash
sudo ufw enable
```
*Use Case:* Activate the firewall to enforce security policies.

#### 5. **Log Firewall Activity**
```bash
sudo iptables -A INPUT -j LOG
```
*Use Case:* Monitor traffic for analysis and debugging.

#### 6. **Delete a Rule**
```bash
sudo ufw delete allow 22/tcp
```
*Use Case:* Remove an existing rule.

### Advanced Use Cases

#### Temporary Block Using `iptables`
```bash
sudo iptables -I INPUT -s 192.168.1.100 -j DROP
```
*Use Case:* Temporarily block traffic from a specific IP address.

#### Open Multiple Ports
```bash
sudo ufw allow 443,80/tcp
```
*Use Case:* Allow HTTPS and HTTP traffic.

#### Rate Limiting with UFW
```bash
sudo ufw limit 22/tcp
```
*Use Case:* Protect against brute force attacks on SSH.

## Best Practices

### General Firewall Tips
- Regularly review and update firewall rules.
- Use the principle of least privilege (allow only necessary traffic).
- Monitor logs to detect unusual activity.

### UFW Specific
- Enable logging with `sudo ufw logging on`.
- Use `sudo ufw reset` to reset all rules if needed.

### IPTables Specific
- Save rules using `sudo iptables-save > /etc/iptables/rules.v4`.
- Load rules at boot with appropriate system services.

---

# LDAP Overview

## What is LDAP?
The Lightweight Directory Access Protocol (LDAP) is a protocol for accessing and maintaining distributed directory information services over an IP network. LDAP is commonly used for:

- Centralized authentication and authorization.
- Storing user, group, and device information.
- Facilitating single sign-on (SSO) for networked systems.

### Key Features of LDAP
- **Hierarchical Structure:** Data is stored in a tree-like structure.
- **Interoperability:** Works with a variety of systems and platforms.
- **Authentication Support:** Can be integrated with security mechanisms like SASL.


### Common LDAP Commands and Examples

#### 1. **Search LDAP Directory**
```bash
ldapsearch -x -b "dc=example,dc=com"
```
*Use Case:* Query user or group information from the directory.

#### 2. **Bind to LDAP Server**
```bash
ldapwhoami -x -D "cn=admin,dc=example,dc=com" -W
```
*Use Case:* Authenticate against an LDAP server.

#### 3. **Add LDAP Entry**
```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f entry.ldif
```
*Use Case:* Add new users or groups to the directory.

#### 4. **Modify LDAP Entry**
```bash
ldapmodify -x -D "cn=admin,dc=example,dc=com" -W -f modify.ldif
```
*Use Case:* Update attributes of an existing user or group.

#### 5. **Delete LDAP Entry**
```bash
ldapdelete -x -D "cn=admin,dc=example,dc=com" -W "cn=user,dc=example,dc=com"
```
*Use Case:* Remove obsolete entries from the directory.

### Advanced Use Cases

#### Bulk Import Entries
```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f bulk.ldif
```
*Use Case:* Add multiple entries at once using an LDIF file.

#### Search with Filters
```bash
ldapsearch -x -b "dc=example,dc=com" "(&(objectClass=person)(uid=jdoe))"
```
*Use Case:* Find specific entries based on attributes.

#### Change User Password
```bash
ldappasswd -x -D "cn=admin,dc=example,dc=com" -W -s newpassword "uid=jdoe,dc=example,dc=com"
```
*Use Case:* Reset a user's password.

#### Export Entire Directory
```bash
ldapsearch -x -LLL -b "dc=example,dc=com" > backup.ldif
```
*Use Case:* Backup all directory data to an LDIF file.

#### Delete All Entries Under a Branch
```bash
ldapdelete -x -D "cn=admin,dc=example,dc=com" -W "ou=groups,dc=example,dc=com"
```
*Use Case:* Remove all entries within a specific branch of the directory.

## Best Practices

### General LDAP Tips
- Use strong administrative passwords and secure connections (e.g., LDAPS).
- Regularly back up directory data.
- Implement access controls to restrict sensitive data.

### Schema Management
- Extend schemas carefully to ensure compatibility.
- Use tools like `slapcat` for schema validation.

### Monitoring and Maintenance
- Enable logging for audit purposes.
- Monitor performance and tune configurations for large directories.
---
