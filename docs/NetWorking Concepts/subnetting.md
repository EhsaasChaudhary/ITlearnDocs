# Subnetting: Commands and Examples

## Understanding Subnetting

### What is Subnetting?
Subnetting is the process of dividing a larger network (or IP address block) into smaller, more manageable sub-networks, known as subnets. This is done to improve network performance, enhance security, and better utilize IP address space.

### Why Subnetting is Needed?
1. **Efficient IP Address Utilization**: Prevents wastage of IP addresses.
2. **Improved Performance**: Reduces network congestion by limiting the size of broadcast domains.
3. **Enhanced Security**: Isolates subnets, ensuring only specific communication is allowed.
4. **Simplifies Management**: Makes it easier to manage a large network.

### How Does Subnetting Work?
1. **Divide the Network**: Use subnet masks to split an IP range into smaller subnets.
2. **Assign IPs**: Allocate IP addresses to devices within each subnet.
3. **Route Traffic**: Configure routers to handle communication between subnets.
   
- **Subnet Mask**: Defines which portion of an IP address is the network ID and which part is the host ID. 
  - Example: For `192.168.1.0/24`, the subnet mask is `255.255.255.0`, meaning the first 24 bits are the network portion, and the last 8 bits are for host addresses.
  
- **CIDR Notation**: `/24` represents the subnet mask's bit length.

- **Dividing a Network**: Network divided into Network address, broadcast address, host address.
  - **Network Address**: Identifies the subnet.
  - **Broadcast Address**: Used to send messages to all hosts in a subnet.
  - **Host Addresses**: Usable IPs for devices.

### Impact of Subnetting on a Network
- Limits the number of devices per subnet.
- Helps segregate traffic, improving speed and security.
- Requires routers to manage communication between subnets.

---

## Setting Up a Subnet

### 1. Planning Subnets
Suppose you have `192.168.1.0/24` and need:
- 2 subnets for 50 devices each.
- 1 subnet for 20 devices.

| Subnet | Required Hosts | Subnet Mask       | Network Address  | Broadcast Address | Host Range            |
|--------|----------------|-------------------|------------------|-------------------|-----------------------|
| A      | 50             | 255.255.255.192 (/26) | 192.168.1.0      | 192.168.1.63     | 192.168.1.1 - 192.168.1.62 |
| B      | 50             | 255.255.255.192 (/26) | 192.168.1.64     | 192.168.1.127    | 192.168.1.65 - 192.168.1.126 |
| C      | 20             | 255.255.255.224 (/27) | 192.168.1.128    | 192.168.1.159    | 192.168.1.129 - 192.168.1.158 |

---

## Commands Related to Subnetting

### 1. Calculate Subnets

Use tools to calculate subnets for an IP range.

#### Example:
```bash
ipcalc 192.168.1.0/24
```
Output:
```
Address:   192.168.1.0          11000000.10101000.00000001. 00000000
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   192.168.1.0/24       11000000.10101000.00000001. 00000000
HostMin:   192.168.1.1          11000000.10101000.00000001. 00000001
HostMax:   192.168.1.254        11000000.10101000.00000001. 11111110
Broadcast: 192.168.1.255        11000000.10101000.00000001. 11111111
Hosts/Net: 254                   Class C
```

---

### 2. Add a Static Route

To enable communication between subnets:

#### Example:
```bash
sudo route add -net 192.168.2.0/24 gw 192.168.1.1
```

This adds a route for the `192.168.2.0/24` subnet through gateway `192.168.1.1`.

---

### 3. View Network Information

To view routing table and network configuration:

#### Example:
```bash
ip route
```
Output:
```
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.1
192.168.2.0/24 via 192.168.1.1 dev eth0
```

---

### 4. Enable IP Forwarding

Enable a Linux machine to act as a router:

#### Example:
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

---

### 5. Test Subnet Mask

To verify the subnet mask of a network interface:

#### Example:
```bash
ifconfig | grep "Mask"
```
Output:
```
inet addr:192.168.1.2  Bcast:192.168.1.255  Mask:255.255.255.0
```

### 6. Test Connectivity

Verifies communication with a device in another subnet.

```bash
ping -c 4 192.168.2.1
```
Output:
    ```
    PING 192.168.2.1 (192.168.2.1) 56(84) bytes of data.
    64 bytes from 192.168.2.1: icmp_seq=1 ttl=64 time=0.032 ms
    ```
  
---

## Real-Life Subnetting Example: Two Networks with 20 Computers Each

### Scenario
You have **two networks**, each with **20 computers**, connected to the **same router**. Subnetting is required to organize and manage these networks.

### Step-by-Step Solution

#### Step 1: Define Requirements
- **Hosts per Network**: 20 devices + some buffer (e.g., printers or future devices). Plan for 30 hosts per network.
- **Number of Networks**: 2.

#### Step 2: Choose an IP Range
Suppose the router is assigned the IP range **192.168.1.0/24** (256 IPs).

#### Step 3: Subnet the Range
To accommodate two networks:
- Required hosts per subnet: **30**.
- Subnet size: `/27` (32 IPs per subnet).

| Subnet ID         | Network Address | Subnet Mask     | Host Range          | Broadcast Address |
|--------------------|-----------------|-----------------|---------------------|-------------------|
| **Subnet 1**      | 192.168.1.0     | 255.255.255.224 | 192.168.1.1-192.168.1.30 | 192.168.1.31      |
| **Subnet 2**      | 192.168.1.32    | 255.255.255.224 | 192.168.1.33-192.168.1.62 | 192.168.1.63      |

#### Step 4: Assign IPs
1. **Subnet 1**:
   - Router IP: `192.168.1.1`.
   - Computers: `192.168.1.2` to `192.168.1.30`.

2. **Subnet 2**:
   - Router IP: `192.168.1.33`.
   - Computers: `192.168.1.34` to `192.168.1.62`.

#### Step 5: Configure the Router
To enable communication between subnets:
- Add static routes:
  ```bash
  route add -net 192.168.1.32/27 gw 192.168.1.1
  route add -net 192.168.1.0/27 gw 192.168.1.33
  ```
- Enable IP forwarding:
  ```bash
  echo 1 > /proc/sys/net/ipv4/ip_forward
  ```

#### Step 6: Test Connectivity
1. Ping between subnets:
   ```bash
   ping 192.168.1.34
   ```
2. Verify routing table:
   ```bash
   ip route
   ```

#### Key Takeaways
- Subnetting isolates traffic and improves performance.
- The router acts as a gateway between subnets.
- Proper subnet masks and static routes ensure seamless communication.

---
