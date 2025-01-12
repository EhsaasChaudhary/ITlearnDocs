# IP Addressing

## **IPv4 (Internet Protocol version 4)**

### **Overview**
IPv4 is the fourth version of the Internet Protocol and is widely used for identifying devices on a network using a logical addressing system. It was first introduced in the 1980s and has been the backbone of the internet since its inception.

### **Key Features**
1. **Address Format**: 
   - 32-bit address, represented in dotted-decimal format (e.g., `192.168.1.1`).
   - Provides approximately **4.3 billion unique addresses** (2³²).

2. **Address Classes**:
   - Divided into five classes (A, B, C, D, E), with A, B, and C being commonly used for host identification.
   - Example:
     - Class A: `1.0.0.0` to `126.0.0.0`
     - Class B: `128.0.0.0` to `191.255.0.0`
     - Class C: `192.0.0.0` to `223.255.255.0`

3. **Subnetting**:
   - Allows dividing a network into smaller, manageable segments.

4. **Broadcast**:
   - IPv4 supports broadcast communication, sending data to all devices on a subnet.

5. **Challenges**:
   - Limited address space due to the explosion of internet-connected devices.
   - Security vulnerabilities inherent in the protocol.

---

## **IPv6 (Internet Protocol version 6)**

### **Overview**
IPv6 was developed as a successor to IPv4 to address its limitations, especially the exhaustion of IP addresses. Introduced in 1998, IPv6 provides a much larger address space and improved features.

