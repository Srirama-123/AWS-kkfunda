# Networking Fundamentals

## 1. IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---------|------|------|
| Address Length | 32-bit | 128-bit |
| Address Format | Decimal (e.g., 192.168.1.1) | Hexadecimal (e.g., 2001:db8::ff00:42:8329) |
| Address Space | ~4.3 billion addresses | 340 undecillion addresses |
| Header Complexity | Simple | More complex but efficient |
| Broadcast | Supported | Not supported (uses multicast instead) |
| Security | No built-in encryption | Integrated IPSec for security |
| NAT (Network Address Translation) | Commonly used due to address exhaustion | Not needed due to large address space |

### Key Differences:
- IPv6 provides a significantly larger address space.
- IPv6 eliminates NAT by providing enough addresses for all devices.
- IPv6 has built-in security features like IPSec.
- IPv6 uses more efficient packet processing.

---

## 2. IP Address Classes

| Class | First Octet Range | Default Subnet Mask | Number of Hosts |
|-------|------------------|---------------------|----------------|
| A | 1 - 126 | 255.0.0.0 (/8) | ~16 million per network |
| B | 128 - 191 | 255.255.0.0 (/16) | ~65,000 per network |
| C | 192 - 223 | 255.255.255.0 (/24) | 254 per network |
| D | 224 - 239 | N/A (Multicast) | N/A |
| E | 240 - 255 | Reserved | N/A |

- **Class A:** Large organizations and ISPs.
- **Class B:** Medium-sized businesses and universities.
- **Class C:** Small businesses and home networks.
- **Class D:** Used for **Multicasting** (not for host assignments).
- **Class E:** Reserved for future use or research.

---

## 3. Public vs Private IPs

### **Private IP Ranges (Non-Routable on the Internet)**

| Class | Private IP Range |
|-------|----------------|
| A | 10.0.0.0 - 10.255.255.255 |
| B | 172.16.0.0 - 172.31.255.255 |
| C | 192.168.0.0 - 192.168.255.255 |

- **Private IPs**: Used within local networks (LANs).
- **Public IPs**: Assigned by ISPs and used to access the internet.

### Why Private IPs?
- They help conserve IPv4 addresses.
- They require **NAT** (Network Address Translation) to connect to the internet.

---

## 4. CIDR (Classless Inter-Domain Routing)
CIDR replaces traditional class-based addressing by allowing more flexible subnetting.

- Instead of **Class A (255.0.0.0)**, CIDR allows **10.0.0.0/8**.
- Instead of **Class C (255.255.255.0)**, CIDR allows **192.168.1.0/24**.

### **CIDR Notation**

| CIDR | Subnet Mask | Number of Hosts |
|------|------------|---------------|
| /8 | 255.0.0.0 | 16.7M |
| /16 | 255.255.0.0 | 65K |
| /24 | 255.255.255.0 | 256 |

CIDR allows for:
- **Efficient allocation** of IP addresses.
- **Smaller subnets** to reduce waste.
- **Aggregation** of routes (route summarization).

---

## 5. Subnetting

### **Why Subnet?**
- Reduces **network congestion**.
- Enhances **security** by isolating networks.
- Efficient use of **IP addresses**.

### **Subnet Mask Table**

| Subnet Mask | CIDR | Number of Hosts |
|-------------|------|---------------|
| 255.0.0.0 | /8 | 16M |
| 255.255.0.0 | /16 | 65K |
| 255.255.255.0 | /24 | 256 |
| 255.255.255.128 | /25 | 128 |
| 255.255.255.192 | /26 | 64 |
| 255.255.255.224 | /27 | 32 |
| 255.255.255.240 | /28 | 16 |
| 255.255.255.248 | /29 | 8 |
| 255.255.255.252 | /30 | 4 |

Each subnet has:
1. **Network Address** (First address, e.g., 192.168.1.0)
2. **Broadcast Address** (Last address, e.g., 192.168.1.255)
3. **Usable Host Addresses** (Between network and broadcast)

### **Example: Subnetting 192.168.1.0/24 into /26**

#### **Subnet Mask:** 255.255.255.192 (/26) → 4 subnets

| Subnet | Network Address | First Host | Last Host | Broadcast |
|--------|----------------|------------|----------|-----------|
| 1 | 192.168.1.0 | 192.168.1.1 | 192.168.1.62 | 192.168.1.63 |
| 2 | 192.168.1.64 | 192.168.1.65 | 192.168.1.126 | 192.168.1.127 |
| 3 | 192.168.1.128 | 192.168.1.129 | 192.168.1.190 | 192.168.1.191 |
| 4 | 192.168.1.192 | 192.168.1.193 | 192.168.1.254 | 192.168.1.255 |

### **Key Takeaways:**
- **Each subnet gets 62 usable hosts** (excluding network/broadcast).
- **Larger subnet mask (higher CIDR) → fewer hosts per subnet**.
- **Smaller subnet mask (lower CIDR) → more hosts per subnet**.

---

## **Final Summary**
- **IPv4 vs. IPv6**: IPv6 has a larger address space, better security, and eliminates NAT.
- **IP Classes**: A, B, and C for hosts; D for multicast; E for reserved.
- **Public vs Private IPs**: Private IPs require NAT to access the internet.
- **CIDR**: Enables flexible subnetting and efficient IP usage.
- **Subnetting**: Divides networks for better management and security.
