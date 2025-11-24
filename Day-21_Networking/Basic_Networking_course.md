# 1️ Introduction to Networking

##  What is a Network?
A network is a collection of interconnected devices (computers, phones, servers) that communicate and share resources.

### Why Networks Matter
- Communication (email, chat)
- File and resource sharing
- Remote access
- Internet connectivity
- Centralized management

---

# 2️ Types of Networks

##  Classification by Area
| Network | Range | Examples |
|--------|--------|----------|
| PAN | 1–10 m | Bluetooth |
| LAN | Building | Wi-Fi, Ethernet |
| MAN | Campus | University network |
| WAN | Global | The Internet |

---

##  Network Topologies


| Topology | Pros | Cons |
|----------|------|------|
| Star | Easy to manage | Switch failure affects the network |
| Mesh | Fault-tolerant | Expensive & complex |
| Bus | Simple | Collisions, not scalable |

---

# 3️ Networking Models

#  OSI Model (7 Layers)

| Layer | Purpose | Examples |
|-------|----------|----------|
| 7. Application | User operations | HTTP, FTP |
| 6. Presentation | Encryption, encoding | SSL, TLS |
| 5. Session | Connection control | API sessions |
| 4. Transport | Reliability | TCP, UDP |
| 3. Network | Routing | IP, ICMP |
| 2. Data Link | Local delivery | MAC, ARP |
| 1. Physical | Signals | Cables, fiber |

---

#  TCP/IP Model (4 Layers)

| Layer | Function | Protocols |
|--------|----------|------------|
| Application | User services | DNS, HTTP |
| Transport | Segments | TCP, UDP |
| Internet | Routing | IP |
| Network Access | Frames | Ethernet, Wi-Fi |

---

# 4️ IP Addressing & Subnetting

## 🔸 IPv4 Basics
- 32-bit numeric address
- Example: `192.168.1.1`

### Address Classes
| Class | Range | Use |
|--------|--------|------|
| A | 1–126 | Large networks |
| B | 128–191 | Medium networks |
| C | 192–223 | Small networks |

### Private Ranges
- 10.0.0.0/8  
- 172.16.0.0/12  
- 192.168.0.0/16

---

##  Subnetting (Detailed)

### Problem:
Network: `192.168.10.0/24`  
Need: 4 subnets

### Step-by-step:
- Borrow 2 bits → /26  
- Mask: `255.255.255.192`  
- Hosts per subnet: 64

### Subnets:
1. 192.168.10.0  
2. 192.168.10.64  
3. 192.168.10.128  
4. 192.168.10.192  

---

##  IPv6 Overview
- 128-bit addresses  
- Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

- Integrated IPSec  
- No more NAT needed  

---

# 5️ Routing Concepts

##  What is Routing?
Routers connect **different networks** and use routing tables to forward packets.

---

##  Types of Routing
### Static Routing
- Manually configured  
- Very stable  
- Not scalable  

### Dynamic Routing
Automatically learns routes via protocols:

| Protocol | Type |
|----------|------|
| RIP | Distance vector |
| OSPF | Link state |
| EIGRP | Hybrid |
| BGP | Path vector (Internet routing) |

---

##  Routing Metrics
Used by protocols to choose best path:
- Hop count  
- Bandwidth  
- Delay  
- Cost  
- Reliability  

---

# 6️ Switching & LAN Technologies

##  Switch Basics
Switches operate at **Layer 2** and use **MAC address tables** to forward frames.

### Concepts:
- Collision Domain: 1 per port  
- Broadcast Domain: 1 per VLAN  
- Switch learns MAC dynamically  

---

##  VLANs (Virtual LANs)

### Example Setup
VLAN 10 - HR
VLAN 20 - Finance
VLAN 30 - IT



### Benefits
- Network segmentation  
- Better security  
- Reduced broadcast traffic  

---

##  Trunking (802.1Q)
Carries traffic for multiple VLANs.
Switch A ===(TRUNK)=== Switch B


---

##  STP (Spanning Tree Protocol)
Prevents switching loops.

States:
- Blocking  
- Listening  
- Learning  
- Forwarding  

---

# 7️ Wireless Networking

##  Wi-Fi Standards

| Standard | Band | Speed |
|----------|------|--------|
| 802.11n | 2.4/5 GHz | 600 Mbps |
| 802.11ac | 5 GHz | 1.3 Gbps |
| 802.11ax (Wi-Fi 6) | Both | Multi-Gbps |

---

##  Wireless Security
Ranking (best → worst):
1. WPA3  
2. WPA2  
3. WPA  
4. WEP *(avoid entirely)*

---

# 8️ Network Services & Protocols

##  Common Ports

| Service | Port | Protocol |
|---------|------|----------|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| DNS | 53 | TCP/UDP |
| DHCP | 67/68 | UDP |
| SSH | 22 | TCP |
| FTP | 21 | TCP |
| SNMP | 161 | UDP |

---

##  DHCP – DORA Process
D - Discover
O - Offer
R - Request
A - Acknowledge



---

# 9️ Network Security

##  Common Attacks
- ARP Poisoning  
- DNS Spoofing  
- MITM  
- DoS/DDoS  
- Password Brute Force  
- Packet Sniffing  

---

##  Security Devices
- Firewall  
- IDS/IPS  
- Proxy server  
- VPN concentrator  
- Authentication server (RADIUS/TACACS+)  

---

#  10 Network Troubleshooting

##  OSI Layer Troubleshooting (Bottom-Up)
1. Physical – cables, ports  
2. Data Link – MAC, ARP  
3. Network – IP addressing  
4. Transport – TCP/UDP  
5. Session  
6. Presentation  
7. Application  

---

##  Tools
- `ping`  
- `tracert/traceroute`  
- `ipconfig / ifconfig`  
- `arp -a`  
- `netstat`  
- `nslookup` / `dig`  
- Wireshark  

---

# Updating pratice details.
basic concepts:

IP Address: This is a unique identifier assigned to each device on a network. Think of it like a postal address for computers.

MAC Address: A hardware address used to identify devices on a local network. It’s unique to each network interface card (NIC) and operates at the data link layer.

Protocol: These are the rules that define how data is transmitted over the network. Examples include TCP/IP, HTTP, FTP, and DNS.

Packets: Data is broken down into smaller packets when being transmitted over a network. Each packet contains part of the data, as well as information about its destination, so it can be reassembled at the receiving end.

-----
1. ipconfig /all
- Command to display the IP and MAC address
<img width="920" height="745" alt="image" src="https://github.com/user-attachments/assets/dac47129-98f3-4189-8423-7789b70a340e" />

---
2. arp -a
- To check all the IP and macs of router
<img width="547" height="185" alt="image" src="https://github.com/user-attachments/assets/0c7234ba-be06-4acc-b87e-96d8253815ac" />

---
3. OSI model
<img width="431" height="498" alt="image" src="https://github.com/user-attachments/assets/2ebafeb8-209a-48c7-80ab-c4e644598aa5" />

---
4. Switches
- A switch is a device used to connect devices within the same local network (LAN) and manage traffic between them. It operates primarily at Layer 2 (Data Link Layer) of the OSI model, but some advanced switches can operate at Layer 3 (Network Layer) as well.

---
5. Routers
- A router is a device that connects different networks together. It operates at Layer 3 (Network Layer) of the OSI model and is responsible for directing data between different networks, such as between a home network (LAN) and the internet (WAN).
<img width="768" height="214" alt="image" src="https://github.com/user-attachments/assets/c1fac94c-6175-4d32-8c43-9b5b14776991" />

---














