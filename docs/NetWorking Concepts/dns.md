# DNS (Domain Name System)

DNS is a critical component of the internet that translates human-friendly domain names (like `google.com`) into machine-readable IP addresses (like `172.217.16.238`). Without DNS, users would have to remember IP addresses to access websites.

---

## How DNS Works

1. **User Query**: When you enter a domain name in your browser, your computer contacts a DNS resolver (usually provided by your ISP) to resolve the domain name into an IP address.
2. **Response**: The resolver returns the IP address to your device, which then connects to the server hosting the website.

---

## Key DNS Records

- **A Record**: Maps a domain to an IPv4 address.  
  Example: `google.com -> 172.217.16.238`
  
- **AAAA Record**: Maps a domain to an IPv6 address.  

- **CNAME Record**: Alias for another domain.  
  Example: `www.example.com -> example.com`
  
- **MX Record**: Specifies mail servers for a domain.  

- **PTR Record**: Used for reverse DNS lookups (IP to domain).  

- **NS Record**: Points to the authoritative name servers for a domain.  

---

## Commands with Examples

### 1. Check DNS Resolution  
**Command**: `nslookup`  
## option 1:
```bash
nslookup tablesmate.vercel.app
```
### Command Output:
```bash
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
Name:   tablesmate.vercel.app
Address: 64.29.17.65
Name:   tablesmate.vercel.app
Address: 216.198.79.65
Name:   tablesmate.vercel.app
Address: 64:ff9b::d8c6:4f41
Name:   tablesmate.vercel.app
Address: 64:ff9b::401d:1141
```
- **Server**: Outputed Server IP associated with the server (here tablesmate.vercel.app)

## option 2:
```bash
nslookup 216.198.79.65
```
### Command Output:
```bash
65.79.198.216.in-addr.arpa      name = atl-cer1-755commercedr.cypresscom.net.
```
- **Name**: The domain name associated with an IP.
