# **30 Common Networking Protocols Questions for SRE/DevOps Interviews (With Answers)**  

Networking is **fundamental** for **SRE/DevOps** engineers, as it impacts **performance, security, and reliability**. Below are **30 commonly asked questions** about **networking protocols**, along with **detailed answers**.

---

## **1. What are the different layers of the OSI model?**  
The **OSI model** has **7 layers**:
1. **Physical** – Cables, switches, NICs.
2. **Data Link** – MAC addresses, Ethernet, ARP.
3. **Network** – IP, ICMP, routing.
4. **Transport** – TCP, UDP.
5. **Session** – Controls sessions (e.g., NetBIOS).
6. **Presentation** – Encryption, compression (SSL, TLS).
7. **Application** – HTTP, SSH, DNS.

---

## **2. What is the difference between TCP and UDP?**  
| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable | Unreliable |
| Error Checking | Yes (ACK, retransmission) | No |
| Speed | Slower | Faster |
| Use Cases | Web browsing, SSH | VoIP, gaming, DNS |

---

## **3. What are the key differences between IPv4 and IPv6?**  
| Feature | IPv4 | IPv6 |
|---------|------|------|
| Address Size | 32-bit | 128-bit |
| Format | Dotted decimal (e.g., 192.168.1.1) | Hexadecimal (e.g., fe80::1) |
| NAT Required? | Yes | No (Built-in Auto-Config) |
| Security | No built-in encryption | Integrated IPSec |

---

## **4. What is ARP (Address Resolution Protocol)?**  
- Maps **IP addresses to MAC addresses**.  
- View ARP cache:  
  ```sh
  ip neigh show
  ```

---

## **5. What is the difference between ARP and RARP?**  
| Feature | ARP | RARP |
|---------|-----|-----|
| Function | IP → MAC | MAC → IP |
| Used by | Hosts | Network devices |

---

## **6. What is ICMP, and what is it used for?**  
- **ICMP (Internet Control Message Protocol)** helps with **error reporting** and diagnostics.
- Used in **ping** and **traceroute**.

---

## **7. How does DNS work?**  
- Translates **domain names → IP addresses**.  
- DNS resolution involves:
  1. **Recursive resolver** (ISP's DNS).
  2. **Root DNS servers** (`.`).
  3. **TLD DNS servers** (`.com`, `.org`).
  4. **Authoritative DNS** (e.g., Google’s DNS).

---

## **8. What is the difference between authoritative and recursive DNS servers?**  
| Feature | Recursive DNS | Authoritative DNS |
|---------|--------------|------------------|
| Function | Resolves queries | Stores domain info |
| Examples | Google’s 8.8.8.8 | `ns1.example.com` |

---

## **9. What is a CDN, and how does it improve performance?**  
- **CDN (Content Delivery Network)** caches **static content** (e.g., images, videos) close to users.
- Reduces **latency and bandwidth usage**.

---

## **10. What is DHCP, and how does it work?**  
- **DHCP (Dynamic Host Configuration Protocol)** assigns **IP addresses** dynamically.
- Process:
  1. **Discover** (Client → Broadcast).
  2. **Offer** (DHCP Server → Client).
  3. **Request** (Client → Server).
  4. **Acknowledge** (Server → Client).

---

## **11. What is NAT (Network Address Translation)?**  
- Converts **private IPs ↔ public IPs**.
- Types:
  - **SNAT** (Source NAT) – Outbound connections.
  - **DNAT** (Destination NAT) – Inbound connections.

---

## **12. What is a VLAN, and why is it used?**  
- **VLAN (Virtual LAN)** separates networks **logically** within a switch.
- **Benefits**:
  - **Security** (isolating traffic).
  - **Scalability**.

---

## **13. What is a subnet mask?**  
- Defines the **network and host portions** of an IP.
- Example:
  - `255.255.255.0` (`/24`) → 256 hosts.
  - `255.255.0.0` (`/16`) → 65,536 hosts.

---

## **14. What is CIDR notation?**  
- **CIDR (Classless Inter-Domain Routing)** represents subnet masks:
  ```sh
  192.168.1.0/24
  ```
  - `/24` → 256 IPs.
  - `/16` → 65,536 IPs.

---

## **15. How does BGP work?**  
- **Border Gateway Protocol** exchanges routing information between **autonomous systems (AS)**.
- Uses **Path Vector Routing**.

---

## **16. What is the difference between BGP and OSPF?**  
| Feature | BGP | OSPF |
|---------|-----|-----|
| Type | Exterior Gateway Protocol (EGP) | Interior Gateway Protocol (IGP) |
| Use Case | Internet routing | Internal network routing |
| Protocol | Path vector | Link-state |

---

## **17. What is an MTU (Maximum Transmission Unit)?**  
- Maximum **packet size** before fragmentation.
- Check MTU:
  ```sh
  ip link show eth0
  ```
- Change MTU:
  ```sh
  ip link set eth0 mtu 1400
  ```

---

## **18. What is TCP slow start?**  
- **Congestion control mechanism** where TCP gradually increases the number of packets sent.

---

## **19. How does SSL/TLS work?**  
- Uses **encryption** for secure communication.
- **Handshake process**:
  1. Client **sends hello**.
  2. Server **sends certificate**.
  3. Key exchange.
  4. Secure communication begins.

---

## **20. What is the difference between HTTP and HTTPS?**  
- **HTTPS** = HTTP + TLS (Secure).

---

## **21. What is a proxy server?**  
- Intermediary between **client and server**.
- Types:
  - **Forward Proxy** – For clients accessing the internet.
  - **Reverse Proxy** – Protects backend services.

---

## **22. What is a load balancer?**  
- **Distributes traffic** across multiple servers.
- Types:
  - **L4 (Transport Layer)** – Uses TCP/UDP.
  - **L7 (Application Layer)** – Uses HTTP headers.

---

## **23. What is Anycast?**  
- **Same IP assigned to multiple locations**.
- Directs users to the **nearest** server.

---

## **24. How does a firewall work?**  
- Filters traffic **based on rules** (`iptables`, `nftables`).

---

## **25. What is QoS (Quality of Service)?**  
- Prioritizes **important network traffic** (e.g., VoIP, streaming).

---

## **26. How do WebSockets work?**  
- **Persistent** full-duplex TCP connection.

---

## **27. What is a GRE tunnel?**  
- **Encapsulates network traffic** over another protocol.

---

## **28. How does MPLS work?**  
- Uses **labels** to forward packets instead of IP lookups.

---

## **29. What is a DoS/DDoS attack?**  
- Overloads a target with excessive traffic.

---

## **30. What is Zero Trust Networking?**  
- Requires **authentication at every step**.

---

## **Final Thoughts**  
These **30 networking protocol questions** cover **fundamentals + real-world applications**, helping you **ace SRE/DevOps interviews**! 🚀