# HTTP vs HTTPS

## What is HTTP?

**HTTP (Hypertext Transfer Protocol)** is the foundation of data communication on the web. It is used to transfer data like HTML pages, images, videos, and more between a web client (browser) and a server.

### How HTTP works:
- A client sends an HTTP request to a server.
- The server processes the request and sends back an HTTP response, usually containing the requested resource.
- HTTP is **stateless**, meaning each request-response pair is independent.

### Use Case:
HTTP is typically used for accessing web pages or APIs where encryption is not required.

---

## What is HTTPS?

**HTTPS (Hypertext Transfer Protocol Secure)** is an extension of HTTP with added security features. It encrypts the communication between the client and server using **SSL/TLS**.

### How HTTPS works:
- Adds a layer of encryption via SSL/TLS, ensuring that data exchanged is secure from eavesdropping or tampering.
- Verifies the authenticity of the server through an SSL certificate.

### Use Case:
HTTPS is essential for secure communication, such as online banking, e-commerce, and protecting sensitive user data.

---

## Key Differences Between HTTP and HTTPS

| Feature         | HTTP                          | HTTPS                           |
|-----------------|-------------------------------|---------------------------------|
| **Security**    | Unencrypted, prone to attacks | Encrypted, secure communication|
| **Port**        | 80                            | 443                             |
| **Certificate** | No SSL/TLS certificate needed | Requires SSL/TLS certificate    |
| **Performance** | Slightly faster               | Slightly slower due to encryption |

---

## Example Commands and Outputs

### 1. Fetching a Webpage (HTTP vs HTTPS)

- Command:
```bash
curl http://example.com
curl https://example.com
```
- Command Output:
```bash
<html>
<head><title>Example Domain</title></head>
<body>...</body>
</html>
```
- Output for both is same, in https what data is encrypted

### 2. Check SSL Certificate ( for HTTPS website)

- Command:
```bash
openssl s_client -connect tablesmate.vercel.app:443
```
- Output for above command contains certificate key, session id and various info for SSL Identification.

### 3. Analyze HTTPS header (HTTP vs HTTPS)

- Command:
```bash
curl -I https://tablesmate.vercel.app
```
- Command Output:
```bash
HTTP/2 200
accept-ranges: bytes
access-control-allow-origin: *
age: 435825
cache-control: public, max-age=0, must-revalidate
content-disposition: inline
content-type: text/html; charset=utf-8
date: Thu, 26 Dec 2024 17:18:24 GMT
etag: "51a5a44d4b8759e7ec7ba4b1f83addcc"
server: Vercel
strict-transport-security: max-age=63072000; includeSubDomains; preload
vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch
x-matched-path: /
x-vercel-cache: HIT
x-vercel-id: bom1::pnqb8-1735233504785-0cf1f8236a74
content-length: 20363
```

- output for the above command is header for the website such as status code, server, cache-control etc.