### **Key Features**
1. **Address Format**:
   - 128-bit address, represented in hexadecimal colon-separated format (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
   - Provides approximately **340 undecillion addresses** (2¹²⁸), which is vastly larger than IPv4.

2. **No Classes**:
   - Does not use traditional address classes. Instead, it employs hierarchical addressing for efficient routing.

3. **Simplified Header**:
   - Designed with a simplified and efficient header compared to IPv4.

4. **Security**:
   - Built-in support for IPsec (Internet Protocol Security), making IPv6 inherently more secure.

5. **No Broadcast**:
   - Replaces broadcast communication with multicast and anycast, which are more efficient.

6. **Auto-Configuration**:
   - Supports both stateful (DHCPv6) and stateless (SLAAC) address auto-configuration.

7. **Compatibility**:
   - Includes mechanisms like dual-stack and tunneling to coexist with IPv4 during the transition period.

---

## **Comparison: IPv4 vs. IPv6**

| Feature                  | IPv4                      | IPv6                                   |
|--------------------------|---------------------------|----------------------------------------|
| **Address Size**         | 32-bit                   | 128-bit                                |
| **Address Format**       | Decimal (e.g., 192.0.2.1) | Hexadecimal (e.g., 2001:0db8::1)       |
| **Address Space**        | ~4.3 billion addresses    | ~340 undecillion addresses             |
| **Security**             | Optional (IPsec support) | Mandatory (IPsec integration)          |
| **Header Complexity**    | More complex             | Simplified                             |
| **Broadcast**            | Supported                | Replaced by multicast/anycast          |
| **Auto-Configuration**   | Limited                  | Extensive support for auto-configuration |
| **Network Efficiency**   | Less efficient           | Improved efficiency and routing        |

---

## **Why IPv6?**
- The rapid growth of the internet, IoT devices, and mobile networks necessitated a protocol that could handle billions of new devices.
- IPv6 offers scalability, better performance, and more robust security, making it the future of internet addressing. 

Despite IPv6's advantages, IPv4 remains widely used due to compatibility issues, the slow transition process, and the development of technologies like NAT (Network Address Translation) that prolong IPv4's usability.

## Command: `ifconfig`

### Usage

- **`ifconfig`**: Displays active network interfaces along with their IP addresses, subnet masks, and MAC addresses.
- **`ifconfig -a`**: Lists detailed information about all network interfaces, including inactive ones.

### Example Output

```bash
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.24.240.76  netmask 255.255.240.0  broadcast 172.24.255.255
        inet6 fe80::215:5dff:fe04:d5b0  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:04:d5:b0  txqueuelen 1000  (Ethernet)
        RX packets 15114  bytes 61383003 (61.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11239  bytes 827892 (827.8 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 60  bytes 7052 (7.0 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 60  bytes 7052 (7.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
## Key Components of `ifconfig` Output

## `eth0` - Ethernet Interface:

- **Flags**: Indicates the interface state and capabilities.
  - **UP**: The interface is active.
  - **BROADCAST**: Supports broadcast of packets.
  - **RUNNING**: The interface driver is operational.
  - **MULTICAST**: Supports multicast communication.
- **MTU (Maximum Transmission Unit)**: Maximum size of packets (in bytes). Default is 1500.

### IPv4 Information

- **`inet`**: IPv4 address of the interface (e.g., `172.24.240.76`).
- **`netmask`**: Subnet mask, indicating the size of the subnet. For example:
  - `255.255.240.0` represents a 20-bit network and a 12-bit host (2^12 = 4096 IPs).
  - **Binary**: `11111111.11111111.11110000.00000000`.
- **`broadcast`**: Address to broadcast packets to all devices on the subnet.

### IPv6 Information

- **`inet6`**: IPv6 address of the interface (e.g., `fe80::215:5dff:fe04:d5b0`).
- **`prefixlen`**: Subnet size (e.g., `64`).
- **`scopeid`**: Specifies the scope of the IPv6 address:
  - **link**: Valid only on the same physical or logical link (e.g., `fe80::/10`).
  - **global**: Valid across the entire IPv6 internet.

### MAC Address

- **`ether`**: MAC address of the interface (e.g., `00:15:5d:04:d5:b0`).

### Transmission Queue

- **`txqueuelen`**: Length of the queue for outgoing packets.

### Packet Statistics

```bash
RX packets 12445 bytes 50759954 (50.7 MB):
Number of packets (12445) and total data (50.7 MB) received by this interface.

RX errors 0 dropped 0 overruns 0 frame 0:
Indicates no errors occurred during reception.

TX packets 9490 bytes 699021 (699.0 KB):
Number of packets (9490) and total data (699 KB) transmitted by this interface.

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0:
Indicates no errors occurred during transmission.
```

### RX (Receive)

- **Packets**: Number of packets received.
- **Bytes**: Total data received.
- **Errors, Drops, Overruns, Frame**: Error statistics.

### TX (Transmit)

- **Packets**: Number of packets transmitted.
- **Bytes**: Total data transmitted.
- **Errors, Drops, Overruns, Carrier, Collisions**: Error statistics.


## `lo` - Loopback Interface:

Used for internal communication within the system.

### Flags
- UP
- LOOPBACK
- RUNNING

### MTU (Maximum Transmission Unit):
- 65536 (used internally)

### IPv4 Loopback:
- **inet**: 127.0.0.1 (commonly referred to as localhost.)
  - Traffic sent here stays within the same machine.

### IPv6 Loopback:
- **inet6**: ::1 (equivalent to 127.0.0.1 for IPv4)

### Packet Statistics:
```bash
RX packets 48 bytes 5650 (5.6 KB):
Traffic received by the loopback interface.

TX packets 48 bytes 5650 (5.6 KB):
Traffic sent over the loopback interface.
```
- **RX (Receive)**: Traffic received by the loopback interface.
- **TX (Transmit)**: Traffic sent over the loopback interface.

No errors or dropped packets are reported, as expected for local traffic.

## Command: `ping`

### Usage Example:
- Test if a host is reachable.

```bash
ping tablesmate.vercel.app
```

### Example Output:

```bash
PING tablesmate.vercel.app (216.198.79.65) 56(84) bytes of data.
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=1 ttl=241 time=58.0 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=2 ttl=241 time=54.9 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=3 ttl=241 time=65.1 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=4 ttl=241 time=54.4 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=5 ttl=241 time=56.8 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=6 ttl=241 time=72.5 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=7 ttl=241 time=75.1 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=8 ttl=241 time=65.8 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=9 ttl=241 time=51.4 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=10 ttl=241 time=51.5 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=11 ttl=241 time=65.1 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=12 ttl=241 time=44.6 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=13 ttl=241 time=50.7 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=14 ttl=241 time=83.7 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=15 ttl=241 time=43.2 ms
64 bytes from atl-cer1-755commercedr.cypresscom.net (216.198.79.65): icmp_seq=16 ttl=241 time=68.1 ms
^C
--- tablesmate.vercel.app ping statistics ---
16 packets transmitted, 16 received, 0% packet loss, time 15182ms
rtt min/avg/max/mdev = 43.209/60.052/83.673/10.957 ms
```

### Components of `ping` Output

- **216.198.79.65**: Resolved IP of the domain.
- **56(84) bytes of data**: Each ICMP packet contains 56 bytes of data, and the total packet size is 84 bytes (56 bytes of data + 28 bytes for headers).
- **64 bytes**: Size of response packet.
- **atl-cer1-755commercedr.cypresscom.net**: The hostname corresponding to the IP address of the server (216.198.79.65).
- **icmp_seq**: The sequence number of ICMP packets (starts with 1 and increments).
- **ttl**: The Time-To-Live (TTL) value, indicating the maximum number of network hops the packet can take before being discarded. A TTL of 241 suggests the packet traversed several hops but is still within its initial limit.
- **time**: The round-trip time (RTT) for the packet, measured in milliseconds. This indicates how long it took for the packet to travel to the server and back.

### Summary:

- **16 received**: The total number of packets successfully received back from the server.
- **16 packets transmitted**: The total number of ICMP packets sent to the server.
- **0% packet loss**: Indicates no packets were lost, showing a reliable connection.
- **time 15182ms**: Total time taken to transmit and receive all packets.

### RTT Statistics:

- **min**: Minimum RTT recorded (43.209 ms).
- **avg**: Average RTT across all packets (60.052 ms).
- **max**: Maximum RTT recorded (83.673 ms).
- **mdev**: Mean deviation, indicating variability in RTT (10.957 ms). A lower value suggests more consistent latency.

---

## Command: `traceroute`

### Usage Example:
- Network diagnosis, shows the path that packets take to reach the destination.

```bash
traceroute tablesmate.vercel.app
```

### Example Output:

```bash
traceroute to tablesmate.vercel.app (64.29.17.65), 64 hops max
  1   172.24.240.1  0.740ms  0.357ms  0.293ms
  2   192.168.28.246  13.179ms  2.941ms  2.385ms
  3   *  *  *
  4   192.168.173.209  31.011ms  38.245ms  22.654ms
  5   192.168.203.1  28.829ms  26.160ms  28.298ms
  6   *  *  *
  7   123.63.198.92  74.375ms  30.335ms  28.007ms
  8   182.19.106.103  31.764ms  60.714ms  29.920ms
  9   *  *  *
 10   *  *  *
|
|
|
 64  *  *  *
```
### Elements in Traceroute:
- **Hop Number**: Each line starts with a hop number, indicating the sequential step in the route.
- **IP Address**: The IP address of the router or device at that hop.
- **Round-Trip Times (RTT)**: The time (in milliseconds) it takes for a packet to travel to that hop and back, displayed for three attempts.
- * : Indicates that no response (ICMP packet) was received from that hop within the timeout period due to firewall (for security).
