Here are **30 commonly asked networking questions** in **SRE/DevOps job interviews**, along with detailed answers.

---

## **1. What is the difference between TCP and UDP?**
| Feature       | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|--------------|--------------------------------|----------------------------|
| Connection   | Connection-oriented | Connectionless |
| Reliability  | Reliable (ensures delivery) | Unreliable (no guarantees) |
| Speed        | Slower due to acknowledgments | Faster, no retransmission |
| Use Cases    | Web browsing, SSH, email | Streaming, gaming, VoIP |

---

## **2. How do you check network interfaces and their configurations in Linux?**
- `ip a`
- `ifconfig` (deprecated)
- `nmcli device show`
- `cat /etc/network/interfaces` (Debian-based)

---

## **3. How do you check active network connections?**
- `netstat -tulnp`
- `ss -tulnp`
- `lsof -i`
- `ip route show`

---

## **4. What is an IP address, and what are the differences between IPv4 and IPv6?**
- **IP Address**: A unique identifier assigned to a device on a network.
- **IPv4**: 32-bit, written as `192.168.1.1`.
- **IPv6**: 128-bit, written as `2001:db8::1`, supports more devices.

---

## **5. What are private IP addresses?**
- **Private IP ranges** (cannot be routed on the internet):
  - `10.0.0.0 - 10.255.255.255`
  - `172.16.0.0 - 172.31.255.255`
  - `192.168.0.0 - 192.168.255.255`

---

## **6. What command can be used to check if a remote host is reachable?**
- `ping example.com`
- `traceroute example.com`
- `mtr example.com` (better for debugging)

---

## **7. How do you check DNS resolution in Linux?**
- `nslookup example.com`
- `dig example.com`
- `host example.com`
- `cat /etc/resolv.conf`

---

## **8. How do you test if a specific port is open on a remote server?**
- `nc -zv <ip> <port>`
- `telnet <ip> <port>`
- `nmap -p <port> <ip>`

---

## **9. What is a subnet mask, and why is it important?**
- **Subnet mask** defines the network and host portions of an IP.
- Example:
  - IP: `192.168.1.10`
  - Subnet Mask: `255.255.255.0`
  - Network: `192.168.1.0/24`

---

## **10. What is the difference between a switch, router, and hub?**
| Device  | Function |
|---------|----------|
| **Switch** | Connects devices in a network, operates at Layer 2 (MAC) |
| **Router** | Connects different networks, operates at Layer 3 (IP) |
| **Hub** | Broadcasts data to all connected devices |

---

## **11. What are VLANs, and why are they used?**
- **VLAN (Virtual LAN)**: Segments a physical network into multiple logical networks.
- **Benefits**:
  - Improves security
  - Reduces broadcast domains
  - Enhances network management

---

## **12. How do you check the default gateway of a system?**
- `ip route show | grep default`
- `route -n`
- `netstat -rn`

---

## **13. What is NAT (Network Address Translation)?**
- Translates private IPs to public IPs for internet access.
- **Types**:
  - **SNAT**: Source NAT (used for outbound connections).
  - **DNAT**: Destination NAT (used for inbound connections).
  - **PAT**: Port Address Translation (many-to-one mapping).

---

## **14. What is the difference between TCP and ICMP?**
| Feature  | TCP | ICMP |
|----------|-----|------|
| Layer | Transport (Layer 4) | Network (Layer 3) |
| Reliable | Yes | No |
| Example Use | HTTP, SSH | Ping, Traceroute |

---

## **15. How do you find the MAC address of a system?**
- `ip link show`
- `ifconfig -a`
- `cat /sys/class/net/eth0/address`

---

## **16. What is ARP (Address Resolution Protocol)?**
- ARP maps IP addresses to MAC addresses.
- Check ARP cache:
  ```bash
  arp -a
  ```

---

## **17. How does DHCP work?**
- **DHCP (Dynamic Host Configuration Protocol)** dynamically assigns IPs.
- Steps:
  1. **Discover** (client requests IP)
  2. **Offer** (server responds with IP)
  3. **Request** (client requests assigned IP)
  4. **Acknowledge** (server confirms)

---

## **18. What is MTU (Maximum Transmission Unit)?**
- Defines max packet size for a network.
- Check:
  ```bash
  ip link show eth0
  ```
- Change:
  ```bash
  ip link set eth0 mtu 1400
  ```

---

## **19. How do you test network bandwidth?**
- `iperf -s` (start server)
- `iperf -c <server-ip>` (run test)

---

## **20. How do you troubleshoot a network issue?**
1. **Check connectivity**: `ping`
2. **Check routes**: `ip route`
3. **Check DNS**: `dig, nslookup`
4. **Check logs**: `dmesg`, `/var/log/syslog`
5. **Check firewall**: `iptables -L`

---

## **21. How do you check and modify firewall rules?**
- Check:
  ```bash
  iptables -L
  ```
- Add rule:
  ```bash
  iptables -A INPUT -p tcp --dport 80 -j ACCEPT
  ```

---

## **22. What is the difference between HTTP and HTTPS?**
| Feature  | HTTP | HTTPS |
|----------|------|------|
| Security | No encryption | Encrypted via TLS/SSL |
| Port | 80 | 443 |

---

## **23. What is latency, throughput, and jitter?**
- **Latency**: Delay in data transmission.
- **Throughput**: Amount of data transferred per second.
- **Jitter**: Variability in latency.

---

## **24. How do you check open ports on a server?**
- `netstat -tulnp`
- `ss -tulnp`

---

## **25. What is a load balancer, and why is it used?**
- **Distributes traffic** across multiple servers.
- **Types**:
  - L4 (TCP/UDP)
  - L7 (HTTP)

---

## **26. What is a CDN (Content Delivery Network)?**
- **Distributes static content** (images, JS, CSS) across edge servers.

---

## **27. What is BGP (Border Gateway Protocol)?**
- **Routing protocol for the internet**.
- Used by ISPs for **path selection**.

---

## **28. How do you capture network packets?**
- `tcpdump -i eth0`
- `wireshark`

---

## **29. How do you configure a static IP in Linux?**
- **Ubuntu/Debian**:
  ```yaml
  network:
    ethernets:
      eth0:
        addresses: [192.168.1.100/24]
        gateway4: 192.168.1.1
  ```
- **Apply changes**:
  ```bash
  netplan apply
  ```

---

## **30. What is Anycast, Unicast, and Multicast?**
| Type  | Description |
|--------|------------|
| **Unicast** | One-to-one communication |
| **Multicast** | One-to-many communication |
| **Anycast** | One-to-nearest communication |

---

### **Final Thoughts**
These **30 networking interview questions** cover **fundamental to advanced concepts** for **SRE/DevOps roles**. Hands-on practice with tools like `tcpdump`, `iptables`, and `netstat` will help you master them! 🚀